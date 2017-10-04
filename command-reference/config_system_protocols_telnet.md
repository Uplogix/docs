<!-- 5.4 -->

Configures the Uplogix Local Manager to respond to Telnet requests on TCP port 23.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system protocols telnet <enable | disable>
```

# Usage 

This change requires a reboot of the system to take effect.

```
[admin@UplogixLM]# config system protocols telnet enable
Telnet will be enabled after the next Local Manager restart.
```

# In the Uplogix web interface

**Inventory > group page > Local Manager configuration button > Protocols** - specific to this inventory group

**Inventory > expanded system page > Configuration tab > Protocols** - specific to this system

# History 

3.4 - This command was introduced.

# Related commands 

**show system protocols**
