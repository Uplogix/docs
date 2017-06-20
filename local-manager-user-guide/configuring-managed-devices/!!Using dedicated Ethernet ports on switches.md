>For a switch configured to use a dedicated Ethernet port with a static IP address, the Local Manager turns off the interface except when it is needed. When the Local Manager turns on the dedicated Ethernet port, it can take 30-50 seconds for the switch to start forwarding traffic if the Spanning Tree Protocol (STP) is running on the switch port.  Uplogix recommends using a feature like Cisco’s portfast STP feature when connecting a switch port to a Local Manager dedicated Ethernet port.

Sometimes, actions that result in a pull OS operation (such as using the **copy** command) may return messages that FTP has failed, because the pull operation starts before the interface is ready. The pull operation then succeeds when the pull is attempted using its secondary transfer method. *This issue is unique to switches using dedicated Ethernet ports with static IP addresses where the Spanning Tree Protocol is running on the switch port.*

If the dedicated Ethernet port uses DHCP, the interface remains up during normal operation.

There are two ways to prevent the problem:

 - Configure the dedicated Ethernet connection to use DHCP (not available for Uplogix 430 or 500 Local Managers)
OR
 - Enable the portfast feature on Cisco switch ports – see following configuration example:
 
```
interface FastEthernet1/0/1
description dedicated Ethernet to Local Manager
switchport access vlan 2
spanning-tree portfast
```