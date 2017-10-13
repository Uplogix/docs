<!-- 5.4 -->

For devices with graphical user interfaces, Uplogix Local Managers provide xbrowser, a browser-based device management capability similar to KVM. 

Prerequisites for using this feature:

- The device that you manage via xbrowser must be configured with a dedicated Ethernet port.

- You must have an XServer installed on your computer. Supported XServers:
 - Cygwin (install X11 components)
 - Xming (required if using the SSH applet on the Uplogix Control Center)
 - X11 (X.Org version:1.3.0)


- You must use an SSH client that supports X11 display forwarding. Supported clients:
 - Cygwin
 - OpenSSH (OpenSSH 4.7p1, OpenSSL 0.9.8b 04 May 2006)
 - Uplogix Control Center's SSH applet
 - X-Windows

- Your SSH client must be configured for X11 display forwarding.

- Your SSH client must be configured so that xbrowser runs a trusted connection to the local XServer. This is the default for the Uplogix Control Center's SSH applet, but needs to be configured on some clients. For example, if you use Cygwin as your SSH client, configure it as follows:

 - export DISPLAY=:0.0
 - xauth generate :0.0 . trusted
 - ssh -Y 198.51.x.x
 - If it is not set up properly you will see the message "Warning: No xauth data; using fake authentication data for X11 forwarding."

> Note: PuTTY is not a supported client for xbrowser.

You will also need to use the config xbrowser command to configure xbrowser.

# Command availability 

CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, server

Uplogix Local Managers: All except Uplogix 430

LMS offerings: Advanced

# Syntax 
```
xbrowser
```

# Usage 

```
[admin@UplogixLM (port1/3)]# xbrowser
initializing browser for first time
```

> Note: At present, xbrowser does not support service processor firmware upgrades.

# History 
3.5 - This command was introduced.

# Related commands 

- **clear xbrowser**
- **config xbrowser**
- **show xbrowser**
