---
title: 'SSSD System Security Service Daemon'
date: 2019-03-12 # yyyy-mo-day
categories: [IT]
tags: [freeipa, ldap, linux, sssd]     # TAG names should always be lowercase
---
## An overview of the SSSD architecture 

The SSSD consists of several processes, each of them has its own function. The SSSD processes can be one of the following:

### the monitor
The purpose of the monitor process is to spawn the other processes, periodically ping them if to check if they are still running and respawn them if not. There is only one instance of the monitor process at a given time.
### a data provider
The data provider process communicates with the remote server (i.e. queries the remote server for a user) and updates the cache (i.e. writes the user entry. There is one Data Provider process per remote server.
### a responder
The system libraries (such as the Name Service Switch module or the PAM module) communicate with the corresponding responder process. When the responder process receives a query, it checks the cache first and attempts to return the requested data from cache. If the data is not cached (or is expired), the responder sends a message to the Data Provider requesting the cache to be updated. When the Data Provider is done updating the cache, the responder process checks the cache again and returns the updated data. It is important to note that the responder process never returns the data directly from the server, the data is always written to the cache by the Data Provider Process and returned to the calling library in the responder process.
### a helper process
The SSSD performs some operations that would be blocking, such as kinit in a special helper sub-process. The sub-processes are forked from the Data Provider processes again for each operation, there is no preforked pool of helper processes. The SSSD establishes pipes towards the processes standard input and output to communicate with the child using an ad-hoc wire protocol.

<p>&nbsp;</p>
<p>Source:&nbsp;<a href="https://docs.pagure.org/SSSD.sssd/developers/ipc.html" target="_blank" rel="noopener">https://docs.pagure.org/SSSD.sssd/developers/ipc.html</a></p>
<p>&nbsp;</p>