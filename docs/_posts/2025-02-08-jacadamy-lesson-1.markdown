---
layout: post
title:  "Google cloud guide example"
categories: jacademy
published: false
---
# Getting started with google cloud

## Setup a free-tier GCP VM and deploy a web app

This is a step-by-step guide on how to create a Virtual Machine (VM) in Google
Cloud Platform (GCP) with Ubuntu OS, located in the eu-mil region, how to SSH into
it and deploy a Spring Boot w/ React web application on it, running on Docker with
Postgres & Tomcat

### 1) Create a Google Cloud Platform Account and Set Up Billing:

- Go to the Google [Cloud Platform Console](https://console.cloud.google.com/)
- Click on "Create account" and follow the instructions to create a new Google
  account.
- Once you have an account, log in to the GCP Console
- If needed, create a project, name in PwC Java Academy
- Set up your billing information by clicking on the billing section in the console
  and adding your payment method. Do not worry about charges, we will utilise
  the $300 free credits
![gCloudPurchace.png](/assets/images/jacademy/gCloudPurchace.png)

### 2) Create an Ubuntu OS Virtual Machine:
...

### 4) SSH into the Virtual Machine:

**Install zip/unzip**

{% highlight bash %}
sudo apt-get install zip
sudo apt-get install unzip
{% endhighlight %}

**Java & Maven through SDKMan**
{% highlight bash %}
curl-s "https://get.sdkman.io" | bash
sdk install java
sdk install maven
{% endhighlight %}