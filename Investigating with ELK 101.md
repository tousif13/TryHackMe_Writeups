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

## Discover Tab

