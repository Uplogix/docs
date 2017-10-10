<!-- 5.4 -->

Used to pull configuration files from network devices. The files are compared to the versions previously stored. If the content is different, the version stored as current is moved to previous, overwriting the existing previous version, and the new file is stored as current. 

The pull process will retry several times if it does not successfully retrieve the file. The file transfer protocol and number of retries are options that default to the best settings for the device; these can be overridden using the config settings command. File transfer may be configured as console, TFTP, FTP or XModem.

Pulling a configuration at 9600 baud may take several minutes on some network devices. You may choose to change the default method to TFTP (if available) using the config settings command.

Rules can be defined to automate this operation using the pullStartupConfig action.

# Command availability

CLI resource: port

Device makes: Alcatel, Cisco, iDirect, ND Satcom, Nortel, Tasman

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
pull startup-config
```

# Usage 

The startup configuration is scheduled to be pulled periodically during initial configuration. The default interval is every 24 hours. The pull startup-config operation can be removed from the schedule using the config removejob command.

```
[admin@UplogixLM (port1/1)]# pull startup-config
Retrieving startup-config from device ...
Complete. startup-config pulled.
startup-config saved to archive as current.
In the Uplogix web interface
Pull operations are automatically scheduled by Uplogix Control Center.
```

# History 
--
#Related commands 

- **push startup-config**
- **copy**
- **rollback config**
