---
title: 'Activate mysql query logs on the fly'
date: 2019-02-14
categories: [IT]
tags: [mysql, it, logs]     # TAG names should always be lowercase
---
<p>login to your mysql instance as root user and then use this commands to active mysql query logs</p>
<pre>SET GLOBAL log_output = 'FILE';<br />SET GLOBAL general_log_file = 'nameoflogfile';<br />SET GLOBAL general_log = 'ON';</pre>