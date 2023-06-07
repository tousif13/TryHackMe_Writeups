# ItsyBitsy

In this challenge room, we will take a simple challenge to investigate an alert by IDS regarding a potential C2 communication.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/9a1c2a00-0e42-4516-ae5e-7c6c5267996c)

## Scenario - Investigate a potential C2 communication alert ( Task 2)

During normal SOC monitoring, Analyst John observed an alert on an IDS solution indicating a potential C2 communication from a user Browne from the HR department. A suspicious file was accessed containing a malicious pattern THM:{ ________ }. A week-long HTTP connection logs have been pulled to investigate. Due to limited resources, only the connection logs could be pulled out and are ingested into the connection_logs index in Kibana

### How many events were returned for the month of March 2022?

    1,482 hits
    
    In time filter, Give 'from' time as 1st March 2022 and 'to' time as 31st March 2022
    
    Update the search, we will get the events of the month of March 2022.
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/01cd376b-da5f-4755-98cc-899df74cc083)

### What is the IP associated with the suspected user in the logs?

    192.166.65.54
    
    Click "Source_ip" from field types.
    
    We can see one IP is of 99.6% and other is 0.4%
    
    Thus, 0.4% IP is the suspected user as his hits are too minimal.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/c5dfdbc2-ae34-46d2-b587-8a1ac0628522)

### The user’s machine used a legit windows binary to download a file from the C2 server. What is the name of the binary?

    bitsadmin
    
    Select the suspected user IP to filter the events.
    
    In field types, click "user_agent", we can see the "bitsadmin" tool.
    
    Bitsadmin is a command-line tool used to create, download or upload jobs, and to monitor their progress.
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/8450e2a3-02a7-460a-af44-e3169ff7455c)

### The infected machine connected with a famous filesharing site in this period, which also acts as a C2 server used by the malware authors to communicate. What is the name of the filesharing site?

    pastebin.com
    
    As we are looking for filesharing site which acts as a c2 server used by malware authors to communicate. We will look for 'hosts'
    
    Click 'host' in the Filter by type and we can see only one host which is 'pastebin.com'
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/1c8c6500-95d9-4e3a-9636-0a871b8517e8)

### What is the full URL of the C2 to which the infected host is connected?

    /yTg0Ah6a
    
    We need to find out full URL of C2. As we already knows the domain name (pastebin.com), we need to find the URI.
    
    Add the pastebin.com by clicking + symbol to filter its events.
    
    Click 'uri' in the Filter by type and we can see an uri : '/yTg0Ah6a'
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/6e13d292-64e7-4bc1-ab2b-1fada9920f5f)

### A file was accessed on the filesharing site. What is the name of the file accessed?

    secret.txt
    
    As we know the full URL, open browser and give the 'pastebin.com/yTg0Ah6a' URL
    
    It shows the secret.txt file.
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/277f2196-90be-4066-b23c-8b8b3c0c44a9)

### The file contains a secret code with the format THM{_____}.

    THM{SECRET__CODE}

    The file contains a code that shows us directly.
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/81340820-19f5-4be1-b99c-c1156d7771cb)

