#uni 
VLANs - Virtual Local Area Networks - are a way to divide a physical network into multiple, separated LANS. 

To configure a VLAN you must on a switch set:
- what ports belong to a VLAN
- how to manage traffic between different switches: **trunk**
- how to manage communication between different VLANs: **routing** (needs a layer 3 device)

Every end device must be configured:
- IP coherent with VLAN
- Default Gateway = IP of VLAN
ES: VLAN 30: 192.168.30.xx
# Inter-VLAN routing
This needs a layer 3 device, there are 2 options:
## Legacy: IP router - multiple 'access' links
One router with multiple links, one for every VLAN. This router routes between these VLANS.

Switch:
```bash
s1(config)#vlan 10
s1(config-vlan)#vlan 30
exit
interface f0/11
switchport access vlan 10
interface f0/4 ecc
```

Router:
```bash
# Setting up VLAN 30
interface f00
ip address 172.17.30.1 255.255.255.0
no shutdown
```
## Router-on-a-stick: 
Router connected with a single link to a switch connected to multiple VLANs.
```bash
# associating sub interface with VLAN 10
r1(config)#interface gigabitEthernet 0/0.10
r1(config-subif)#encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface gigabitEthernet 0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
```
## Multilayer Switch - Layer 3 Switch
This is a more modern approach.
```bash
interface vlan 10
 ip address 192.168.10.1 255.255.255.0

interface vlan 20
 ip address 192.168.20.1 255.255.255.0

ip routing
```
# CISCO
```bash
enable
configure terminal

vlan 10
 name AMMINISTRAZIONE

vlan 20
 name TECNICI
 
# setting which ports belong to which VLAN:
interface fastEthernet 0/1
 switchport mode access
 switchport access vlan 10

interface fastEthernet 0/2
 switchport mode access
 switchport access vlan 20
 
# Setting a trunk: multiple VLANs working on the same interface
interface gigabitEthernet 0/1
 switchport mode trunk
 # per consentire solo alcune vlan:
 switchport mode trunk allowed 10,20
 
 
show vlan brief
show interface trunk
```