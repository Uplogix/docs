<!-- 5.5 -->

This functionality allows you to dial into Local Managers through an Irridium modem without

### Method 1: Telnet directly into the RUDICS via PuTTY:


Open PuTTY to display the configuration window. Enter the IP address or hostname of the RUDICS router and select 'Telnet' as the connection type. Available ports are **2663** through **2667**.

![Putty - IP and Tunnels](http://uplogix.com/support/docs/img/putty-rudics-telnet3.jpg)

Once you have successfully connected, you should be able to issue modem commands.

### Method 2: Telnet to the RUDICS router via the UCC


SSh to the UCC and [become root](https://uplogix.com/docs/control-center-user-guide/managing-the-control-center "Becoming Root").

```
login as: emsadmin
emsadmin@UplogixUCC's password:
Last login: Mon Jun 18 16:20:28 2018 from 192.34.24.11
[emsadmin@UplogixUCC ~]$ sudo su -
[sudo] password for emsadmin:
[root@UplogixUCCl ~]# 
```
Telnet to the RUDICS router 
 
```
[root@vUCC-Eval ~]# telnet rudics.hostname.com 2663

Entering character mode
Escape character is '^]'.
```
## Prepare the session by setting the serial settings
 
Once you are connected to RUDICS, issue the commands **ATZ**, **ats29=8**, and **ats57=9660**, allowing the modem to return 'OK.'
 
```
ATZ
OK
ats29=8
OK
ats57=9660
OK

```

## Dial into the Local Manager
The dial command is **atdi** and the phone number with no spaces.
```
atdi00881693144440
```

