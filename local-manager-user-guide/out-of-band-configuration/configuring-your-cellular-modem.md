<!-- 5.4 -->

Before following the steps in this guide, ensure you have already completed [Getting Started with Cellular Modems](http://uplogix.com/docs/local-manager-user-guide/out-of-band-configuration/getting-started-cellular-modems)

This article describes the configuration of a Local Manager with a cellular modem.

# Resource Configuration

Log into the Local Manager and access the modem resource using the **modem** command. This resource must be configured with the **config init** command before it can use the cellular modem. When prompted for make, use **cellular**.

```
[admin@U500]# modem
embedded

[admin@U500 (modem)]# config init
 This device has already been initialized.
Would you like to reinitialize it? (y/n): y
--- Enter New Values ---
description: []: AT&T LTE Modem
make: [embedded]: cellular
serial bit rate [38400]:
serial data bit [8]:
serial parity [none]: 
serial stop bit [1]:
serial flow control [none]:
Do you want to commit these changes? (y/n): y
Testing login will take a few moments...
Login successful; credentials are valid.
```
    
**Note:** Some Verizon CDMA modems use a baud rate of 115200

## Testing Connectivity

Use the **terminal** command to ensure a good connection with the modem. After establishing a console session, run a few AT commands like **ATZ** or **AT+CSQ**.

```
[admin@U500 (modem)]# terminal
Press ~[ENTER] to exit
Connecting ...
Console session started.
atz
OK
at+csq
+CSQ: 21,0
OK
```

## Configure APN

<div class='ucc' />Inventory > Local Manager > Out-of-Band > Modem > Cellular</div>

An APN is required to use PPP and will be specified by your cellular service provider. To configure the APN(s) on a modem, open a **terminal** session and use the **AT+CGDCONT** command. You can also set the APN from the Control Center.

For **Verizon** modems:

```
AT+CGDCONT=1,"IPV4V6","vzwims"
AT+CGDCONT=2,"IPV4V6","vzwadmin"
AT+CGDCONT=3,"IPV4V6","provider.apn.com"
```

For **AT&T** modems:

```
AT+CGDCONT=1,"IP","provider.apn.com" 
```

For both types of modems, note that **provider.apn.com** will need to be replaced with your provider’s custom APN designation. You will be able to get this information from your cell provider account representative.

## Configure Initialization String

The initialization string can be used to designate the APN of your service provider for use with PPP. However, this method is no longer necessary/recommended as of LMS version 5.4. See the previous **Configure APN** section if you are running 5.4 or later.

Use the **config answer** command to add an initialization string.

For 5.4 and later:

```
[admin@U500 (modem)]# config answer
[config answer]# init "" ATZ
```

For 5.3 and prior:

```
[admin@U500 (modem)]# config answer
[config answer]# init "" ATZ OK AT+CGDCONT=1,\"IP\",\"provider.apn.com\"
```

**Note:** The quotes used in the AT+CGDCONT command require the “\” escape character.

**Note:** CDMA modems do not require the APN designation command “AT+CGDCONT” for proper operation. If you are using a CDMA modem, please use this alternate init string:

```
[config answer]# init "" ATZ
```

Verify your settings with the **show answer** command.

```
[admin@U500 (modem)]# show answer
disabled
SLV suspended when PPP on
init "" ATZ OK AT+CGDCONT=1,\"IP\",\"provider.apn.com\"
answer after 3 rings
number 5125551212
domain text.provider.net
```

Please note that **provider.apn.com** will need to be replaced with your provider’s custom APN designation. You will be able to get this information from your cell provider account representative. In addition **text.provider.net** will need to be substituted for the text message domain used by your provider
    
### Initialization Strings Explained

The initialization strings for cellular modems are more complex than typical V.92 modems. Below is a brief explanation of each element of the cellular-specific init string.

<table>
<tr><td><strong>ATZ</strong></td>
<td>Restores the default configuration of the modem.</td></tr>
<tr><td><strong>AT+CGDCONT=1</strong></td><td>
Defines the use of PDP (packet Data Protocol) context, will be followed by connectivity type and APN.</td></tr>
<tr><td><strong>“IP”</strong></td>
<td>Sets the modem to use IP connectivity.</td></tr>
<tr><td><strong>“provider.apn.com”</strong></td>
<td>The APN designation set up by your provider</td></tr></table>

## Configure Number and Domain for SMS-initiated PPP

If you will be using [SMS-initiated PPP](https://uplogix.com/docs/local-manager-user-guide/out-of-band-configuration/sms-initiated-ppp), set the number and domain using the **config answer** command.

```
[admin@U500 (modem)]# config answer
[config answer]# number 5125551212
[config answer]# domain text.provider.net
[config answer]# exit
```

## Set Modem Frequency (if required)

The modem’s default quad-band mode may not work outside of North America. You may need to set the frequency to the appropriate mono-band to use the modem in other locations.

To check the current band: **AT+WMBS?**

To restore the modem to the default North America settings, use: **AT+WMBS=7,1**

The syntax of the command is **AT+WMBS=(band),(param)**

**Supported Bands:**

<table><tr><td><strong>0</strong></td><td>mono-band 850 MHz</td></tr><tr><td><strong>1</strong></td><td>mono-band 900 extended MHz (900E)</td></tr><tr><td><strong>2</strong></td><td>mono-band 1800 MHz</td></tr><tr><td><strong>3</strong></td><td>mono-band 1900 MHz</td></tr><tr><td><strong>4</strong></td><td>dual-band 850/1900 MHz</td></tr><tr><td><strong>5</strong></td><td>dual-band 900E / 1800 MHz</td></tr><tr><td><strong>6</strong></td><td>dual-band 900E / 1900 MHz</td></tr><tr><td><strong>7</strong></td><td>quad-band 850/900E/1800/1900 MHz</td></tr></table>

**Parameters:**

<table><tr><td><strong>0</strong></td><td><strong>Default</strong>. The wireless modem must be reset to start using the specified band. </td></tr><tr><td><strong>1</strong></td><td>The change is effective immediately. The GSM stack is restarted on the specified band.</td></tr></table>

## Check Network Registration

To determine if the modem is properly connecting to the cellular network, use the AT+CREG? command. The command will return one of the following responses:

- 0,0 – The modem is not registered on any network
- 0,1 – The modem is registered on the home network
- 0,2 – The modem is not connected to the network
- 0,3 – The modem is not connected to the network
- 0,5 – The modem is registered on a network and it is roaming

For proper operation, **AT+CREG?** should respond with 0,1.

##  Configure PPP Settings

Before the modem can connect to the cellular network, a phone number must be specified.

**Note:** If the LM fails to establish a PPP connection, try populating the username and password fields with arbitrary values. Some providers require a username and password to be sent, even if no authentication is taking place.

    [admin@U500 (modem)]# config ppp
    --- Existing Values ---
    Phone Number:
    User Name:
    Password: ********
    Use Static IP Address: false
    Change these? (y/n) [n]: y
    --- Enter New Values ---
    Phone Number:[]: *99***1#
    User Name: []: username
    Password []: ********
    Confirm Password: ********
    Use Static IP Address: (y/n) [n]:
    Do you want to commit these changes? (y/n): y

**Note:** For CDMA and EV-DO modems, use **#777** as the phone number. Consult your service provider for more information.

## Configure SMS monitor for SMS-initiated PPP

The Uplogix Local Manager must be told to monitor, periodically, the SIM card for incoming SMS text messages (sent by the Control Center) to determine if it should establish a PPPconnection. This can be accomplished with a modem monitor and an included rule named smsPppOn.

    [admin@U500 (modem)]# config monitor sms smsPppOn
    Job was scheduled 0: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor sms none smsPppOn 30

**Note:** SMS-initiated PPP is not currently supported for Verizon CDMA modems.

### Testing SMS/PPP from Control Center

To initiate a PPP connection from the Control Center, navigate to the Local Manager summary page and click on **Schedule Task**. From the drop-down task menu, select SMS Message and click Next. As of LMS 5.3, the only available option is **PPP On**. Click Next to send the SMS message.

### Error Messages

**Failed to send SMS message.** – SMS messages are sent using an e-mail to SMS gateway. To send messages, the Control Center must be properly configured to send e-mail. Check the SMTP settings under Administration -> Server Settings -> Mail Settings.

# Troubleshooting

The following commands may be useful in the troubleshooting of cellular modems. For more information about these commands, please consult the Multitech Support Portal.

**AT+CCID**

Returns the modem’s CCID number.

**AT+CFUN**

Selects the mobile station’s level of functionality.

	AT+CFUN?	Query current functionality level
	AT+CFUN=0	Set minimum functionality; run IMSI DETACH procedure
	AT+CFUN=1	Set full functionality; restart GSM stack

**AT+CGSN**

Returns the modem’s IMEI number.

**AT+CMGL**

Queries the modem for SMS messages.

	AT+CMGL=0	Show unread messages
	AT+CMGL=4	Show all messages
	AT+CMGD=n	Delete message n

**AT+CNUM**

Returns the modem’s phone number. Should match what is configured in config answer.

**AT+COPS**

Selects a Public Land Mobile Network (PLMN) acquisition method. 

	AT+COPS?	Queries for current PLMN
	AT+COPS=?	Queries for PLMN list
	AT+COPS=0	Set automatic mode (default)
	AT+COPS=1	Set manual mode
	AT+COPS=2	Deregister
	AT+COPS=4	Set manual mode with fallback to automatic mode

**AT+CPOF**

Stops the GSM software stack as well as the hardware layer or modem activity.

	AT+CPOF	Stop the GSM stack
	AT+CPOF=1	Stop the modem

**ATD**

Dials a phone number. Useful for testing dial-out capabilities.

**ATE1**

Turns on local echo.

**AT+IPR**

Sets the baud rate.

	AT+IPR=<baud rate>	Set modem baud rate.

**AT#RESET**

Resets the modem.

	AT#RESET=0	Reset the GSM stack and internal modem
	AT#RESET=1	Reset the internal modem only

# Cellular Native Ruleset Monitoring

The following rules read and report cellular signal strength and reboot the modem if it returns an error.

The ruleset can be configured on the Uplogix modem resource with the command **config monitor modem CellularNative.**

    conf rule no CellularSignalQuality0
    conf rule CellularSignalQuality0
    description Cellular Signal QualityAt0
    action alarm -a "Cellular Signal Quality below minimum"
    action writeStatus Cell % is 0
    conditions
    modem.response matches "CSQ:\s0,"
    exit
    exit
    
    conf rule no CellularSignalQuality1
    conf rule CellularSignalQuality1
    description Cellular Signal QualityAt1
    action alarm -a "Cellular Signal Quality below minimum"
    action writeStatus Cell % is 1
    conditions
    modem.response matches "CSQ\s1,"
    exit
    exit
    
    conf rule no CellularSignalQuality2
    conf rule CellularSignalQuality2
    description Cellular Signal QualityAt2
    action alarm -a "Cellular Signal Quality below minimum"
    action writeStatus Cell % is 2
    conditions
    modem.response matches "CSQ:\s2,"
    exit
    exit
    
    conf rule no CellularSignalQuality3
    conf rule CellularSignalQuality3
    description Cellular Signal QualityAt3
    action alarm -a "Cellular Signal Quality below minimum"
    action writeStatus Cell % is 3
    conditions
    modem.response matches "CSQ:\s3,"
    exit
    exit
    
    conf rule no CellularSignalQuality4
    conf rule CellularSignalQuality4
    description Cellular Signal QualityAt4
    action alarm -a "Cellular Signal Quality below minimum"
    action writeStatus Cell % is 4
    conditions
    modem.response matches "CSQ:\s4,"
    exit
    exit
    
    conf rule no CellularSignalQuality5
    conf rule CellularSignalQuality5
    description Cellular Signal QualityAt5
    action alarm -a "Cellular Signal Quality below minimum"
    action writeStatus Cell % is 5
    conditions
    modem.response matches "CSQ:\s5,"
    exit
    exit
    
    conf rule no CellularSignalQuality6
    conf rule CellularSignalQuality6
    description Cellular Signal QualityAt6
    action writeStatus Cell % is 6
    conditions
    modem.response matches "CSQ:\s6,"
    exit
    exit
    
    
    conf rule no CellularSignalQuality7
    conf rule CellularSignalQuality7
    description Cellular Signal QualityAt7
    action writeStatus Cell % is 7
    conditions
    modem.response matches "CSQ:\s7,"
    exit
    exit
    
    conf rule no CellularSignalQuality8
    conf rule CellularSignalQuality8
    description Cellular Signal QualityAt8
    action writeStatus Cell % is 8
    conditions
    modem.response matches "CSQ:\s8,"
    exit
    exit
    
    conf rule no CellularSignalQuality9
    conf rule CellularSignalQuality9
    description Cellular Signal QualityAt9
    action writeStatus Cell % is 9
    conditions
    modem.response matches "CSQ:\s9,"
    exit
    exit
    
    conf rule no CellularSignalQuality10
    conf rule CellularSignalQuality10
    description Cellular Signal QualityAt10
    action writeStatus Cell % is 10
    conditions
    modem.response matches "CSQ:\s10,"
    exit
    exit
    
    conf rule no CellularSignalQuality11
    conf rule CellularSignalQuality11
    description Cellular Signal QualityAt11
    action writeStatus Cell % is 11
    conditions
    modem.response matches "CSQ:\s11,"
    exit
    exit
    
    conf rule no CellularSignalQuality12
    conf rule CellularSignalQuality12
    description Cellular Signal QualityAt12
    action writeStatus Cell % is 12
    conditions
    modem.response matches "CSQ:\s12,"
    exit
    exit
    
    conf rule no CellularSignalQuality13
    conf rule CellularSignalQuality13
    description Cellular Signal QualityAt13
    action writeStatus Cell % is 13
    conditions
    modem.response matches "CSQ:\s13,"
    exit
    exit
    
    conf rule no CellularSignalQuality14
    conf rule CellularSignalQuality14
    description Cellular Signal QualityAt14
    action writeStatus Cell % is 14
    conditions
    modem.response matches "CSQ:\s14,"
    exit
    exit
    
    conf rule no CellularSignalQuality15
    conf rule CellularSignalQuality15
    description Cellular Signal QualityAt15
    action writeStatus Cell % is 15
    conditions
    modem.response matches "CSQ:\s15,"
    exit
    exit
    
    conf rule no CellularSignalQuality16
    conf rule CellularSignalQuality16
    description Cellular Signal QualityAt16
    action writeStatus Cell % is 16
    conditions
    modem.response matches "CSQ:\s16,"
    exit
    exit
    
    conf rule no CellularSignalQuality17
    conf rule CellularSignalQuality17
    description Cellular Signal QualityAt17
    action writeStatus Cell % is 17
    conditions
    modem.response matches "CSQ:\s17,"
    exit
    exit
    
    conf rule no CellularSignalQuality18
    conf rule CellularSignalQuality18
    description Cellular Signal QualityAt18
    action writeStatus Cell % is 18
    conditions
    modem.response matches "CSQ:\s18,"
    exit
    exit
    
    conf rule no CellularSignalQuality19
    conf rule CellularSignalQuality19
    description Cellular Signal QualityAt19
    action writeStatus Cell % is 19
    conditions
    modem.response matches "CSQ:\s19,"
    exit
    exit
    
    conf rule no CellularSignalQuality20
    conf rule CellularSignalQuality20
    description Cellular Signal QualityAt20
    action writeStatus Cell % is 20
    conditions
    modem.response matches "CSQ:\s20,"
    exit
    exit
    
    conf rule no CellularSignalQuality21
    conf rule CellularSignalQuality21
    description Cellular Signal QualityAt21
    action writeStatus Cell % is 21
    conditions
    modem.response matches "CSQ:\s21,"
    exit
    exit
    
    conf rule no CellularSignalQuality22
    conf rule CellularSignalQuality22
    description Cellular Signal QualityAt22
    action writeStatus Cell % is 22
    conditions
    modem.response matches "CSQ:\s22,"
    exit
    exit
    
    conf rule no CellularSignalQuality23
    conf rule CellularSignalQuality23
    description Cellular Signal QualityAt23
    action writeStatus Cell % is 23
    conditions
    modem.response matches "CSQ:\s23,"
    exit
    exit
    
    conf rule no CellularSignalQuality24
    conf rule CellularSignalQuality24
    description Cellular Signal QualityAt24
    action writeStatus Cell % is 24
    conditions
    modem.response matches "CSQ:\s24,"
    exit
    exit
    
    conf rule no CellularSignalQuality25
    conf rule CellularSignalQuality25
    description Cellular Signal QualityAt25
    action writeStatus Cell % is 25
    conditions
    modem.response matches "CSQ:\s25,"
    exit
    exit
    
    conf rule no CellularSignalQualityAbove25
    conf rule CellularSignalQualityAbove25
    description Cellular Signal QualityAt25
    action alarm -a "Cellular modem RSSI Above 25"
    action writeStatus Cell % is > 25
    conditions
    modem.response matches "CSQ:\s(?:(?:[2][5-9])|(?:[3-9][0-9])),"
    exit
    exit
    
    conf rule no CellularErrorMessage
    conf rule CellularErrorMessage
    description Cellular Error Message
    action powerCycle
    action alarm -a "Cellular modem returning errors"
    conditions
    modem.response matches "ERROR":2i AND
    NOT has-run powerCycle :5m
    exit
    exit
    
    config rule CellularNonResponsive
    action alarm -a "the modem has become unusable for 5 minutes, powercycling"
    action event GENERIC -a "the modem has become unusable for 5 minutes,  powercycling"
    action powerCycle
    action writeStatus no response powercycling
    conditions
    modem.response equals FAILED_TO_GET_RESPONSE :10i AND
    NOT has-run powerCycle :5m
    exit
    exit
    
    conf ruleset no CellularNative
    conf ruleset CellularNative
    description Cellular Rules for Multitech GPRS Cell Modems
    rules
    CellularNonResponsive, CellularErrorMessage, CellularSignalQuality25, CellularSignalQuality24, CellularSignalQuality23, CellularSignalQuality22, CellularSignalQuality21, CellularSignalQuality20, CellularSignalQuality19, CellularSignalQuality18, CellularSignalQuality17, CellularSignalQuality16, CellularSignalQuality15, CellularSignalQuality14, CellularSignalQuality13, CellularSignalQuality12, CellularSignalQuality11, CellularSignalQuality10, CellularSignalQuality9, CellularSignalQuality8, CellularSignalQuality7, CellularSignalQuality6, CellularSignalQuality5, CellularSignalQuality4, CellularSignalQuality3, CellularSignalQuality2, CellularSignalQuality1, CellularSignalQuality0, CellularSignalQualityAbove25
    exit
    exit

# How to Enable

To use the CellularNative ruleset, apply it to a monitor on the modem resource.

```
[admin@UplogixLM (modem)]# config monitor modem CellularNative :30
```
