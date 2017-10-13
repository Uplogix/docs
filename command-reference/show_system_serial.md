<!-- 5.4 -->

Shows whether the Uplogix Local Manager’s console port is configured for null-modem operation. To display a connected device’s serial console settings, use the **show serial** command.

# Command availability 

CLI resource: system

Uplogix system: 430, 3200

LMS offerings: All

# Syntax 

```
show system serial
```

# Usage 

```
[admin@xyzcoAus01]# show system serial
Null modem: no
```

# In the Uplogix web interface

**Inventory > group page > System > Serial** - specific to this inventory group

**Inventory > Local Manager page > System > Serial** - specific to this system

# History 

3.4 - This command was introduced to replace show Local Manager serial.

# Related commands 

**config system serial**
**config serial**
**show serial**
