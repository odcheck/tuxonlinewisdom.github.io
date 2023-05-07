---
title: 'Latest IPMI command that I have used'
date: 2019-02-26
categories: [IT]
tags: [ipmi, bmc, ipmitool]
---
<p>Reset the IPMI</p>
<pre>ipmitool mc reset cold -I lan -H 10.0.0.1 -U admin -P password</pre>
<p>Boot direct into the Bios on next Boot</p>
<pre>ipmitool -I lanplus -H 10.0.0.101 -U ADMIN chassis bootdev bios<br />Set Boot Device to bios<br /><br /></pre>
<p>&nbsp;</p>