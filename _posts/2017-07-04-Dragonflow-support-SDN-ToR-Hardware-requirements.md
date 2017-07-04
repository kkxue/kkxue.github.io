---
layout: post
author: kkxue
title: Dragonflow support SDN ToR Hardware requirements
date: 2017-07-04 18:34:00 -0700
categories:
- Dragonflow
tags:
- Dragonflow
- SDN ToR
---

### Add SDN ToR Hardware In 
There are several model of SDN ToR Hardwares support OVSDB/OpenFlow/RPC
we want to add it to our sdn solution to achieve automated underlay network provisioning, like automated create VTEP, translation between vlan and vxlan. 
does Hierarchical Port Binding (SDN ToR) features  can really achieve the goal?
### Automatic Topology Discovery 
Including SDN ToR Hardware and compute node server,should  dynamic display of topology changes.
for now, df support it?
### Northbound API
AFAIK, Currently df doesn't have Northbound api, right?
if so, it makes third party Controllers unable to interact with df 
### Control SDN ToR Hardware Directly
if  third party Controllers  Control SDN ToR Hardware,it will have a problem on consistency of data, does it possible to Control SDN ToR Hardware Directly?


ref:
http://www.h3c.com.hk/Technical_Support___Documents/Technical_Documents/Switches/H3C_S10500/H3C_S10500_Series_Switches/Configure/Configuration_Guide/H3C_S10500_CG-R7523P01-6W100/12/201609/951138_1285_0.htm

