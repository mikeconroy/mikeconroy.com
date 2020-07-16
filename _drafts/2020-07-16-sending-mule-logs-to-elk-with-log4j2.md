---
title: Mule & ELK Part 2 - Sending Mule Logs to ELK with Log4j2 (CloudHub & On-Premise)
author: Mike Conroy
layout: post
permalink: /2020/07/sending-mule-logs-to-elk-with-log4j2/
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
