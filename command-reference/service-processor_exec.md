<!-- 5.4 -->

Allows you to pass commands to the service processor.

# Command availability 

CLI resource: port

Device makes: HP, Sun, server

Uplogix Local Managers: All except Uplogix 430

LMS offerings: Advanced

# Syntax 

```
service-processor execute <command>
```

# Usage 

Service processor commands that can be executed:

**channel** - Configure Management Controller channels
**chassis** - Get chassis status and set power state
**event** - Send pre-defined events to MC
**fru** - Print built-in FRU and scan SDR for FRU locators
**fwum** - Update IPMC using Kontron OEM Firmware Update Manager
**i2c** - Send an I2C Master Write-Read command and print response
**isol** - Configure IPMIv1.5 Serial-over-LAN
**kontronoem** - OEM Commands for Kontron devices
**lan** - Configure LAN Channels
**mc** - Management Controller status and global enables
**pef** - Configure Platform Event Filtering (PEF)
**picmg** - Run a PICMG/ATCA extended cmd
**power** - Shortcut to chassis power commands
**raw** - Send a RAW IPMI request and print response
**sdr** - Print Sensor Data Repository entries and readings
**sel** - Print System Event Log (SEL)
**sensor** - Print detailed sensor information
**session** - Print session information
**sunoem** - OEM Commands for Sun servers
**user** - Configure Management Controller users

# History 

3.4 - This command was introduced.

# Related commands
--
