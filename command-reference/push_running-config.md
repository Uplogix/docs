<!-- 5.4 -->

Used to push configuration files to network devices. Use **config settings** to set the primary and secondary file transfer protocols and the maximum number of attempts. TFTP, FTP, and XModem are supported. Named running-configuration files referenced in the command line are case sensitive. 

Rules can be defined to automate this operation using the pushRunningConfig action.

# Command availability

CLI resource: port

Device makes: Alcatel, Cisco, Comtech EF Data, iDirect, Juniper, ND Satcom, Netscreen, Tasman

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
push running-config <previous | candidate | current | named > [-reboot]
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

The push operation will try the secondary transfer method if the primary method fails, and will make up to the specified number of attempts if necessary. 

Pushing a running configuration works in the same way as it would on a Cisco device. If an element is present in the stored copy but not the file being pushed, it remains in the configuration. Elements present in the file being pushed but not in the stored copy are added. Elements present in both the stored copy and the file being pushed will be updated.

push running-config can be scheduled to automatically update using the **config schedule** command.

# In the Uplogix web interface

**Schedule > Scheduled Tasks** - all equipment that matches the selected filter

**Inventory > local Manager page > port detail > schedule** - specific to this system

# History 

4.5 - Named running-configuration files added 

#Related commands 

- **pull running-config**
- **copy**
- **rollback config**