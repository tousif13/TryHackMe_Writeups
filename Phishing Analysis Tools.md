# Phishing Analysis Tools

##  What information should we collect? (Task 2)

Below is a checklist of the pertinent information an analyst (you) is to collect from the email header:

* Sender email address
* Sender IP address
* Reverse lookup of the sender IP address
* Email subject line
* Recipient email address (this information might be in the CC/BCC field)
* Reply-to email address (if any)
* Date/time

Afterward, we draw our attention to the email body and attachment(s) (if any).

Below is a checklist of the artifacts an analyst (you) needs to collect from the email body:

* Any URL links (if an URL shortener service was used, then we'll need to obtain the real URL link)
* The name of the attachment
* The hash value of the attachment (hash type MD5 or SHA256, preferably the latter)

## Email header analysis (Task 3)

Some of the pertinent information that we need to collect can be obtained visually from an email client or web client (such as Gmail, Yahoo!, etc.). But some information, such as the sender's IP address and reply-to information, can only be obtained via the email header.

Email Header Analysis Tools :

* `Google Messageheader` - https://toolbox.googleapps.com/apps/messageheader/analyzeheader 
* `Message Header Analyzer`- https://mha.azurewebsites.net/
* `MailHeader` - https://mailheader.org/
* `IPinfo` - https://ipinfo.io/
* `URLScan.io` - https://urlscan.io/
* `Talos Reputation Center`: https://talosintelligence.com/reputation

### What is the official site name of the bank that capitai-one.com tried to resemble?

    capitalone.com
    
## Email body analysis (Task 4)

Now it's time to direct your focus to the email body. This is where the malicious payload may be delivered to the recipient either as a link or an attachment

Links can be extracted manually, either directly from an HTML formatted email or by sifting through the raw email header.

`URL Extractor`: https://www.convertcsv.com/url-extractor.htm (To extract URLs from the email)

After extracting the URLs, the next step is to check the reputation of the URLs and root domain. You can use any of the tools mentioned in the previous task to aid you with this.

If the email has an attachment, you'll need to obtain the attachment safely. Accomplishing this is easy in Thunderbird by using the Save button.

There are many tools available to help us with this, but we'll focus on two primarily; they are listed below:

> The Cisco Talos Intelligence Group maintains a reputation disposition on billions of files. This reputation system is fed into the AMP, FirePower, ClamAV, and Open-Source Snort product lines. The tool below allows you to do casual lookups against the Talos File Reputation system. This system limits you to one lookup at a time, and is limited to only hash matching. This lookup does not reflect the full capabilities of the Advanced Malware Protection (AMP) system

`Talos File Reputation`: https://talosintelligence.com/talos_file_reputation

`VirusTotal`: https://www.virustotal.com/gui/ (Analyze suspicious files and URLs to detect types of malware, automatically share them with the security community.)

### How can you manually get the location of a hyperlink?

    Copy Link Location
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/b754391d-a115-4309-9963-8bfee6c176c6)

## Malware Sandbox (Task 5)

Luckily as Defenders, we don't need to have malware analysis skills to dissect and reverse engineer a malicious attachment to understand the malware better.

There are online tools and services where malicious files can be uploaded and analyzed to better understand what the malware was programmed to do. These services are known as malware sandboxes

For instance, we can upload an attachment we obtained from a potentially malicious email and see what URLs it attempts to communicate with, what additional payloads are downloaded to the endpoint, persistence mechanisms, Indicators of Compromise (IOCs), etc

`Any.Run`: https://app.any.run/

> Analyze a network, file, module, and the registry activity. Interact with the OS directly from a browser. See the feedback from your actions immediately

`Hybrid Analysis`: https://www.hybrid-analysis.com/

> This is a free malware analysis service for the community that detects and analyzes unknown threats using a unique Hybrid Analysis technology.

`Joe Security`: https://www.joesecurity.org/

> Joe Sandbox empowers analysts with a large spectrum of product features. Among them: Live Interaction, URL Analysis & AI based Phishing Detection, Yara and Sigma rules support, MITRE ATT&CK matrix, AI based malware detection, Mail Monitor, Threat Hunting & Intelligence, Automated User Behavior, Dynamic VBA/JS/JAR instrumentation, Execution Graphs, Localized Internet Anonymization and many more

## PhishTool (Task 6)

`PhishTool`: phishtool.com

> Be you a security researcher investigating a new phish-kit, a SOC analyst responding to user reported phishing, a threat intelligence analyst collecting phishing IoCs or an investigator dealing with email-born fraud.

PhishTool combines threat intelligence, OSINT, email metadata and battle tested auto-analysis pathways into one powerful phishing response platform. Making you and your organisation a formidable adversary - immune to phishing campaigns that those with lesser email security capabilities fall victim to

PhishTool conveniently grabs all the pertinent information we'll need regarding the email.

* Email sender
* Email recipient
* Timestamp
* Originating IP and Reverse DNS lookup

### Look at the Strings output. What is the name of the EXE file?

        #454326_PDF.exe

## Phishing Case 1 (Task 7)

* Open the `Phish3Case1.eml` file that consists of email information.
* Open the file in app.phishtool.com
* Analyze the email information

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/a2e0ec5a-c24e-4492-b19a-d50e26d63443)

### What brand was this email tailored to impersonate?

    Netflix

### What is the From email address?

    JGQ47wazXe1xYVBrkeDg-JOg7ODDQwWdR@JOg7ODDQwWdR-yVkCaBkTNp.gogolecloud.com
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/87d3307a-3298-45d3-9fa4-a80eb29f302f)

### What is the originating IP? Defang the IP address.

    209[.]85[.]167[.]226
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/7fc26d54-a5e0-436f-8109-af3a732d67e3)

### From what you can gather, what do you think will be a domain of interest? Defang the domain.

* Return-Path defines how and where bounced emails will be processed. For this reason, the domain in the email address is the requested domain.

    etekno[.]xyz
  
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/2d4286ea-b0ce-4b00-b106-68b953170b36)

### What is the shortened URL? Defang the URL.

    hxxps[://]t[.]co/yuxfZm8KPg?amp=1
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/266e359e-892f-4cad-b387-9471b60f9740)

## Phishing Case (Task 8)

`Task` : https://app.any.run/tasks/8bfd4c58-ec0d-4371-bfeb-52a334b69f59

### What does AnyRun classify this email as?

    Suspicious Activity
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/90b98b1a-f5b0-4772-a85f-5452d9800e06)

### What is the name of the PDF file?

    payment-updateid.pdf

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/90b98b1a-f5b0-4772-a85f-5452d9800e06)

### What is the SHA 256 hash for the PDF file?

    cc6f1a04b10bcb168aeec8d870b97bd7c20fc161e8310b5bce1af8ed420e2c24

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/29e7e47b-4b19-4b3f-8ddf-8eb0f22c31d9)

### What two IP addresses are classified as malicious? Defang the IP addresses. (answer: IP_ADDR,IP_ADDR)

    2[.]16[.]107[.]83,2[.]16[.]107[.]24
    
* Click on `Text Report`
* See under `connections` tab
  
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/e133decc-3f9e-41b0-ad17-59b9bb87e518)

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/155e0f37-8cc4-46f8-9601-099c130dc6d8)

### What Windows process was flagged as Potentially Bad Traffic?

    svchost.exe

* See under `Threats` in the text report.
  
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/9983b9fb-50e8-4a8a-ba4c-8d1061293462)

## Phishing Case 3 (Task 9)

`Task` : https://app.any.run/tasks/82d8adc9-38a0-4f0e-a160-48a5e09a6e83

### What is this analysis classified as?

    Malicious Activity

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/981954e0-9568-4128-9e24-0d1b0594059d)

### What is the name of the Excel file?

    CBJ200620039539.xlsx

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/981954e0-9568-4128-9e24-0d1b0594059d)

### What is the SHA 256 hash for the file?

    5f94a66e0ce78d17afc2dd27fc17b44b3ffc13ac5f42d3ad6a5dcfb36715f3eb

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/ea3f8ed3-72d7-44fe-9cff-549704c3c604)

### What domains are listed as malicious? Defang the URLs & submit answers in alphabetical order. (answer: URL1,URL2,URL3)

    biz9holdings[.]com,findresults[.]site, ww38[.]findresults[.]site

* Open `Text Report`
* See under `connections`
  
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/387811bc-11e9-4207-b043-19635ba28534)

### What IP addresses are listed as malicious? Defang the IP addresses & submit answers from lowest to highest. (answer: IP1,IP2,IP3)

    204[.]11[.]56[.]48,103[.]224[.]182[.]251,75[.]2[.]11[.]242,

* See the IP under connections.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/387811bc-11e9-4207-b043-19635ba28534)

### What vulnerability does this malicious attachment attempt to exploit?

    CVE-2017-11882
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/c80c7fef-da34-4415-a4ec-316b44273df6)

