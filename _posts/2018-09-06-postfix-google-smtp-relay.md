---
title: 'Postfix Google as SMTP Relay'
date: 2018-09-06
categories: [IT]
tags: [postfix, google, smtp, relay]
---
<p>as a fix solution you can use google, as smtp relay for e.g. notifications. In this example I am working on a Fedora 27 Host.</p>
<p>Install needed packages</p>
<pre>dnf -y install postfix mailx cyrus-sasl-plain</pre>
<p>Restart and enable services</p>
<pre>systemctl restart postfix &amp;&amp; systemctl enable postfix</pre>
<p>Adjust&nbsp;/etc/postfix/main.cf depends your needs (marked in red)</p>
<pre>myhostname = <span style="color: #ff0000;">zuerich.tuxclouds.org</span><br /><br />relayhost = [smtp.gmail.com]:587<br />smtp_use_tls = yes<br />smtp_sasl_auth_enable = yes<br />smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd<br />smtp_tls_CAfile = /etc/ssl/certs/ca-bundle.crt<br />smtp_sasl_security_options = noanonymous<br />smtp_sasl_tls_security_options = noanonymous</pre>
<p>Setup the secret</p>
<pre>vim /etc/postfix/sasl_passwd<br />[smtp.gmail.com]:587 <span style="color: #ff0000;">username:password</span></pre>
<p>Issue the command <a href="http://www.postfix.org/postmap.1.html">postmap</a> to read the new secret</p>
<pre>postmap /etc/postfix/sasl_passwd</pre>
<p>Set correct owner and permissons</p>
<pre>chown root:postfix /etc/postfix/sasl_passwd<br />chmod 640 /etc/postfix/sasl_passwd</pre>
<p>Reload the service</p>
<pre>systemctl reload postfix</pre>
<p>Verify the setup, by sending you a Test Notification Mail</p>
<pre>echo "Test Mail" | mail -s "Test Notification Mail" <span style="color: #ff0000;">joe@example.net</span></pre>
<p>&nbsp;</p>
