---
layout: default
title: Ryu Certification - Hewlett-Packard_HP2920 - config
---
# [Ryu Certification](https://ryu-sdn.org/certification.html)
* Hewlett-Packard HP2920

# OpenFlow related configuration
<pre>
HP-2920-48G# show config

Startup configuration: 34

; J9728A Configuration Editor; Created on release #WB.15.15.0006
; Ver #05:18.f3.ff.35.0d:29

hostname "HP-2920-48G"
module 1 type j9728a
logging ************
logging facility local0
timesync sntp
sntp unicast
sntp server priority 1 ************
time timezone 540
ip default-gateway ************
snmp-server community "public" unrestricted
openflow
   controller-id 1 ip 10.24.150.30 controller-interface vlan 1
   instance "br0"
      member vlan 2
      controller-id 1
      version 1.3
      connection-interruption-mode fail-standalone
      max-backoff-interval 5
      enable
      exit
   ip-control-table-mode
   enable
   exit
oobm
   no ip address
   exit
no lldp run
vlan 1
   name "DEFAULT_VLAN"
   no untagged 1-2
   untagged 3-48,A1-A2,B1-B2
   ip address ************ 255.0.0.0
   exit
vlan 2
   name "VLAN2"
   untagged 1-2
   no ip address
   exit
</pre>

# Version information
<pre>
HP-2920-48G# show version
Image stamp:
 /ws/swbuildm/rel_nashville_qaoff/code/build/anm(swbuildm_rel_nashville_qaoff_rel_nashville)
                Mar 15 2014 13:22:18
                WB.15.15.0006
                568
Boot Image:     Primary
</pre>

# Modified test scenario for switch restrictions
<pre>
$ find ryu/tests/switch/of13/ -name '*.json' -print0 | xargs -0 sed -i 's/\"table_id\":0/\"table_id\":102,\"priority\":1/g'
$ find ryu/tests/switch/of13/match/ -name '*.json' -print0 | xargs -0 sed -i 's/  0$/  102/g'
$ sed -i 's/table_id=ofp.OFPTT_ALL/table_id=102/g' ryu/tests/switch/tester.py;
</pre>

