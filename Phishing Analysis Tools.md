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

