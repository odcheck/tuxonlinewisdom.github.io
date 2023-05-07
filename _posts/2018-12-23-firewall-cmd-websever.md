---
title: 'firewall-cmd Webserver Access on the public Zone'
date: 2018-02-07
categories: [IT]
tags: [redhat, firewall, centos, firewall-cmd, https, http, webserver]
---
<p>short but sweet</p>
<pre>firewall-cmd --permanent --zone=public --add-service=http<br />firewall-cmd --permanent --zone=public --add-service=https<br />firewall-cmd --reload</pre>