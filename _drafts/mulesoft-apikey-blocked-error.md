---
title: Mule - Resolving the "APIKey is Blocked" error
author: Mike Conroy
layout: post
permalink: /2020/04/...
comments: true
categories:
  - Computing
  - Technology
  - MuleSoft
  - APIs
  - Mule 4
  - API Manager
---

[![Jekyll Logo](/assets/images/MuleSoft/logo.png){: .centre-image}](https://www.mulesoft.com/)


# The Problem

You have created the API Specification in Design Centre.

Published it to Exchange.

Created it in API Manager to be managed.

Imported it to Anypoint Studio to be developed.

Added Auto-Discovery code to link it to API Manager.

You go to run it locally in Anypoint Studio and it appears to succesfully deploy but when you call it you get no response and nothing appears in the logs. After some hunting you find the following error in the logs:

*API ApiKey{id='16122111'} is blocked (unavailable).*

{% include image.html url="/assets/images/MuleSoft/blocked-apikey.png" description="Blocked ApiKey Error" %}

When you call the API you get no response and no log messages in the console. The API Manager also does not mark the API as Active to show an implementation is running.

The issue occurs as the embedded Mule runtime (in Anypoint Studio) is not authenticated with the Anypoint Platform so although it has the API ID that is not enough to connect to the API Manager.

To resolve this in Anypoint Studio go to Window -> Preferences -> Anypoint Studio -> API Manager.
You will see two fields that you need to populate; Client ID & Client Secret.
{% include image.html url="/assets/images/MuleSoft/env-credentials-anypoint-studio.png" description="Environment Credentials - Studio Configuration" %}

Obtaining the Client ID & Client Secret of the Environment.
In Anypoint Platform[link] go to Management Center -> Access Management -> Organization.
Click the Business Group or Organization name that the API has been created in.
Copy the Client Id & Client Secret into the configuration in Anypoint Studio.
{% include image.html url="/assets/images/MuleSoft/orginfo.png" description="Anypoint Platform Organisation Information" %}

Alternatively, the credentials can also be picked up from the Environments tab in Access Management.
If you don't have access to Access Management you will need to request these credentials from your Platform Admin.

Click Validate and ensure the green tick appears confirming the credentials are correct.
Re-run the Mule App and the error should no longer appear and you will be able to call the API and get a response.

{% include image.html url="/assets/images/MuleSoft/valid-success.png" description="Validation Succesful" %}
