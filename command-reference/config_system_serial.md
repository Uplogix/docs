<!-- 5.4 -->

Interactive command to specify the Uplogix Local Manager's console port settings. To configure the console port for a device connected to the system, use the **config serial** command.

# Command availability 

CLI resource: system

Uplogix system: 400, 3200

LMS offerings: All

# Syntax 

```
config system serial
```

# Usage 

Changing the serial settings may stop communication with an external modem connected to the system’s console port. Be sure to read the configuration guide for your modem for important information.

```
[admin@UplogixLM]# config system serial
--- Existing Values ---
Null modem: no
Change these? (y/n) [n]: y
Enable null modem? (y/n) [n]: y
Do you want to commit these changes? (y/n): y
```

# In the Uplogix web interface

**Inventory > group page > System > Serial** - specific to this inventory group

**Inventory > Local Manager page > Network > Serial** - specific to this system

# History 
3.4 - This command was introduced to replace config envoy serial.

# Related commands 

- **show system serial**
- **config serial**
- **show serial**
