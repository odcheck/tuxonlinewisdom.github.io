---
title: 'Nagwin free Edition for easy Monitoring at home'
date: 2021-04-30
categories: [IT]
tags: [nagwin, nagios, monitoring, windows, snmp, linux]
---
After I had set up everything at home, I wanted to transfer the whole thing into a simple monitoring system like Nagios for the fun of it. Unfortunately, I used the Raspberry Pi for the UniFi controller, so that I only had a Dell Optiplex Mini, which I could use as a server for this activity. The good guy still had a Windows 10 Pro, which already severely limits the choice of monitoring software. I wasted about 10 minutes with the free version of PRTG until I discovered Nagwin, which comes with Nagios 4.4.5 and has a crude cygwin construct under the hood. The free version can monitor up to 20 hosts and 100 services, which is enough for my project.

[Get nagwin from here](https://itefix.net/nagwin){:target="_blank"}


## Issues and Fixes
Of course, there were a few challenges right away. The blat tool to send mails installed but can not use gmail as smtp, not to mention the notification command. The firewall settings in Windows 10 Professional, which blocked access to the web interface and the check_smnp.exe does not work.

### blat and google
For this we need stunnel, otherwise we can not send mails via google smtp.
* Download stunnel
* Make a backup of the stunnel.conf and use this one 

```
socket = l:TCP_NODELAY=1
socket = r:TCP_NODELAY=1
;debug = 7
;output = stunnel.log

client = yes

[pop3s]
accept  = 995
connect = pop.gmail.com:995

[ssmtp]
accept  = 465
connect = smtp.gmail.com:465
```

* Create a google App Password for the mail account and use this

* Put your password and username in **$USER1$** and **$USER2$** in ../resource.cfg like this

```
# Sets $USER1$ to be the path to the plugins
$USER1$=/plugins

# Sets $USER2$ to be the path to event handlers and stuff
$USER2$=/bin

# Store some usernames and passwords (hidden from the CGIs) like mail account
$USER3$=username@gmail.com
$USER4$=illstrongpasswordfromgoogle

# smnp community
$USER5$=nicepassworddude
```

* I've edit the notification command for Hosts and Services like this

```
# 'notify-host-by-gmail' command definition
define command{
	command_name	notify-host-by-gmail
	command_line	/usr/bin/printf "%b" "***** Nagios *****\n\nNotification Type: $NOTIFICATIONTYPE$\nHost: $HOSTNAME$\nState: $HOSTSTATE$\nAddress: $HOSTADDRESS$\nInfo: $HOSTOUTPUT$\n\nDate/Time: $LONGDATETIME$\n" | /bin/blat - -to $CONTACTEMAIL$ -f $USER3$ -subject "** $NOTIFICATIONTYPE$ Host Alert: $HOSTNAME$ is $HOSTSTATE$ **" -server 127.0.0.1 -port 465 -u $USER3$ -pw $USER4$
	}

# 'notify-service-by-gmail' command definition
define command{
	command_name	notify-service-by-gmail
	command_line	/usr/bin/printf "%b" "***** Nagios *****\n\nNotification Type: $NOTIFICATIONTYPE$\n\nService: $SERVICEDESC$\nHost: $HOSTALIAS$\nAddress: $HOSTADDRESS$\nState: $SERVICESTATE$\n\nDate/Time: $LONGDATETIME$\n\nAdditional Info:\n\n$SERVICEOUTPUT$\n" | /bin/blat - -to $CONTACTEMAIL$ -f $USER3$ -subject "** $NOTIFICATIONTYPE$ Service Alert: $HOSTALIAS$/$SERVICEDESC$ is $SERVICESTATE$ **" -server 127.0.0.1 -port 465 -u $USER3$ -pw $USER4$
	}
```

### Firewall in Windows 10
Just create a new incoming rule and allow port 443. Port 80 if you also want to have the redirect feeling.

### check_snmp.exe
Is totaly useless out of the box.
But here I found an already finished variant on the net, which I simply replaced including the attached DLL. The check_snmp.exe delivers however NULL with network interfaces, which is to be gotten along however, since here also a check_snmp_if.exe was present, which serves exactly my requirement.

[Grab it from here](https://exchange.nagios.org/directory/Plugins/Uncategorized/Operating-Systems/Windows-NRPE/NagiosPluginsNT/details){:target="_blank"}


### pnp4nagios
With pnp4nagios some templates do not work, but this is usually due to the fact that in the template php file used only the file name of the template file, which is actually responsible for it. In short, simply copy+paste.


