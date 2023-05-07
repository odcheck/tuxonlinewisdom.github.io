---
title: 'MariaDB failes to start cause of tc.log' # Title in the Post as H1
date: 2019-06-17
categories: [IT] 
tags: [mariadb, start, logfiles] # always in small letters
#external_links:
#    target: _blank # target of external links
#external_url: '' # URL
#image:
#  src: # points to the image on cloudinary cdn starting with /
#  alt: # description 
---

**Solution** \
Just remove the tc.log File and afterwards the mariadb.service will start.