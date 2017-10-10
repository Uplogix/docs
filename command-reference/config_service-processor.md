<!-- 5.4 -->

Allows you to enable and configure a server's service processor.  Initializes IPMI interactions to collect baseboard information and execute actions

# Command availability 

CLI resource: port

Device makes: HP, Sun, server

Uplogix Local Managers: All 

LMS offerings: Advanced

# Syntax 

```
config service-processor
```

# Usage 

```
[admin@UplogixLM (port1/3)]# config service-processor
Service processor enabled: true
Using dedicated ethernet
IPMI Port: 664
Username: xyz123
Password: ********
Connection Type: auto(none)
Change these? (y/n) [n]:
```

# History 

3.4 - This command was introduced.

# Related commands

- **show service-processor**
