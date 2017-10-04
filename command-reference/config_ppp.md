<!-- 5.4 -->

Interactive command to configure the point-to-point protocol (PPP) server information.

# Command availability 

CLI resource: modem

Modem: All

Uplogix system: All

LMS offerings: All

# Syntax 

```
config ppp
```

# Usage 

```
[admin@UplogixLM (modem)]# config ppp
--- Existing Values ---
Phone Number:
User Name:
Password: ********
Use Static IP Address: false
Change these? (y/n) [n]: y
```

To use a hardware authenticator, set the password as [PIN]$(SECURID)where [PIN] is an optional password of up to 8 characters and the rest is entered exactly as shown. The password is case-sensitive. 

To set a static IP address for an Iridium modem, answer y to the prompt Use Static IP Address? and enter the desired IP address when prompted.

If the ppp server requires Challenge Handshake Authentication Protocol (CHAP) you must enter a username and password.

# In the Uplogix web interface

**Inventory > group page > Local Manager configuration button  > PPP** - specific to this inventory group

**Inventory > expanded system page > Configuration tab > PPP **- specific to this system

# History 

3.0 – Revised to support RSA® SecurID® hardware authentication.

# Related commands 

**show ppp**

**config system pulse**
