# MAL: REMnux - The Redux

Deploy the machine to perform the following tasks.

## Analysing Malicious PDF's (Task 3)

### Analyzing PDF's

PDF's are capable of containing many more types of code that can be executed without the user's
knowledge. This includes:
* Javascript
* Python
* Executables
* Powershell Shellcode

We'll be using `peepdf` to begin a precursory analysis of a PDF file to determine the presence of Javascript. If there is, we will extract this Javascript code (without executing it) for our inspection

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/b34a7793-0e1c-4564-af4b-3fc977b072d7)

### How many types of categories of "Suspicious elements" are there in "notsuspicious.pdf"

    3
 
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/4eb97564-be79-4ad2-b9fc-6c05d6c475dd)

### Extract the javascript .

First step is to create a script for peepdf.

The following command will create a script for peepdf.

    echo 'extract js > javascript-from-demo_notsuspicious.pdf' > extracted_javascript.txt

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/b6fbb772-b4ee-438b-a6ef-4fda52219ea9)

Second step , we can extract the javascript using peepdf using command

    peepdf -s extracted_javascript.txt demo_notsuspicious.pdf

### Use peepdf to extract the javascript from "notsuspicious.pdf". What is the flag?

    THM{Luckily_This_Isn't_Harmful}
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/211cbc5c-ddbe-40df-a71e-67b03ea05afc)

### How many types of categories of "Suspicious elements" are there in "advert.pdf"

    6

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/49a879f0-9f25-496e-988d-d3fc6604ebdf)

### Now use peepdf to extract the javascript from "advert.pdf". What is the value of "cName"?

    notsuspicious
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/7df3de67-59de-423e-a148-1ea3bbd3fd16)

## Analysing Malicious Microsoft Office Macros (Task 4)

Malware infection via malicious macros (or scripts within Microsoft Office products such as Word and Excel) are some of the most successful attacks to date.

Example of APT - Emotet, QuickBot

To check if a MS Office document contains macros we can use the `vmonkey` utility.

`vmonkey <filename>.doc` command is used.

### What is the name of the Macro for "DefinitelyALegitInvoice.doc"

    DefoLegit
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/586f9e44-35bc-47a0-a4cd-ba7a5767ce19)

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/27d0b1fa-dd5c-4487-a069-e72d1781b42a)

### What is the URL the Macro in "Taxes2020.doc" would try to launch?

    http://tryhackme.com/notac2server.sh
    
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/8225bad5-395a-4eba-a236-3191b17772f4)

## I Hope You Packed Your Bags (Task 5)

At it's very simplest, file entropy is a rating that scores how random the data within a PE file is. With a scale of 0 to 8. 0 meaning the less "randomness" of the data in the file, where a scoring towards 8 indicates this data is more "random".

For example, files that are encrypted will have a very high entropy score. Where files that have large chunks of the same data such as "1's" will have a low entropy score.

### Low Entropy

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/21a5d848-d939-4492-9499-761d9bd70066)

### High Entropy

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/57d4dd31-5145-43c3-94d2-7376d35c5a8b)

### Malware analysts unpacking a file 

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/9662fdcb-c51a-4945-9e58-e7c308676503)

### What is the highest file entropy a file can have?

    8

### What is the lowest file entropy a file can have?

    0

### Name a common packer that can be used for applications?

    UPX

## How's Your Memory? (Task 6)

### Volatility

Volatility is unable to assume what the operating system that we have created a memory dump is.

Whilst Volatility can't assume, it can guess. Here's where profiles come into play.

In other scenarios, we would use the `imageinfo` plugin to help determine what profile is most suitable with the syntax of `volatility -f Win7-Jigsaw.raw imageinfo`

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/da0b6ded-e119-469c-aa90-8995a02ffd7a)

Profile `Win7SP1x64` is the first suggested and just happens to be the correct OS version.

We can list the processes that were running via `pslist` :

`volatility -f Win7-Jigsaw.raw --profile=Win7SP1x64 pslist` command is used.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/49843670-fdbe-4088-9378-eec2d185c977)

