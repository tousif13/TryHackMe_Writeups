# Metasploit: Introduction

## Main Components of Metasploit ( Task 2)

### Auxiliary

* Any supporting module, such as scanners, crawlers and fuzzers, can be found here.
* `tree -L 1 auxiliary/`

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/2b5e89f7-cfed-422c-811c-b6279aca3f5c)

### Encoders

* Encoders will allow you to encode the exploit and payload in the hope that a signature-based antivirus solution may miss them.
* Signature-based antivirus and security solutions have a database of known threats. They detect threats by comparing suspicious files to this database and raise an alert if there is a match. Thus encoders can have a limited success rate as antivirus solutions can perform additional checks.
* `tree -L 1 encoders/`

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/c93f8d06-f5fd-4882-837c-968e84c968c2)

### Evasion

* While encoders will encode the payload, they should not be considered a direct attempt to evade antivirus software. On the other hand, “evasion” modules will try that, with more or less success.
* `tree -L 2 evasion/`

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/0c637ef5-ddca-4b9c-9a0b-ab9c2d9b882c)

### Exploits

* Exploits, neatly organized by target system.
* `tree -L 1 exploits/`

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/c65ca9ca-8cd1-44f7-a2ad-df6b8502e01d)

### NOPs

* NOPs (No OPeration) do nothing, literally. They are represented in the Intel x86 CPU family they are represented with 0x90, following which the CPU will do nothing for one cycle. They are often used as a buffer to achieve consistent payload sizes.
* `tree -L 1 nops/`

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/a1f16738-08ad-4846-b998-d8024b5ddaaf)

### Payloads

* Payloads are codes that will run on the target system
* Metasploit offers the ability to send different payloads that can open shells on the target system.
* `tree -L 1 payloads/`

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/fc66e151-99c4-46a1-a1f4-3233747eec6e)

