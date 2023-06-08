# kiba

If we try to access kibana through browser by IP address, we won't get direct access. It will display this page :

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/0fa7feb7-4810-44fd-aa97-1530bbab484f)

So through http port we can't get access of kibana. Thus, we will look for open ports of provided IP.

Initiate nmap scan to the provided IP.

`sudo nmap -p- 10.10.174.118`

