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

The main options to be used are:

* `-t`: This sets the targeted SIEM backend you wish to get queries for (Elasticsearch, Splunk, QRadar, ElastAlert).
* `-c`: This sets the configuration file used for the conversion. The file handles the field mappings between the rule and the target SIEM environment, ensuring that the necessary fields are correct for performing investigations on your environment.
* `--backend-option`: This allows you to pass a backend configuration file or individual modifications that dictate alert options for the target SIEM environment. For example, in ElasticSearch, we can specify specific field properties to be our primary keyword_field to be searched against, such as fields that end in the `.keyword` or `.security` fields below:

        python3.9 sigmac -t es-qs -c tools/config/winlogbeat.yml --backend-option keyword_field=".keyword" --backend-option analyzed_sub_field_name=".security"
        
We can convert our AnyDesk Installation rule  to a Splunk alert as shown below:

        python3.9 sigmac -t splunk -c splunk-windows Process_Creation_AnyDesk_Installation.yml
        
### Uncoder.io

Uncoder.IO is an open-source web Sigma converter for numerous SIEM and EDR platforms. It is easy to use as it allows you to copy your Sigma rule on the platform and select your preferred backend application for translation.

We can copy our rule and convert it into different queries of our choice. Below, the rule has been converted into Elastic Query, QRadar and Splunk. You can copy the translation into the SIEM platform to test for any matches.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/85b62547-9e70-48fb-9643-05bc3f6166c1)

We have to give the yaml file we did for the AnyDesk Installation Sigma rule as input and convert it as elastic query through `uncoder.io`

We will get the output query :

        (process.command_line.text:"*\-\-install*" AND process.command_line.text:"*\-\-start\-with\-win*" AND process.working_directory.text:"*C\:\\ProgramData\\AnyDesk.exe*")

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/03565285-d168-4c8d-b1e7-d97fcd1049fe)

Now we use it to analyse log data from the launched machine on the Kibana dashboard

We have to remove `\` and `*` as it will show errors for the part of regex.

After removing those, the Elastic query will be:

        (process.command_line.text:--install AND process.command_line.text:--start-with-win AND process.working_directory.text:C\:\\ProgramData\\AnyDesk.exe)

Now feed it to the kibana search space.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/0c409783-f673-4561-b34e-1751a118a790)

### What command line tool is used to convert Sigma rules?

        Sigmac
        
### At what time was the AnyDesk installation event created? [MMM DD, YYYY @ HH:MM:SS]

        Jun 28, 2022 @ 22:19:00

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/b676242b-6f4c-41e7-84e0-619d234f41a7)

### What version of AnyDesk was installed?

        7.0.10

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/c6837558-a3da-465e-905f-8593dfc6342b)

## Practical Scenario (Task 6)

Your organisation, Aurora, has recently been experiencing unusual activities on some of the machines on the network. Amongst these activities, the IT Manager noted that an unknown entity created some scheduled tasks on one of the machines and that a ransomware activity was also recorded.

The SOC Manager has approached you to find ways of identifying these activities from the logs collected on the environment. It would be best if you used Sigma rules to set your detection parameters and perform search queries through the Kibana dashboard.

To complete the task, you will require two Sigma rules processed into ElasticSearch to query for the scheduled task and the ransomware events. Below are tips to construct a good rule for the task:

* For the Scheduled Task, understand that it is a process creation event.
* The rule's detection variables should contain image and commandline arguments.
* You may choose to exclude SYSTEM accounts from the query.
* For the ransomware activity, you'll look for a created file ending with .txt.
* The file creation process would be run via cmd.exe.
* Change the default time window on Kibana from the default last 30 days to last 1 year (or ensure it encompasses 2022).

The query of above task will be:

        (process.executable.text:"\schtasks.exe" AND process.command_line.text: "*schtasks*" AND process.command_line.text: *Create*)
        
### To detect the creation of the scheduled task, what detection value would be appropriate for the Sigma rule?

        schtasks.exe
        
### What was the name of the scheduled task created?

        spawn
        
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/17a4ae27-4fa9-4e96-bb5b-cbffb3032cd3)

In the above command, it will create task called spawn. Thus, the name of the scheduled task is `spawn`

### What time is this task meant to run?

        20:10
        
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/dff689af-1455-4705-95d9-687e51fc8af1)

Time is also mentioned there when the task is created.

### To detect ransomware activity, what logsource category would be appropriate for the Sigma rule?

        file_event

* To detect this logsource category, we need to refer the Sigma taxonomy.
* https://github.com/SigmaHQ/sigma-specification/blob/main/Taxonomy_specification.md
* Look for Event_ID : 11

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/3e54976e-94cb-4368-928a-dd61a48bd6f7)

### What is the name of the created file?

        YOUR_FILES.TXT

Query :

    (process.executable.text:"\cmd.exe" AND file.path.text:*.txt)

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/5204b23e-e808-4c65-8e2e-8770ec42f46e)

### What was the event code associated with the activity?

        11
        
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/9e64037a-caad-4028-a71c-7c5e04f7788a)

### What were the contents of the created ransomware file?

        echo T1486 - Purelocker Ransom Note

* We know already that created ransomware file is `YOUR_FILES.txt`
* Let's search that in kibana search

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/30bc79f1-c139-4cf9-90c5-4281e46f28d7)

* We got 4 hits.
* First file that entered is the one which consists of contents. Inspecting the last hit will display us the contents of the ransomware file.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/1859d2ac-ea4f-4761-923b-599ec9d11b7e)
