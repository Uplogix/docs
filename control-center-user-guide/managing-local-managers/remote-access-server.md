<!-- 5.4 -->

<div class='ucc' />Inventory > Local Manager Summary > Out-of-Band > Modem</div>

# Overview

This functionality allows users to connect to a modem pool (or remote access server) to dial into Local Managers.

Requirements for using this capability are:

* The Local Manager uses a circuit switched modem such as V.92 or Iridium.
* The Local Manager has been configured to accept incoming calls, and a list of permitted source phone numbers has been defined. These settings are configured with the **config answer** command.

In the example below, a Cisco router is configured as a Remote Access Server (RAS) for the Dial Applet to connect to the Local Manager. From the Local Manager's Out-of-Band configuration menu, select *Modem* and configure settings under the *Modem Pool* section.

* **Protocol** - choose telnet or SSH. Select SSH will enable authentication fields.
* **Host** - IP address or DNS Name of the RAS. 
* **Port Range** - Port range assigned by host for remote access, or the ports on the access server that map to the modems.
* **Username, Password** - Required if using SSH as the connection protocol
* **Allowed SSH Fingerprints** - Add the RAS' SSH fingerprint to protect against IP spoofing.
* **Phone Number** - Enter the command for dialing (ATDI/ATDT/ATD) and the phone number with no spaces.
* **Init String** - Enter an optional initialization string with no spaces.
 
![Uplogix Control Center - SSH Applet Button](http://uplogix.com/support/docs/img/UCC-Modem-Pool.jpg)

Once the access server information has been configured (in the Remote Access Server section), a blue Dial button appears in the Control Center. Click the Dial button to connect to the Local Manager via out-of-band, circuit switched phone number.

![Uplogix Control Center - Modem Pool](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-dial-button.png)
  
The Control Center Dial applet connects to the modem server with the information pre-programmed in the RAS section of the Local Manager Modem configuration.

## Configuring a Cisco Router as an Uplogix Modem Pool


To configure a Cisco router as an Uplogix modem pool, connect a modem to the AUX port (or NME-16A multiport card) on the router.

### Configure Reverse SSH for Modem Access

In this configuration, reverse SSH is being configured on a modem used for dial-out lines. To get any of the dial-out modems, you can use any SSH client and start a SSH session as to get to the next available modem from the rotary device.


To configure Reverse SSH for modem access, terminal into the Cisco router and enter the following commands: 

```
1. enable 
2. configure terminal 
3. line {line-number} {ending-line-number} 
4. no exec 
5. login authentication {listname} 
6. rotary {group} 
7. transport input ssh 
8. exit 
9. exit 
10. ssh -l {userid} :rotary {number} {ip-address} 

```