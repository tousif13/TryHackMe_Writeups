# Sigma

> Sigma is an open-source generic signature language developed by Florian Roth & Thomas Patzke to describe log events in a structured format. This allows for quick sharing of detection methods by security analysts. It is mentioned that "Sigma is for log files as Snort is for network traffic, and Yara is for files."

> Sigma makes it easy to perform content matching based on collected logs to raise threat alerts for analysts to investigate. Log files are usually collected and stored in a database or SIEM solution for further analysis.

### Sigma Development Process

* `Sigma Rule Format`: Generic structured log descriptions written in YAML.
* `Sigma Converter`: A set of python scripts that will process the rules on the backend and perform custom field matching based on specified SIEM query language.
* `Machine Query`: Resulting search query to filter out alerts during investigations. The query will be based on the specified SIEM.

### Sigma Rule Syntax (Task 3)

Sigma rules are written in YAML Ain't Markup Language (YAML)

Download and open the Task file provided by the tryhackme to get the understanding of sigma rule syntax.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/0fe51129-21b0-4d75-b678-f5d6f3a9702f)

* `Title`: Names the rule based on what it is supposed to detect. This should be short and clear.
* `ID`: A globally unique identifier mainly used by the developers of Sigma to maintain the order of identification for the rules submitted to the public repository, found in UUID format. We can also add references that comes under Derived, Obsolete, Merged, Renamed and Similar etc.
* `Status`: Describes the stage in which the rule maturity is at while in use. There are five declared statuses that you can use: Stable, Test, Experimental, Deprecated and Unsupported. 
* `Description`: Provides more context about the rule and its intended purpose. With the rule, you can be as verbose as possible on the malicious activity you intend to detect.
* `Logsource`: Describes the log data to be used for the detection. It consists of other optional attributes: Product, Category, Service and Definition.
* `Detection`: A required field in the detection rule describes the parameters of the malicious activity we need an alert for. The parameters are divided into two main parts: the search identifiers - the fields and values that the detection should be searching for -  and condition expression - which sets the action to be taken on the detection, such as selection or filtering.
* `FalsePositives`: A list of known false positive outputs based on log data that may occur.
* `Level`: Describes the severity with which the activity should be taken under the written rule. The attribute comprises five levels: Informational -> Low -> Medium -> High -> Critical
* `Tags`: Adds information that may be used to categorise the rule. Tags may include values for CVE numbers and tactics and techniques from the MITRE ATT&CK framework. Sigma developers have defined a list of predefined tags.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/319eba6f-a703-46e4-bd93-a77327190975)

The detection section of the rule describes what you intend to search for within the log data and how the selection and filters are to be evaluated. The definition of the search identifiers can comprise two data structures - `lists and maps` - which dictate the order in which the detection would be processed

### Which status level could lead to false results or be noisy, but could also identify interesting events?

    Experimental
    
### The rule detection comprises two main elements: __ and condition expressions.

    Search Identifiers
    
### What two data structures are used for the search identifiers?

    Lists and maps
    
## Rule Writing and Conversion (Task 4)

### Scenario 

> Administrators rely on remote tools to ensure devices are configured, patched and maintained. However, your SOC Manager just received and shared intel on how AnyDesk, a legitimate remote tool, can be downloaded and installed silently on a user's machine using the file description. As a SOC analyst, you have been tasked to analyse the intel and write a Sigma rule to detect the installation of AnyDesk on Windows devices.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/4bef20fb-5ee6-421e-a2a5-f8101e556861)

### Step 1: Intel Analysis

The shared intel shows us a lot of information and commands to download and install AnyDesk. An adversary could wrap this up in a malicious executable sent to an unsuspecting user through a phishing email. We can start picking out values that would be important for detecting any occurrence of an installation.

* `Source URL`: This marks the download source for the software, highlighted by the `$url` variable.
* `Destination File`: The adversary would seek to identify a destination directory for the download. This is marked by the `$file` variable
* `Installation Command`: From the intel, we can see that various instances of `CMD.exe` are being used to install and set a user password by the script. From this, we can pick out the installation attributes such as `--install`, `--start-with-win` and `--silent`.
* `Adversary Persistence`: The adversary would seek to maintain access to the victim's machine. In this instance, they would create a user account `oldadministrator` and give the user elevated privileges to run other tasks.
* `Registry Edit`: We can also pick out the registry edit, where the added user is added to a `SpecialAccounts` user list.

### Step 2: Rule Identification

We can start building our rule by filling in the Title and Description sections, given the information that we are looking for an AnyDesk remote tool installation. Let us also set the status as `experimental` , as this rule will be tested internally.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/5918de16-ec9c-4af0-a2a4-ff7c4221baa7)

### Step 3: Log Source

As indicated from our intel, Windows devices would be our targetted device. Windows Eventlog and Sysmon provide events such as process creation and file creation. Our case focuses on the creation of an installation process, thus listing our logsource category as `process_creation`.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/564f22d0-2de1-467b-b377-d5d5e7eaed36)

### Step 4: Detection Description

The detection section of our rule is the essential part. The information derived from the intel will define what we need to detect within our environment. For the AnyDesk installation, we noted the installation commands that would be used by the adversary that contains the strings: `install`, and `start-with-win`. We can therefore write our search identifiers as below with the modifiers `contains` and `all` to indicate that the rule will match all those values.

Additionally, we can include searching for the current directory where the commands will be executed from, `C:\ProgramData\AnyDesk.exe`

For our condition expression, this evaluates the selection of our detection.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/90c4e32f-eeaa-4d8f-822d-6f34e4e00373)

### Step 5: Rule Metadata

After adding the required and vital bits to our rule, we can add other helpful information under level, tags, references and false positives. We can reference the MITRE ATT&CK Command and Control tactic and its corresponding `T1219` technique for tags.


With this, we have our rule, which we can now convert to the SIEM query of our choice and test the detection.

### Rule Conversion

Sigma rules need to be converted to the appropriate SIEM target that is being utilised to store all the logs. Using the rule we have written above, we shall now learn how to use the sigmac and uncoder.io tools to convert them into ElasticSearch and Splunk queries.

### Sigmac

> Sigmac is a Python-written tool that converts Sigma rules by matching the detection log source field values to the appropriate SIEM backend fields. As part of the Sigma repo (Advisable to clone the repo to get the tool and all the available rules published by the Sigma team), this tool allows for quick and easy conversion of Sigma rules from the command line. Below is a snippet of how to use the tool through its help command, and we shall display the basic syntax of using the tool by converting the AnyDesk rule we have written to the Splunk query.

