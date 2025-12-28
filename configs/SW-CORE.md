

enable 
configure  terminal
hostname SW-CORE

vlan 10
 name VLAN-MANAGEMENT
 exit
vlan 20
name VLAN-DMZ
exit
vlan 30
 name VLAN-1
 exit
 vlan 40
 name VLAN-2
 exit

interface vlan 10
ip address 172.16.2.5 255.255.255.0
no shutdown
exit
interface vlan 30
ip address 172.16.3.2 255.255.255.0
no shutdown
exit
interface vlan 40
ip address 172.16.4.2 255.255.255.0
no shutdown
exit 


interface  GigabitEthernet0/0
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40
 switchport trunk native vlan 10

no shutdown
exit

interface range GigabitEthernet0/1-2
switchport mode access
switchport access vlan 30
no shutdown
exit

interface  GigabitEthernet0/3  
switchport mode access
switchport access vlan 40
no shutdown
exit
interface  GigabitEthernet1/0 
switchport mode access
switchport access vlan 40
no shutdown
exit
end

en

conf t
snmp-server community TunTelec RO 

snmp-server group MYGROUP v3 auth read all 
snmp-server user NOC-Admin MYGROUP v3 auth md5 NewPassphrase123
snmp-server trap-source VLAN10
snmp-server enable traps 
snmp-server enable traps SLA 
snmp-server enable traps snmp linkdown linkup 
snmp-server enable traps ospf cisco-specific state-change nssa-trans-change
snmp-server enable traps syslog
snmp-server host 172.16.2.3 version 3 auth NOC-Admin


snmp-server view all mib-2 included
snmp-server view all system included
snmp-server view all interfaces included


logging on 
logging 172.16.2.3
logging source-interface vlan10
logging trap warning 

write memory
copy running-config startup-config





######################################################################
######################################################################







!


enable 
configure  terminal
hostname SW-CORE
!
vlan 10
 name MANAGEMENT
vlan 20
 name DMZ
vlan 30
 name LAN1
vlan 40
 name LAN2
!
interface GigabitEthernet0/0
 description UPLINK-to-pfSense
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 10
 switchport trunk allowed vlan 10,20,30,40
no shutdown
 exit
 
interface range GigabitEthernet0/1-2
switchport mode access
switchport access vlan 30
no shutdown
exit

interface  GigabitEthernet0/3  
switchport mode access
switchport access vlan 40
no shutdown
exit

interface  GigabitEthernet1/0 
switchport mode access
switchport access vlan 40
no shutdown
exit


interface Vlan10
 description Management VLAN
 ip address 172.16.2.5 255.255.255.0
 no shutdown
 exit

 interface vlan 30
ip address 172.16.3.2 255.255.255.0
no shutdown
exit

interface vlan 40
ip address 172.16.4.2 255.255.255.0
no shutdown
exit 
!

ip default-gateway 172.16.2.1
!


snmp-server view MYVIEW iso included
snmp-server group MYGROUP v3 auth read MYVIEW
snmp-server user NOC-Admin MYGROUP v3 auth md5 NewPassphrase123


snmp-server contact NOC-Team
snmp-server location DataCenter-Core

! Allow only Zabbix server to query SNMP
access-list 50 permit 172.16.2.20
snmp-server community public RO 50

! Set trap destination to Zabbix server (v3 auth)
snmp-server host 172.16.2.20 version 3 auth NOC-Admin

! Enable the essential SNMP traps that your switch supports
snmp-server enable traps snmp
snmp-server enable traps coldstart
snmp-server enable traps warmstart
snmp-server enable traps linkdown
snmp-server enable traps linkup

! Optional but recommended
snmp-server enable traps authentication



end
write memory


end
write memory
