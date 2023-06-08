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

* You will see four different directories under payloads: adapters, singles, stagers and stages
* `Adapters` : An adapter wraps single payloads to convert them into different formats. For example, a normal single payload can be wrapped inside a Powershell adapter, which will make a single powershell command that will execute the payload.
* `Singles` : Self-contained payloads (add user, launch notepad.exe, etc.) that do not need to download an additional component to run.
* `Stagers` : Responsible for setting up a connection channel between Metasploit and the target system. Useful when working with staged payloads. “Staged payloads” will first upload a stager on the target system then download the rest of the payload (stage). This provides some advantages as the initial size of the payload will be relatively small compared to the full payload sent at once.
* `Stages` : Downloaded by the stager. This will allow you to use larger sized payloads.

### Post

* Post modules will be useful on the final stage of the penetration testing process listed above, post-exploitation.
* `tree -L 1 post/`

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/ff255d5b-a19e-469d-97ee-7e739d96c3ec)

### What is the name of the code taking advantage of a flaw on the target system?

      Exploit
      
### What is the name of the code that runs on the target system to achieve the attacker's goal?

      Payload
      
### What are self-contained payloads called?

      Singles
      
### Is "windows/x64/pingback_reverse_tcp" among singles or staged payload?

      Singles
      
## Msfconsole (Task 3)

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/5b596db3-348d-4ccf-8635-6231a527d55c)

* `Use` command is used to select a module
* `use exploit/windows/smb/ms17_010_eternalblue` selects the `eternalblue` module

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/9b48fed9-ddc8-47ff-bd4f-6785b347a338)

* `show` command can be used in any context followed by a module type (auxiliary, payload, exploit, etc.) to list available modules.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/c859b019-30e2-422e-bc41-f3529b5175e8)

* `info` is not a help menu; it will display detailed information on the module such as its author, relevant sources, etc

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/8a851949-dea2-44e6-947a-190690b9854a)

* `search` command will search the Metasploit Framework database for modules relevant to the given search parameter. You can conduct searches using CVE numbers, exploit names (eternalblue, heartbleed, etc.), or target system.

* `search type: value` is used to search according to type.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/d02f58a6-e688-421f-9ab8-bfe3f4f43b1c)

### How would you search for a module related to Apache?

      search apache
      
### Who provided the auxiliary/scanner/ssh/ssh_login module?

      todb
      
`info auxiliary/scanner/ssh/ssh_login module`
      
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/05a0ccc1-a6ee-4a08-a918-fb07268250bf)
