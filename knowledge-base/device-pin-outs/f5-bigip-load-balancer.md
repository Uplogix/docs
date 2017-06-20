To connect the applianceto a BigIP, you will need to modify a standard DB-9 adapter.

The typical pinout for a standard DB-9 to RJ-45 is:

|RJ-45 Pin|Color|DB-9 Pin|
|---:|:--:|:---|
|  1|	  blue|	  7|
|  2|	  orange|  4|
|  3|	  black|	  3|
|  4|	  green|	  5|
|  5|	  red|	  5|
|  6|	  yellow|	  2|
|  7|	  brown|	  6|
|  8|	  white|	  8|
 

The BigIP machine is looking for carrier detect on pin 1 of the DB-9. Since this pin is empty in the normal configuration, it needs to be wired into an electrical signal so that the BigIP will see carrier detect and provide the login prompt.

You can modify this adapter by removing a wire from an unused DB-9 female adapter.  Attach the female side to slot 1 of the DB-9 side.  Strip the other end of the wire and combine it with the orange wire in slot 4.

![Big IP Adapter](http://uplogix.com/support/docs/img/kb-lm/f5-big-ip.jpg)

The typical serial settings for an F5 connection are 9600, 8 N 1, no flow control.  Also, configuration on the BigIP may affect communications through the serial port.