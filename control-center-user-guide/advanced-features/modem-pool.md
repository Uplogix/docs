# Configuring a Cisco router as an Uplogix Modem Pool

Configuring Reverse SSH for Modem Access

To configure Reverse SSH for modem access, perform the steps shown in the “SUMMARY STEPS” section below.

In this configuration, reverse SSH is being configured on a modem used for dial-out lines. To get any of the dial-out modems, you can use any SSH client and start a SSH session as shown (in Step 10) to get to the next available modem from the rotary device.



![Uplogix Control Center - SSH Applet Button](http://uplogix.com/support/docs/img/UCC-Modem-Pool.jpg)

SUMMARY STEPS
1.    enable 

2.    configure terminal 

3.    line line-number ending-line-number 

4.    no exec 

5.    login authentication listname 

6.    rotary group 

7.    transport input ssh 

8.    exit 

9.    exit 

10.    ssh -l userid :rotary {number} {ip-address} 


