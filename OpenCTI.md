# OpenCTI

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/2ac9adf2-0a4d-4118-89f1-f1441ae3348d)

OpenCTI is another open-sourced platform designed to provide organisations with the means to manage CTI through the storage, analysis, visualisation and presentation of threat campaigns, malware and IOCs.

> Developed by the collaboration of the French National cybersecurity agency (ANSSI), the platform's main objective is to create a comprehensive tool that allows users to capitalise on technical and non-technical information while developing relationships between each piece of information and its primary source. The platform can use the MITRE ATT&CK framework to structure the data. Additionally, it can be integrated with other threat intel tools such as MISP and TheHive. Rooms to these tools have been linked in the overview.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/a113f88f-8ddf-401b-9cb8-dcc5bbf40f22)

## Investigative Scenario (Task 6)

As a SOC analyst, you have been tasked with investigations on malware and APT groups rampaging through the world. Your assignment is to look into the CaddyWiper malware and APT37 group. Gather information from OpenCTI to answer the following questions.

### What is the earliest date recorded related to CaddyWiper?

* Under `Knowledge` tab, In `Arsenal`, Search for `CaddyWiper`.
* CLick the `CaddyWiper` module.
* In Overview tab, under `Latest reports about this entity` frame, we can see the records related to the CaddyWiper.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/720f818e-2c41-4280-a7f7-694578958a19)

* First or earliest date recorded is `2022/03/15`

### Which Attack technique is used by the malware for execution?

* Go to `knowledge` tab.
* Go to `Attack Patterns`.
* Under `Execution` as stated in the task, Look for the red marked field.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/cfdf8dc3-a87d-4fa5-9467-dbfb81fd88b8)

* We get to know that it is `Native API`.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/d4bfb582-844c-4e97-b389-5f664f42e4f3)

### How many malware relations are linked to this Attack technique?

* Select the `Native API` attack technique
* Go to `knowledge` tab.
* Under `Distribution of Relations`, we can see the malware relations.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/efdc8eaa-a3b1-43aa-8490-68fc3c8df9e0)

### Which 3 tools were used by the Attack Technique in 2016?

* In that attack technique's knowledge tab, Select `Tools` at the right pane window.
* It will list all the tools used by the attack technique.
* Look for `2016` dated tools.
* We get `ShmiRatReporter`, `Empire`, `BloodHound`.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/5a7da08e-a6fe-4165-9d51-9cf2ee859f3f)

### What country is APT37 associated with?

* Go to `Threats` tab.
* Click on `Intrusion Sets` tab which consists of TTPs, tools, malware and infrastructure used by a threat actor against targets who share some attributes.
* Search for `APT37` intrusion set and click on it.
* In the Overview, we can see that it is originated from `North Korea`.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/7a04c983-6f7e-4ba1-9bba-782ef7cf41e0)


### Which Attack techniques are used by the group for initial access?

* Go to `Knowledge` tab.
* Scroll down, we will find two tabs, `TIMELINE` and `GLOBAL KILL CHAIN`.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/45f4fabb-d74b-4a19-bbab-a8af76fdda2c)

* Click Global kill chain, scroll down looking for `initial access`.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/6a7601d1-bc1d-4190-ae28-932f01c459de)

There we found out the attack techniques used by the group for initial access. (`T1189` & `T1566`)

