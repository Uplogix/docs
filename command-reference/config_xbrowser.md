<!-- 5.4 -->

Allows you to change the xbrowser configuration for this device. 

# Command availability 

CLI resource: port

Device makes: server

Uplogix Local Managers: All except Uplogix 430

LMS offerings: Advanced

# Syntax 

```
config xbrowser
```

# Usage 

```
[admin@UplogixLM (port1/3)]# config xbrowser
--- Existing  Values ---
Browser port: 443
Browser protocol: https
Change these? (y/n) [n]:
```

Browser protocol may be either http or https.

# History 

3.5 - This command was introduced.

# Related commands

- **clear xbrowser**
- **show xbrowser**
- **xbrowser**