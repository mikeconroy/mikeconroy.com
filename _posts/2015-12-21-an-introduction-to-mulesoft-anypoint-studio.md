---
id: 227
title: An Introduction to MuleSoft Anypoint Studio
date: 2015-12-21T12:12:15+00:00
author: Mike Conroy
layout: post
guid: https://mikepconroy.com/?p=227
permalink: /2015/12/an-introduction-to-mulesoft-anypoint-studio/
categories:
  - Computing
  - Technology
---
<p style="text-align: center;">
  <strong>What is Anypoint Studio?</strong>
</p>

* * *

Anypoint studio is a tool for building integrations & APIs for systems. It is based on <a href="https://eclipse.org/home/index.php" target="_blank">eclipse</a> (the popular open source Java IDE) so provides a familiar environment for many. It is a graphical tool which has a low learning curve and makes it easy to build integrations. Connectors, as the name suggests, are the part in a &#8220;flow&#8221; which actually connects to a system and extract or import data. There are many built-in connectors such as Salesforce, databases, ftp and even Facebook & Twitter. It is also possible to download more that have been built by the community from the <a href="https://www.mulesoft.com/exchange?_bm=b&_bt=39007376812&utm_campaign=G_Brands_EMEA_Search_Shohil_Mule_Connectors&utm_medium=cpc&utm_source=google&utm_term=%252Bmulesoft%2520%252Bconnectors#!/?types=connector&sortBy=name" target="_blank">Anypoint Exchange</a> or develop your own if what you need isn&#8217;t available. The following guide shows just how quick and easy it is to create a MuleSoft application which grabs data from a system and transforms it before sending it to a different system.

<p style="text-align: center;">
  <strong>Creating a basic app &#8211; Salesforce to HTTP</strong>
</p>

* * *
&nbsp;
{% include image.html url="/assets/images/MuleSoft/screenshot.png" description="MuleSoft Anypoint Studio - Salesforce Flow" %}

The flow that we will create will return data from Salesforce (Accounts in our example) to the browser in JSON when visiting http://localhost:8081/salesforce.demo

  1. Create a new Mule project (File -> New -> Mule Project).
  2. In the right panel search for &#8220;HTTP&#8221; and drag the result across into the main area, do the same for &#8220;Salesforce&#8221;, a &#8220;DataMapper&#8221; and a &#8220;Logger&#8221; so it looks like the image above. We now have the basic outline of our flow so it&#8217;s time for some configuration.
  3. First click on the HTTP connector that we have put in the flow and click the plus next to connector configuration in the panel at the bottom. Enter &#8220;salesforcedemo&#8221; in the base path field and click ok. Note &#8211; If you are running something else on port 8081 then you will need to  change that setting to a different port.
  4. Create a (free) developer Salesforce account, add some Account records and then do the same as above with the Salesforce connector, choose basic authentication, enter your account credentials (you will need to request a security token in Salesforce and enter that) and test connection. Assuming it succeeded, hit okay twice and back in the bottom panel next to operation choose &#8220;Query&#8221; from the drop-down box and enter the following: SELECT Name,Phone,Type FROM Account.
  5. Next we need to look at the DataMapper which takes data in one format and converts it into a different format as it says on the tin. In our case we want to transform the Salesforce data we have received into a JSON format and output that to the browser. In the configuration for this component we have 2 parts &#8211; Input & Output. The input side should automatically detect the Salesforce object we are grabbing but we will need to configure the output. Next to Type choose JSON, select From Input -> Copy Structure. Then click Create Mapping.
  6. In the logger configuration simply enter #[&#8216;Sending to browser&#8217;] in the Message field.

Finally run the application by right-clicking the project in the left hand side browser -> Run-As -> Mule Application. When you see the word DEPLOYED in your console that means your application should now be running and if you visit http://localhost:8081/salesforcedemo you should retrieve a JSON view of all the accounts in your Salesforce environment.
