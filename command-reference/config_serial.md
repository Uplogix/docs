<!-- 5.4 -->

Interactive command to specify serial console connection settings for a network device. To configure the Uplogix system's management console port, use the **config system serial** command.

# Command availability 

CLI resource: port, powercontrol, modem

Device makes: All

Modem: All

Power controllers: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
config serial
```

This command is available from terminal pass-through as **~s**

# Usage 

The option to test the new settings is presented before the commit dialog.

The test option is not presented if called using **~s**.

```
[admin@UplogixLM (port1/1)]# config serial
Serial Bit Rate: 9,600
Serial Data Bit: 8
Serial Parity: none
Serial Stop Bit: 1
Serial Flow Control: none
DSR: false
CTS: false
RX : 0
TX : 0
Overrun Errors: 0
Parity Errors: 0
Breaks: 0
Change these? (y/n) [n]: y
--- Enter New Values ---
serial bit rate [9600]:
serial data bit [8]:
serial parity [none]:
serial stop bit [1]:
serial flow control [none]:
Do you want to commit these changes? (y/n): 
```

# History 

--

# Related commands 

**config system serial**

**show serial**

**show system serial**
