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

API & Integration platforms are often responsible for transferring business critical data between systems and networks. Failures could have big impacts to a business such as users not being able to login, financial transactions not being processed or customers being unable to view account information. It is therefore vital that sufficient monitoring tools are in place that enable operation teams to respond quickly when errors occur as well as identify trends to perform preventive maintenance to reduce failures.

In the event of an error the support team will need to track down where an error occurred - Is the target or source system down? Are there validation errors? Are there authentication errors? Is the API receiving malicious requests? and so on.

On top of these reactive type of queries the team and the business would also need to get analytics out of the platform to view trends, metrics and performance of the interfaces deployed - Since last deployment has usage increased? Since last deployment do requests take longer to process? What are our peak number of transactions? What percentage do the number of requests increase by each year? When do errors occur the most? How many records were processed today compared to the previous day? And a variety of questions based on business usage of the API Platform.

MuleSoft provides monitoring tools and searching of the logs which can help with some of the team's queries (especially around performance) but log aggregation tools can provide even more support especially around analytics and searching logs across multiple APIs & Integration (i.e. aggregation, like the name suggests).

This post will be a part of a series of posts looking at MuleSoft and the ELK Stack for enabling log aggregation and monitoring. This post specifically will give an overview of the ELK Stack and it's components and then discuss how to send MuleSoft logs to ELK via Log4j2.

# What is the ELK Stack?

The ELK stack is offered by [Elastic](https://www.elastic.co/) and is named after 3 open source components for ingesting, parsing, storing and visualising logs:
* [Elasticsearch](https://www.elastic.co/elasticsearch/) - This is the storage part of the stack responsible for storing and searching the logs. It operates in clusters so can be scaled horizontally with ease. Users interact with it over an API and it provides "lightning fast" search capabilities.
* [Kibana](https://www.elastic.co/kibana/) - To navigate and visualise the log data stored in Elasticsearch which includes searching logs and creating charts, metrics and dashboards.
* [Logstash](https://www.elastic.co/logstash/) - This is the tool that takes in logs, parses them and sends them into Elasticsearch. Just like an integration tool, it receives [input](https://www.elastic.co/guide/en/logstash/current/input-plugins.html), performs [transformations/filters](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html), and then sends the [output](https://www.elastic.co/guide/en/logstash/current/output-plugins.html) to another system.

The ELK ecosystem has grown significantly and now offers many tools beyond these initial 3 but with Elasticsearch and Kibana remaining at the core of the stack. In a future post we will take a look at another offering - [Beats](https://www.elastic.co/beats/).

# Why send logs to ELK?

* Make operations lives easier.
* Reduce mean time to resolve.
* Identify trends in API usage.
* Control over storage and how long logs are kept for - meet auditing requirements.
* Security - Identify trends and malicious attempts - e.g. validation failures.

# Options for sending logs to ELK from a Mule Runtime

# How to send Mule Logs to ELK with Log4j2?

There are a few options for sending logs from Mule applications to the ELK stack and the runtime model used can dictate available options. For example, if your Mule applications run in on-premise or "customer hosted" Mule runtimes File Beat could be used instead to monitor the 'actual' log files that Mule writes and send them to Logstash. Since FileBeat is an executable in it's own right it is not possible to install this on a CloudHub worker so this isn't an option.

This post focuses on configuring Log4j2 to send the logs to the ELK stack which will work in CloudHub and Customer-Hosted runtimes.

#### Log4j2 Configuration

The complete Log4j2 configuration can be found [here](/assets/elk/log4j2.xml).
The Appender
{% highlight xml %}
<Socket name="socket" host="localhost" port="4560" protocol="TCP">
    <JsonLayout compact="true" eventEol="true" />
    <!-- <PatternLayout pattern="{&quot;log_timestamp&quot;:&quot;%d&quot; ,&quot;log_thread&quot;:&quot;[%t]&quot; , &quot;log_level&quot;:&quot;%-5p&quot; , %m}%n" /> -->
</Socket>
{% endhighlight %}

And the Appender Ref
{% highlight xml %}
<AsyncRoot level="INFO">
    <AppenderRef ref="file" />
    <AppenderRef ref="socket" />
</AsyncRoot>
{% endhighlight %}

#### Logstash Configuration

The complete Logstash configuration can be found [here](/assets/elk/logstash-mule.conf).
Logstash uses Socket for the input as you can see from the log4j2 configuration.
  Listens to TCP on port xxx.
  Uses a filter to identify the date
  then sends the logs onto the elastic search cluster and index as defined.


#### Elasticsearch & Kibana

Very little configuration required...


Future posts will look further into parsing the log messages and visualising them as well as how File Beats could be used instead.


Turn into a series of posts? https://engineering.chrobinson.com/how-to/linking-a-series-of-jekyll-posts/
  Add that this is an ongoing series of posts touching different parts of the topic and the post will continuously be update - feedback is welcome.
  Part 1 - Introduction to ELK & MuleSoft - Why it's used?
  Part 2 - Sending Logs to ELK with Log4j2
    Confirm this works from CloudHub (may be difficult without Logstash being publicly accessible) and disabling CloudHub Logs?? CloudHub appender?
    Log Levels - Do debug logs go through? Errors?
  Part 3 - Sending Logs to ELK with Beats
  Part 4 - Parsing the logs to load cleanly into Elasticsearch
    Index configuration on Elastic Search (should multiple apps go across multiple indexes or a single one).
    Review log4j2 layout - is json layout correct? JSON Parse Error?
    Parsing the elements of the message.
    Correlation ID? Metrics?
  Part 5 - Creating useful dashboards in Kibana to visualise your API.

Add a note that Operations can refer to the team responsible for the API which could/will include developers in a DevOps environment.

Other blog posts
  Configuration of Kibana
    Dashboards that could be created??

  logstash -f config/logstash-mule.conf
  ./kibana
  ./mule start
  ./elasticsearch start
