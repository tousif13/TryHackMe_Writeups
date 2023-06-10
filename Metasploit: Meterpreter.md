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

