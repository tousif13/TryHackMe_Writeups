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

