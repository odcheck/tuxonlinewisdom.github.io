---
title: 'Set static hostname on Unifi USG using the CLI'
date: 2021-04-16
categories: [IT]
tags: [unifi, usg, dhcp, cli]     # TAG names should always be lowercase
---

## Set the mapping
```
configure
set system static-host-mapping host-name host1.memoriam.com inet 192.168.1.201
set system static-host-mapping host-name host1.memoriam.com alias boltthrower
commit
save
```

## Delete the mapping
```
configure
delete service dhcp-server shared-network-name net_LAN_192.168.1.0-24 subnet 192.168.1.0/24 static-mapping aa-aa-aa-aa-aa-aa ip-address 192.168.1.40
delete service dhcp-server shared-network-name net_LAN_192.168.1.0-24 subnet 192.168.1.0/24 static-mapping aa-aa-aa-aa-aa-aa mac-address 'aa-aa-aa-aa-aa-aa'
delete service dhcp-server shared-network-name net_LAN_192.168.1.0-24 subnet 192.168.1.0/24 static-mapping aa-aa-aa-aa-aa-aa
commit
save
```
