---
title: Resolving the "APIKey is Blocked" error in Mule
author: Mike Conroy
layout: post
permalink: /2020/04/resolving-api-key-blocked-error/
comments: true
categories:
  - Computing
  - Technology
  - MuleSoft
  - APIs
  - Mule 4
  - API Manager
---

[![MuleSoft Logo](/assets/images/MuleSoft/logo.png){: .centre-image}](https://www.mulesoft.com/)

I recently had to setup Anypoint Studio on a new machine to continue developing Mule APIs. Quite quickly I hit an issue when running an API locally I wouldn't get any response or messages in the logs when the API was called. This is a problem I have had other Mule developers (especially those newer to MuleSoft) ask previously how to resolve so I have decided to write up the explanation.

# The Problem

You have created the API Specification in Design Centre.

Published it to Exchange.

Created it in API Manager to be managed.

Imported it to Anypoint Studio to be developed.

Added Auto-Discovery code to link it to API Manager.

You go to run it locally in Anypoint Studio and it appears to succesfully deploy but when you call it you get no response and nothing new appears in the logs. After some hunting you find the following error in the logs during deployment:

<div style="text-align: center; font-style: italic;">API ApiKey{id='16122111'} is blocked (unavailable).</div>

{% include image.html url="/assets/images/MuleSoft/blocked-apikey.png" description="ApiKey is blocked error" %}

The API Manager also does not mark the API as Active to show the implementation is running and connected.

# The Cause

The issue occurs as the embedded Mule runtime (in Anypoint Studio) is not authenticated with the Anypoint Platform so although it has the API ID that is not enough to connect to the API Manager. This prevents a third party from registering a Mule App against *your* API in the API Manager (e.g. if they mistyped the ID).

# The Resolution

#### Anypoint Studio

To resolve this in Anypoint Studio go to Window -> Preferences -> Anypoint Studio -> API Manager.

You will see two fields that you need to populate; Client ID & Client Secret.
{% include image.html url="/assets/images/MuleSoft/env-credentials-anypoint-studio.png" description="Environment Credentials - Studio Configuration" %}

These fields need to be populated with either Organisation Credentials or Business Group Credentials.

These can be obtained by going to [Anypoint Platform](https://anypoint.mulesoft.com) -> Management Center -> Access Management -> Organization.

Click the Business Group or Organization name that the API has been created in.

Copy the Client Id & Client Secret into the configuration in Anypoint Studio.
{% include image.html url="/assets/images/MuleSoft/orginfo.png" description="Anypoint Platform Organisation Information" %}

Alternatively, the credentials can also be picked up from the Environments tab in Access Management.
If you don't have access to Access Management you will need to request these credentials from your Platform Admin.

Click Validate and ensure the green tick appears confirming the credentials are correct.
Re-run the Mule App and the error should no longer appear and you will be able to call the API and get a response.

{% include image.html url="/assets/images/MuleSoft/valid-success.png" description="Validation Succesful" %}

#### CloudHub & Runtime Manager

Apps deployed to CloudHub or on-premise will also need the above Client ID & Secret set as properties.
The properties to set are:

- *anypoint.platform.client_id*
- *anypoint.platform.client_secret*


Hope this helps, more information on this can be found [here](https://docs.mulesoft.com/api-manager/2.x/org-credentials-config-mule4).
