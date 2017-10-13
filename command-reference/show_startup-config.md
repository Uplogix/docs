<!-- 5.4 -->

Displays the device’s collected startup configuration.

# Command availability 

CLI resource: port

Device makes: Alcatel, Cisco, iDirect, ND Satcom, Nortel, Tasman

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show startup-config [candidate | current | previous | <user ver> | archive #]
```

# Usage 

```
[admin@UplogixLM (port1/1)]# show startup-config previous
!
version 12.0
no service pad
service Timestamps debug uptime
service Timestamps log uptime
no service password-encryption
!
hostname DMZ-2948
!
no logging console
!
ip subnet-zero
no ip routing
bridge irb
!
interface FastEthernet1
 no ip address
 no ip directed-broadcast
 no ip mroute-cache
 bridge-group 1
!
interface FastEthernet2
 no ip address
 no ip directed-broadcast
 no ip mroute-cache
 bridge-group 1
!
interface FastEthernet3
 no ip address
 no ip directed-broadcast
 no ip mroute-cache
```

# In the Uplogix web interface

**Inventory > system page > port detail > Files > startup** - specific to this device

# History 
--
# Related commands 

- **pull start-up config**
- **show running-config**
