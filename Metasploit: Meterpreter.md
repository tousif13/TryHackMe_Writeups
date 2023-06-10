# Metasploit: Meterpreter

> Meterpreter is a Metasploit payload that supports the penetration testing process with many valuable components. Meterpreter will run on the target system and act as an agent within a command and control architecture. Meterpreter runs on the target system but is not installed on it. It runs in memory and does not write itself to the disk on the target. This feature aims to avoid being detected during antivirus scans.

> Meterpreter also aims to avoid being detected by network-based IPS (Intrusion Prevention System) and IDS (Intrusion Detection System) solutions by using encrypted communication with the server where Metasploit runs (typically your attacking machine). If the target organization does not decrypt and inspect encrypted traffic (e.g. HTTPS) coming to and going out of the local network, IPS and IDS solutions will not be able to detect its activities.

`Meterpreter will establish an encrypted (TLS) communication channel with the attacker's system.`

There are so many meterpreter payloads to use. We can decide which version of Meterpreter to use based on three factors:

* The target operating system (Is the target operating system Linux or Windows? Is it a Mac device? Is it an Android phone? etc.)
* Components available on the target system (Is Python installed? Is this a PHP website? etc.)
* Network connection types you can have with the target system (Do they allow raw TCP connections? Can you only have an HTTPS reverse connection? Are IPv6 addresses not as closely monitored as IPv4 addresses? etc.) 
