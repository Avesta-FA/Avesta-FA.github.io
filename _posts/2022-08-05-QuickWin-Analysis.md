---
title: "QuickWin Analysis"
date: 2022-08-05
author: Avesta Fahimipour
categories:
  - Blog
---


# QuickWin-CheatSheet
The purpose of this repository is to be a cheat sheet for the security community to find and detect adversaries.  
While there will be a lot of quick wins I will also add detection techniques that require more analysis.  

## High Level

### Long Tail Analysis
Long tail analysis is a multi purpose detection technique that works on historical data. The output contains two important sections:  
* Least frequently used (LFU)  
* Most frequently used (MFU)  

Depending on the data that is being analyzed both sections can be interesting.  
This technique was originally founded by Eric Conrad, SANS Instructor.  
https://www.youtube.com/watch?v=KgVmNicfHxo

#### How To  

`Data | Group-Object id -NoElement | sort count`

`Data | sort | uniq -c | sort -n`

### Stacking
Generally, endpoints tend to be very similar especially if you have a baseline configuration.  
When you gather data from your endpoints  (e.g Registry) you can perform what is called stacking.  
When you stack the specified data from all the endpoints you will end up with entries that only exist on a small number of endpoints. Those entries are the ones you want to analyze.  

#### How To  

A great tool that utilizes this technique is called [Kansa](https://github.com/davehull/Kansa/) by dave hull.  




### Fuzzy Searching 
A fuzzy search is a technique that uses search algorithms to find strings that match patterns approximately.  
This technique is especially useful when looking for phishing domains targeting your organization.  

#### How To  
[dnstwist](https://github.com/elceef/dnstwist) can help you generate this type of information.  
Different SIEMs also have fuzzy matching that allows you to detect phishing domains in real-time.  



### Frequency Analysis
One of the ways adversaries try to evade prevention and detection is by using random values, this can be used for network and endpoint data, but how would we detect these?  
I present [freq](https://github.com/MarkBaggett/freq) made by MarkBagget, SANS instructor.  
This tool calculates the randomness of data, a low number means that the data is random.  



### Comparative Analysis
You can always compare network and endpoint data that are similar together to detect anomalies.  
On a day to day basis similar systems should always behave similarly.  



### Netflow Analysis
Some might think that netflow is just network metadata and can't be used to detect malicious activity.  
Here are some ways you can use netflow to detect adversaries:  
* Upload to download ratio  
  - During normal operations most of the time it's anomalous to have more uploads compared to downloads.  
* Number of connections
  - This one should be compared by other similar systems simply because you don't know how many connections those systems make on a daily basis
* Long duration time
  - Any connection that has been up for several hours should be investigated 



## Low Level

### DNS Null Record
While all DNS record types can be used for malicious behavior the Null type is almost always an indicator of anomalous behavior and should be alerted on.  


### WMI
Windows Management Instrumentation gives adversaries two options to use it:
* WMIC
  - This options allows adversaries to run WMI on the command line
* WMI Event Consumer & Filter Binding 
  - An Event Consumer allows an adversary to run their script or process of choosing, these consumers are binded to filters that allow them to run

#### How To
There are various ways to detect WMI activity:
* Event Logs 5857-5861
* Autoruns
* Get-WmiObject
* Get-CimInstance


