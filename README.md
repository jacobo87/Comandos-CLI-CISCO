[![Unlicense](https://img.shields.io/badge/License-Unlicense-blue.svg)](https://unlicense.org/)
[![made-with-Markdown](https://img.shields.io/badge/Made%20with-Markdown-1f425f.svg)](http://commonmark.org)
[![GitHub watchers](https://badgen.net/github/watchers/jacobo87/Comandos-CLI-CISCO/)](https://GitHub.com/jacobo87/Comandos-CLI-CISCO/watchers/)



# Configurar Switch y router Cisco
> Comandos básicos para configurar un ROUTER CISCO mendiante CLI 

### Cambiar nombre
```
Switch>enable
Switch#configure terminal
Switch(config)#hostname SW_2
SW_2(config)#
```
### Configurar contraseña cifrada
```
SW_2(config)#enable secret asir1a
```
### Configurar vlan 1
```
SW_2(config)#interface vl
SW_2(config)#interface vlan 1
SW_2(config-if)#ip address 192.168.2.2 255.255.255.0
SW_2(config-if)#no shutdown
```
### Configurar vlan
```
Switch>enable
Switch#configure terminal

Enter configuration commands, one per line.  End with CNTL/Z.

Switch(config)#vlan 2
Switch(config-vlan)#name contabilidad
Switch(config-vlan)#exit
Switch(config)#interface range fastEthernet 0/1-2
Switch(config-if-range)#switchport access vlan 2
Switch(config-if-range)#switchport mode access
Switch#show vlan
```
### Guardar configuración
```
SW_2#copy running-config startup-config

Destination filename [startup-config]?

Building configuration...

[OK]

SW_2#
```
### Configurar enlaces troncales
```
sw_jag_gestion>enable
sw_jag_gestion#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
sw_jag_gestion(config)#interface gigabitEthernet 0/1
sw_jag_gestion(config-if)#switchport mode trunk
sw_jag_gestion(config-if)#
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to up
sw_jag_gestion(config-if)#switchport trunk allowed vlan 102
sw_jag_gestion(config-if)#switchport trunk allowed vlan 202
sw_jag_gestion(config-if)#switchport trunk allowed vlan 302
sw_jag_gestion(config-if)#
```
### Configurar VTP
```
Switch>enable
Switch#conf terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname vtp-server
vtp-server(config)#vtp mode server
Device mode already VTP SERVER.
vtp-server(config)#vtp domain asir_domain
Changing VTP domain name from NULL to asir_domain
vtp-server(config)#vtp password 1234
Setting device VLAN database password to 1234
vtp-server(config)#interface gigabitEthernet 0/1
vtp-server(config-if)#switchport mode trunk
vtp-server(config)#interface gigabitEthernet 0/2
vtp-server(config-if)#switchport mode trunk
vtp-server(config)#interface fastEthernet 0/1
vtp-server(config-if)#switchport mode trunk
```
### Configurar switch multicapa
```
Switch>enable
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#vl
Switch(config)#vlan 10
Switch(config-vlan)#exit
Switch(config)#vlan 20
Switch(config-vlan)#exit
Switch(config)#interface vlan 10
Switch(config-if)#
%LINK-5-CHANGED: Interface Vlan10, changed state to up
Switch(config-if)#ip address 192.168.10.1 255.255.255.0
Switch(config-if)#no shutdown
Switch(config-if)#exit
Switch(config)#interface vlan 20
Switch(config-if)#
%LINK-5-CHANGED: Interface Vlan20, changed state to up
Switch(config-if)#ip address 192.168.20.1 255.255.255.0
Switch(config-if)#no shutdown
Switch(config-if)#exit
Switch(config)#interface range gigabitEthernet 1/0/1-12
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 10
%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan10, changed state to up
Switch(config-if-range)#exit
Switch(config)#interface range gigabitEthernet 1/0/13-24
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 20
Switch(config-if-range)#
%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan20, changed state to up
Switch(config-if-range)#exit
Switch(config)#ip routing (**Muy importante**)
Switch(config)#
```
### Configurar DHCP
```
SW_2(config)#ip dhcp pool DHCP
SW_2(dhcp-config)#network 192.168.2.0 255.255.255.0
SW_2(dhcp-config)#default-router 192.168.2.1
SW_2(dhcp-config)#dns-server 1.1.1.1
SW_2(dhcp-config)#exit
SW_2(config)#ip dhcp excluded-address 192.168.2.100 192.168.2.254 (**Mal son las IPs excluidas.**)
SW_2(config)#exit
```
### Configurar enrutamiento CISCO
```
Router>enable
Router#conf terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname R2
R2(config)#interface gigabitEthernet 0/0
R2(config-if)#ip address 192.168.2.2 255.255.255.0
R2(config-if)#no shutdown
R2(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0, changed state to up
R2(config-if)#exit
R2(config)#interface gigabitEthernet 0/1
R2(config-if)#ip address 192.168.3.1 255.255.255.0
R2(config-if)#no shutdown
R2(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/1, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to up
R2(config-if)#exit
R2(config)#exit
R2#
R2#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
R2(config)#ip route 192.168.1.0 255.255.255.0 192.168.2.1
R2(config)#do show ip route
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP

      D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area

      N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2

      E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP

      i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area

      * - candidate default, U - per-user static route, o - ODR

      P - periodic downloaded static route

Gateway of last resort is not set

S    192.168.1.0/24 [1/0] via 192.168.2.1

    192.168.2.0/24 is variably subnetted, 2 subnets, 2 masks

C       192.168.2.0/24 is directly connected, GigabitEthernet0/0

L       192.168.2.2/32 is directly connected, GigabitEthernet0/0

    192.168.3.0/24 is variably subnetted, 2 subnets, 2 masks

C       192.168.3.0/24 is directly connected, GigabitEthernet0/1

L       192.168.3.1/32 is directly connected, GigabitEthernet0/1
R2(config)#
```


> [Jacobo Azmani](https://jacoboazmani.org) 
