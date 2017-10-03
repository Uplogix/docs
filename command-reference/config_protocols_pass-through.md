Enables direct SSH and telnet connection to a device’s console using TCP ports. Once configured, the user or an automated script can connect to the device’s console port by SSH shell connection to a specific TCP port with all the rollback, session logging, and authority protection available through the LMS command line.

Pre-authenticated pass-through provides telnet based pre-authentication to a specific ip address tied to the permissions of a specific user. 

# Command availability 

CLI resource: port, modem, powercontrol

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, Garmin, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, native, server

Modem: All

Power controllers: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
config protocols pass-through <enable | disable> <telnet | ssh> [“port number”] [nopassword <username> <source IP> <binary>]
```

Port number is optional but must be between 1025 and 9999.

If a port is not specified, the default of 2000 + port number will be used. For example, port 1/1 would be accessible on port 2001.

Binary option allows all ASCII characters so “~” commands are not available

# Usage 

This change takes effect when the Uplogix system reboots.

```
[admin@xyzcoAus01 (port1/1)]# config protocols pass-through enable ssh
```

Pass-through port will be 2001.

SSH port change will take place after the next Local Manager restart.

# History 

2.5 – This command was moved from the Local Manager resource to the port resource.

4.3 – Added Pre-Authenticated telnet access using <username>’s privileges from <source IP>

# Related commands 

**show protocols pass-through**
