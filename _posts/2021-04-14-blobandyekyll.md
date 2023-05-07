---
title: 'Hosting a static website on GCP'
date: 2021-04-14
categories: [IT]
tags: [cms, gcp, jekyll]     # TAG names should always be lowercase
---
I actually wanted to use blob storage with Azure, but they wouldn't accept a billing account with PayPal as a payment method, so I decided to use Google.

## What do we need
**or don't need**

* A Google Account
* A valid payment method
* A Storage Bucket, that's how they call it
* A domain would be nice and if you use the domain as bucket name, GCP will order a valid LetsEncrypt certificate for you.

