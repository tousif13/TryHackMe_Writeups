# Investigating with ELK 101

## Elastic Stack

Elastic stack is the collection of different open source components linked together to help users take the data from any source and in any format and perform a search, analyze and visualize the data in real-time.

Elastic Stack consists of 4 components.

* Elasticsearch
* Logstash
* Beats
* Kibana

### Elasticsearch

Elasticsearch is a full-text search and analytics engine used to store JSON-formated documents. Elasticsearch is an important component used to store, analyze, perform correlation on the data, etc. Elasticsearch supports RESTFul API to interact with the data

### Logstash

Logstash is a data processing engine used to take the data from different sources, apply the filter on it or normalize it, and then send it to the destination which could be Kibana or a listening port

A logstash consists of 3 components : 

`Input` - where the user defines the source from which the data is being ingested

`Filter` - where the user specifies the filter options to normalize the log ingested above.

`Output` - where the user wants the filtered data to send. It can be a listening port, Kibana Interface, elasticsearch database, a file, etc

### Beats 

Beats is a host-based agent known as Data-shippers that is used to ship/transfer data from the endpoints to elasticsearch. Each beat is a single-purpose agent that sends specific data to the elasticsearch. All available beats are shown below.

### Kibana

Kibana is a web-based data visualization that works with elasticsearch to analyze, investigate and visualize the data stream in real-time. It allows the users to create multiple visualizations and dashboards for better visibility—more on Kibana in the following tasks.

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/d1bd0aac-d5db-4148-8996-88cf77a940e7)

Kibana is an integral component of Elastic stack that is used to display, visualize and search logs. Some of the important tabs we will cover here are:

* Discover Tab
* Visualisation
* Dashboard

Starting the attackbox by accessing kibana using machine's IP and credentials provided in tryhackme platform.

## Discover Tab (Task 5)

### Select the index vpn_connections and filter from 31st December 2021 to 2nd Feb 2022. How many hits are returned?

      2,861 hits
      
      In top right side There will be Time Filter. In that, select left side from arrow time as `Absolute` and select it to 31st December 2021 and right to the arrow select date to 2nd Feb 2022. It will show the results between these timeline.
      
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/712db80e-4007-452a-af00-28a75f6d2830)

### Which IP address has the max number of connections?

      238.163.231.224
      
      In left side there will be `Filter by Type`. In that see "Source_ip" field will be there. If we click it, We can see which IP occured more. 
      
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/b4c392b7-0548-4e48-8d42-5a7f9df7136e)

### Which user is responsible for max traffic?

      James
      
      In "Filter by Type", In "UserName" field, if we click it, We can see which user has max traffic.
      
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/629fe6ad-9de9-4aac-bc5c-622ba8d647ce)

### Create a table with the fields IP, UserName, Source_Country and save

      In "Filter by Type", if we hover over field name we desired, we will see '+' symbol to add the field to the table. Add IP, UserName, Source_Country to the table.
      
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/d4eeba90-2cea-43c3-85c1-f9fe836c6fb1)

### Apply Filter on UserName Emanda; which SourceIP has max hits?

       107.14.1.247
       
       
