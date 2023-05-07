---
title: 'Unifi Controller Service does not start after update'
date: 2019-02-16
categories: [IT]
tags: [unifi, update, java, raspberry]
---
```
Feb 16 17:45:08 moshpit systemd[1]: Starting unifi...
Feb 16 17:45:24 moshpit unifi[908]: Feb 16, 2019 17:45:24 PM org.apache.commons.ttpclient.HttpMethodDirector executeWithRetry
INFO: I/O exception (java.net.ConnectException) caught when processing request:
```
<p>Solution is quite simple, you have to update your Java Installation to get rid of this issue.</p>
<p>This Version will work</p>
<pre>pi@moshpit:~ $ java -version<br />java version "1.8.0_201"<br />Java(TM) SE Runtime Environment (build 1.8.0_201-b09)<br />Java HotSpot(TM) Client VM (build 25.201-b09, mixed mode)</pre>
<p>Stop the Service</p>
<pre>sudo systemctl stop unifi</pre>
<p>Enter the Java Directory</p>
<pre>cd /usr/lib/jvm</pre>
<p>Backup old Java</p>
<pre>sudo mv &lt;oldversion_dir&gt;/ backup_oldjava</pre>
<p>Copy the new Java into the old Directory or simple use a symbolic link&nbsp;</p>
<pre>sudo cp -rf /usr/java/jdk1.8.0_201/ &lt;javadir&gt;</pre>
<p>Start the Service again</p>
<pre>sudo systemctl start unifi</pre>
<p>&nbsp;</p>