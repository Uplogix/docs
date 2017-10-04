<!-- 5.4 -->

This command clears the system-level alarm that is normally generated when an RSA SecurID hardware authenticator is removed from the system.

This command does not silence the port-level alarm that is generated when the hardware authenticator is removed and the connected device is then unable to authenticate. To silence the port-level alarm, you can:

- Plug the hardware authenticator back into the USB connector
- Suspend the port (this silences the alarm temporarily but does not address the cause)
- Set the port to authenticate by some other means than hardware authentication

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system clear securid
```

# Usage 

```
[admin@UplogixLM]# config system clear securid
Rsa SecurID alarm cleared
```

# History 

3.4 - This command was introduced.

# Related commands 

--
