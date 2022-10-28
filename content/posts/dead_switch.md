---
title: "WireGuard Dead Switch on Raspbian"
date: 2022-10-27T20:16:05+02:00
draft: false
params:
    ShowPostNavLinks: true
    ShowCodeCopyButtons: true
    ShowBreadCrumbs: true
tags: ["Linux"]
categories: ["IT"]
#weight: 1 #pin possition
---
![](/img/zwsem.jpg?classes=float-left,shadow)
 ### WireGuard on Raspbian as Dead Switch
Modify `rc.local` in `/etc`.  
Enter those lines after `fi`.  
**piuk** is a name of the WireGuard network interface. 

``` cli       
sleep 15  
sudo iptables -t nat -A POSTROUTING -o piuk -j MASQUERADE  
sudo iptables -A FORWARD -i piuk -o eth0 -m state --state RELATEDESTABLISHED   -j ACCEPT  
sudo iptables -A FORWARD -i eth0 -o piuk -j ACCEPT  
exit 0  
```