When connecting managed devices to the dedicated Ethernet ports of the Local Manager, configure their dedicated Ethernet connections to use static IP addresses or acquire DHCP addresses from the Local Manager.

>Dedicated Ethernet is not available for the Uplogix 430 and 500 Local Manager platforms, as they provide serial device ports only.

When setting the Local Manager to assign DHCP addresses to devices, the DHCP pool must not overlap with other pools or subnets:

 - the base address must not overlap the system's management IP address
 - the base address must not overlap existing static assignments on ports

> **CAUTION:** If these requirements are not met, the Local Manager will not assign addresses properly and Ethernet-related features will be unavailable.

Use the **config system protocols dhcp** command to set the base DHCP address that will be used in generating addresses.

The syntax for this command is: **config system protocols dhcp [nnn.nnn.nnn]** where nnn.nnn.nnn is the base address to be used. The default base address is 169.254.100.

The devices connected to individual ports must also be configured to use DHCP. When configuring a device on a port using the **config init** command, the dialog asks whether to configure a dedicated Ethernet port. If you respond with **y**, the next prompt asks whether to use DHCP. 

```
Configure dedicated ethernet port? (y/n) [n]: y
Use DHCP? (y/n) [n]: y
```

If the device is configured to use DHCP, it is not accessible until it requests a DHCP address.

Changes to the **config system protocols dhcp** setting take effect after restarting the Local Manager.

Control Center: Inventory > Local Manager Summary Page > Network > Protocols > DHCP Server Settings.

<!-- 5.2 --> 
