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
       
       Select Emanda in UserName field in left side pane list. It will filter only Emanda hits and Click "Source_ip" field, it will show the which IP has max hits.
       
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/7d7e44b0-9d56-425e-8028-f4c34e78bff6)

### On 11th Jan, which IP caused the spike observed in the time chart?

      172.201.60.191
      
      In the timechart provided, click the chart of Jan 11th. It will gives Jan 11th hits and we can also see the time constraint changed automatically to Jan 11th.
      
      Click "Source_ip" field, we can see which IP caused the spike.
      
### How many connections were observed from IP 238.163.231.224, excluding the New York state?

      48 hits
      
      From "Source_ip" field, Click + on 238.163.231.224 to add the filter that it selects particular IP hits only.
      
      From "source_state", Click - on New York to select filter that excludes New York.
      
      Both filters are applied together and we can see 48 hits.
      
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/f3f548e5-3448-4403-af12-82f9a5140892)

## KQL Overview (Task 6)

KQL (Kibana Query Language) is a search query language used to search the ingested logs/documents in the elasticsearch. Apart from the KQL language, Kibana also supports Lucene Query Language. 

### Create a search query to filter out the logs from Source_Country as the United States and show logs from User James or Albert. How many records were returned?

      161 Hits returned
      
      In search bar, Give Source_Country:"United States" (It will give autofill options readily for you)
      
      Give "and" keyword and give UserName:"James"
      
      Give "or" keyword and give UserName:"Albert"
      
 The total search query looks like :
 
      Source_Country : "United States" and UserName : "James" or UserName : "Albert"
      
 ![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/5cc1ec73-5b57-4cd4-9010-c4833cbf7ed6)

### As User Johny Brown was terminated on 1st January 2022, create a search query to determine how many times a VPN connection was observed after his termination.

      1 Hit
      
      In Time Filter, Give 'from' time as 1st January 2022 on absolute and give 'to' time as Now
      
      In search filter, Give Username:"Johny Brown"
      
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/37fd0bb4-1cee-4b7c-aa47-3e4575e2c0f7)

## Creating Visualizations (Task 7)

The visualization tab allows us to visualize the data in different forms like Table, Pie charts, Bar charts, etc. This visualization task will use multiple options this tab provides to create some simple presentable visualizations.

### Which user was observed with the greatest number of failed attempts?

      Simon
      
      In menu, Go to Visualize Library
      
      Click create visualization and select lens
      
      Select 'Add filter'

![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/aa4034fb-c756-4759-9210-82c82a6b45cd)

      Select Field you want to apply constraints on ('action' in this case)
      
      Select Operator type like is, isnot, exists etc. ('is' in this case)
      
      Select Value according to your requirements. ('failed' in this case)
      
      Click Save
      
      Drop down the record in visualization work window.
      
      Drop down the UserName field in visualization.
      
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/d30fc5a5-4d37-4051-b56a-dbf88eb7d0c8)

### How many wrong VPN connection attempts were observed in January?

      274 attempts.
      
      Keep same procedure of previous visualization.
      
      Change the time filter from 1st January to 31st January
      
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/3586ed6c-97f5-40d9-a298-bc3bb8275151)

## Creating Dashboard (Task 8)

      Go to Menu and select Dashboard.
      
      CLick create new dashboard.
      
      Select your saved visualizations or create a new one.
      
![image](https://github.com/tousif13/TryHackMe_Writeups/assets/33444140/9b2d437a-00e3-4e5d-9567-45ca391fbb71)

We briefly explored ELK components and then focused more on the Kibana interface and its features. While exploring Kibana Interface, we learned:

* How to create a search query to search for the logs
* Apply filters to narrow down the results.
* Create Visualizations and dashboards.
* How to investigate VPN logs.
