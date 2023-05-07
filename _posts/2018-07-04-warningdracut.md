---
title: 'Warning: dracut-initqueue timeout CentOS7'
date: 2018-07-04
categories: [IT]
tags: [centos, it, dracut-initqueue, redhat]     # TAG names should always be lowercase
---
<p>common on recent harware changes<br />First boot into the rescue mode, then change to the boot directory</p>
<pre>cd /boot</pre>
<p>perform a copy of the current files as security purpose</p>
<pre>cp -p initramfs-3.10.0-693.17.1.el7.x86_64.img initramfs-3.10.0-693.17.1.el7.x86_64.img.bak</pre>
<p>build a new one</p>
<pre><code>dracut -f -H initramfs-3.10.0-693.17.1.el7.x86_64.img 3.10.0-693.17.1.el7.x86_64</code></pre>