<!-- 5.4 -->

Used to push configuration files to network devices. Use **config settings** to set the primary and secondary file transfer protocols and the maximum number of attempts. TFTP, FTP, and XModem are supported.

Rules can be defined to automate this operation using the pushStartupConfig action.

# Command availability

CLI resource: port

Device makes: Alcatel, Cisco, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
push startup-config <previous | candidate | current named> [-reboot]
```

# Usage 

```
[admin@UplogixLM (port1/1)]# push running-config previous
Copying running-config to device.
Transfering via XModem. (Attempt 1)
Sent running-config at 581 B/s.
File running-config was transferred to the device successfully via XModem.
runningConfig downloaded to device. 
```

The push startup-config operation will try the secondary transfer method if the primary method fails, and will make up to the specified number of attempts if necessary.
 
push can be scheduled to automatically update using the config schedule command.

# In the Uplogix web interface

**Schedule > Scheduled Tasks** - all equipment that matches the selected filter

**Inventory > Local Manager page > port detail > schedule** - specific to this system

# History 
--

# Related commands 

**pull startup-config**
**copy**
