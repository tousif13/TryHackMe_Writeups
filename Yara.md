# Yara

## Introduction to Yara rules (Task 4)

`yara myrule.yar somefile`

where 

`yara` - Command

`myrule.yar` - File that contains yara rule

`somefile` - Name of file, directory, or process ID to use the rule for.

## Using LOKI and its YARA rule set (Task 8)

### Scan file 1. Does Loki detect this file as suspicious/malicious or benign?

    Suspicious

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/6899ac8d-6b64-4582-a5b7-32554bcba8b8)

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/8d4b9f48-a7a0-4486-a78f-4477caa93c7e)

### What Yara rule did it match on?

    webshell_metaslsoft
    


### What does Loki classify this file as?

    Web Shell
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/23244ca9-88c5-4f8e-9c74-70b043c00835)

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/670ce0b3-bd0d-40fd-a246-7b66517ced2e)

### Based on the output, what string within the Yara rule did it match on?

    Str1
    
### What is the name and version of this hack tool?

    b374k 2.2

### Inspect the actual Yara file that flagged file 1. Within this rule, how many strings are there to flag this file?

    1

### Scan file 2. Does Loki detect this file as suspicious/malicious or benign?

    benign

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/dd45f45b-3b69-45d0-ad53-dc1a617172f8)

### Inspect file 2. What is the name and version of this web shell?

    b374k 3.2.3

![file2ver2](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/a0651e8b-3e31-4748-a365-0a901cc35f33)

![file2ver](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/62737f80-7f72-467a-9441-848efe6543be)

## Creating Yara rules with yarGen (Task 9)

To run yarGen :

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/65e9be28-f7e2-4320-bd83-c53a0a571ce0)

![yargen](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/da12f7a4-553f-4121-82aa-960e11f2218d)

### From within the root of the suspicious files directory, what command would you run to test Yara and your Yara rule against file 2?

    yara files2.yar file2/1ndex.php

### Did Yara rule flag file 2?

    Yay

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/640b66b1-2f56-4d01-90d9-5d1b767db296)

### Copy the Yara rule you created into the Loki signatures directory

    cp file2.yar ~/tools/Loki/signature-base/yara

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/2f33b2de-3bbb-487e-956f-4b373adf7ff9)

### Test the Yara rule with Loki, does it flag file 2? (Yay/Nay)

    Yay
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/4e1290a6-3dcb-4a33-ae81-64f3af4ea2f9)

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/1c1c1f88-b7ea-45e3-8204-cac18078d35d)

### What is the name of the variable for the string that it matched on?

    Zepto

### Inspect the Yara rule, how many strings were generated?

    20

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/bb6b215a-1ac8-491b-9882-4b1a09185be0)

### One of the conditions to match on the Yara rule specifies file size. The file has to be less than what amount?

    700kb

