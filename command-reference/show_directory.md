<!-- 5.4 -->

Displays files stored for each supported device.

# Command availability

CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, native, server

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show directory [-v]
```

The –v parameter ads file size and date display.

# Usage 

Files are associated with a particular port, make, model, and OS combination. If you change a device on one of the Uplogix Local Manager’s ports, the files will not be accessible from that device unless it is a similar make, model, and OS combination.

```
[admin@xyzcoAus01 (port1/1)]# show dir
Config
    Startup
        Current   startup-config
        Previous  startup-config
OS
        Current   cat4000-k8.7-6-7.bin
```

# History 

1.4 - The verbose flag (-v) was modified to display archived versions of device files.

# Related commands 

- **copy**
