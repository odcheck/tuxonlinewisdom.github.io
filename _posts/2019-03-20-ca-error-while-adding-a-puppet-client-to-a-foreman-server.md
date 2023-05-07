---
title: 'CA error while adding a puppet client to a Foreman Server'
date: 2019-03-20 # yyyy-mo-day
categories: [IT]
tags: [deployment, puppet, ca, ssl, foreman]     # TAG names should always be lowercase
---
<p>on the foreman server I had to run:</p>
<pre>puppet cert clean client-certname</pre>
<p>on the client</p>
<pre>rm -rf /var/lib/puppet/ssl</pre>
<p>and</p>
<pre>puppet agent -td --server=&lt;foremanservername&gt;</pre>
<h3>Additional Hints</h3>
<p>To fix this, remove the certificate from both the master and the agent and then start a puppet run, which will automatically regenerate a certificate.</p>
<p>On the master:</p>
<pre>puppet cert clean &lt;fqdn-hostname&gt;</pre>
<p>On the agent:</p>
<p>1a. On most platforms: find /var/lib/puppet/ssl -name &lt;fqdn-hostname&gt;.pem -delete<br />1b. On Windows: del "\var\lib\puppet\ssl\certs\&lt;fqdn-hostname&gt;.pem" /f<br />2. puppet agent -t<br /><br /></p>
