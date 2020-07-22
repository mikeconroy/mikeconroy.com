---
title: Mule & ELK Part 1 - An Introduction to the ELK Stack with Mule
author: Mike Conroy
layout: post
permalink: /2020/06/an-introduction-to-elk-stack-with-mule/
comments: true
categories:
  - Computing
  - Technology
  - ELK
  - MuleSoft
---

<div markdown="1" style="text-align: center;">
  [![MuleSoft Logo](/assets/images/MuleSoft/logo.png)](https://www.mulesoft.com/)
  [![ELK Logo](/assets/images/elk/logo.png)](https://www.elastic.co/what-is/elk-stack)
</div>

API & Integration platforms are often responsible for transferring business critical data between systems. Failures could have big impacts to a business such as users not being able to login, financial transactions not being processed or customers being unable to make purchases. It is therefore vital that sufficient monitoring tools are in place that enable operations teams to identify trends to prevent failures in advance and also respond quickly when errors do occur.

This post will be a part of a series of posts looking at MuleSoft and the ELK Stack for enabling log aggregation and monitoring. This post specifically will give an overview of the ELK Stack and it's components and future posts will go into configuration details and how to send logs to the ELK Stack.

# What is the ELK Stack?

The ELK stack is offered by [Elastic](https://www.elastic.co/) and is named after 3 open source components for ingesting, parsing, storing and visualising logs:
* [Elasticsearch](https://www.elastic.co/elasticsearch/) - This is the storage part of the stack responsible for storing and searching the logs. It operates in clusters so can be scaled horizontally with ease. Users interact with it over an API and it provides "lightning fast" search capabilities.
* [Kibana](https://www.elastic.co/kibana/) - To navigate and visualise the log data stored in Elasticsearch which includes searching logs and creating charts, metrics and dashboards.
* [Logstash](https://www.elastic.co/logstash/) - This is the tool that takes in logs, parses them and sends them into Elasticsearch. Just like an integration tool, it receives [input](https://www.elastic.co/guide/en/logstash/current/input-plugins.html), performs [transformations/filters](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html), and then sends the [output](https://www.elastic.co/guide/en/logstash/current/output-plugins.html) to another system.

The ELK ecosystem has grown significantly and now offers many tools beyond these initial 3 but with Elasticsearch and Kibana remaining at the core of the stack. In a future post we will take a look at another offering - [Filebeat](https://www.elastic.co/beats/filebeat).

# Why send logs to ELK?

In the event of an error the operations team will need to track down where an error occurred - Is the target or source system down? Are there validation errors? Are there authentication errors? Is the API receiving malicious requests? and so on.

On top of these reactive queries the team and the business would also need to get analytics out of the platform to view trends, metrics and performance of the interfaces deployed - Since last deployment has usage increased? Since last deployment do requests take longer to process? What are our peak number of transactions? What percentage do the number of requests increase by each year? When do errors occur the most? How many records were processed today compared to the previous day? And a variety of questions based on business usage of the API Platform.

MuleSoft provides [monitoring](https://docs.mulesoft.com/monitoring/) tools and searching of the logs which can help with some of the team's queries (especially around performance) but log aggregation tools can provide even more support especially around analytics and searching logs across multiple APIs & Integration (i.e. aggregation, like the name suggests). Tools like Kibana can provide deeper analytics, metrics and customised dashboards using data from a range of sources.

In summary, the benefits of sending the logs to a log aggregation tool are as follows:

* Make operations lives easier and reduce mean time to resolve incidents.
* Identify trends in API usage for business purposes and technical/performance reasons.
* Control over storage and how long logs are kept for - which may be a regulation or auditing requirement in some cases.
* Security - Identify trends and malicious requests - e.g. authentication failures, DOS attempts from a set of IPs.

# How to send Mule Logs to ELK?
There are a couple of options for sending Mule logs to the ELK stack and the decision on which method will likely come down to infrastructure setup.
* [Log4j2](https://logging.apache.org/log4j/2.x/) - The configuration of the Mule applications can be updated to send logs to Logstash via a socket. [Part 2]({% link _drafts/2020-07-16-sending-mule-logs-to-elk-with-log4j2.md %}) of this series will walkthrough the configuration required for this method.
  * **Pros:** Works on both CloudHub & customer hosted (on-premise) runtimes as it's the apps responsibility to ship the logs.
  * **Cons:** Not officially supported by MuleSoft and requires editing of the Log4j2.xml file in *all* Mule apps that need to send the logs.

* [Filebeat](https://www.elastic.co/beats/filebeat) - This option consists of running the Filebeat agent on the Mule Runtime servers where it will monitor log files and send updates through to Logstash. Part 3 of this series will walkthrough the configuration required for this method.
  * **Pros:** Doesn't require editing of all the Mule apps (infrastructure or DevOps team can take responsibility for shipping logs). If Filebeat fails to send some logs the log files will still be available on the server's disk. 
  * **Cons:** Can only be used on customer hosted runtimes and *not* CloudHub (due to not being able to install the agent on the server).

* [CloudHub REST API](https://docs.mulesoft.com/runtime-manager/cloudhub-api) - This option requires a custom application to be buit that will call the CloudHub REST API to retrieve logs and then forward them onto ELK.
  * **Pros:** Doesn't require disabling of CloudHub logs & easier to handle errors than Log4j2 configuration (if app detects a failure it can try to call the API again/raise an alert etc.).
  * **Cons:** Custom development and additional application to maintain that is calling the CloudHub API. Only possible with CloudHub. Logs not sent through in real-time.

In general, Log4j2 is the approach taken when CloudHub is used and Filebeat when on premise. These two options require the least customisation & development.

This post and series are on-going and will be continuously updated. I would love to hear your thoughts & comments below!