---
title: 'Setup Foreman locale issue on Centos 7'
date: 2018-02-07
categories: [IT]
tags: [centos, locales, foreman]
---
<p>is about a locale issue during a foreman setup on CentOS 7.</p>
<pre>locale environment variables were bad; continuing with LANG=C</pre>
<p>In my case the output of locale -a showed en_US.utf8 but the output of env and the line line in /etc/locale.conf reads different.<br />en_US.UTF-8 which seams to be wrong or not translated correctly.<br />Long Story short, either export the correct settings or update the /etc/locales.conf file so that it read like this for example</p>
<pre>LC_ALL=en_US.utf8<br />LANG=en_US.utf8<br />LANGUAGE=en_US.utf8</pre>
