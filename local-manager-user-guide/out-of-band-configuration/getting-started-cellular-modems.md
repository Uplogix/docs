<!-- 5.4 -->

Before configuring the Local Manager to use a cellular modem, the modem must be unpacked, have a SIM card inserted, and be physically installed in the LM. 

This guide answers the necessary pre-configuration questions chronologically and should be followed as written.

# Which type of modem do I have?

The Uplogix Local Manager supports different types of cellular modems, with two major hardware distinctions (TDMA, CDMA) and two main service providers (AT&T, Verizon).

Your modem should be clearly labeled both on the packaging and the modem itself. 

## HSPA+, 1XRTT, GPRS Modem - 1 Antenna
![HSPA Modem](http://uplogix.com/support/docs/img/hspa_modem_1.jpg)

## LTE Modem - 2 Antennas

![LTE Modem](http://uplogix.com/support/docs/img/lte_modem_1.jpg)

![LTE Modem](http://uplogix.com/support/docs/img/lte_modem_2.jpg)

# Which service provider does my modem require?

The required service provider will typically depend on the cellular technology being used (TDMA vs CDMA). Since these technologies are incompatible, you'll want to make sure you order service from the correct provider.

In the United States, the biggest providers for CDMA are **Verizon** and **Sprint**. For TDMA, you can use **AT&T** and **T-Mobile**. To determine which technology your modem is using, reference the model number on its white sticker.

## HSPA+ Modems

HSPA+ modems are only available on TDMA networks, but they are certified in most countries, so you can use any service provider that supports TDMA such as **AT&T** and **T-Mobile**.

## LTE Modems

**AT&T** LTE modems have a model number of **MTSMC-LAT1-U**.

**Verizon** CDMA modems have a model number of **MTSMC-LVW2-U**.

**European** modems have a model number of **MTSMC-LEU1-U**.

# What kind of service plan should I order?

For most setups, you'll want to purchase a data plan with at least 15MB of data per month. Generally, service plans will allow you to pool the data usage among multiple SIM cards. 

Although the Local Manager will not be using the OOB connection all the time, you should consider the typical bandwidth usage of the heartbeat service.

* Minimal Heartbeat: 4KB approximately every 30 seconds, or 480KB/hr
* Full Heartbeat: approximately 10KB every 30 seconds, or 1.2MB/hr
* CLI Interaction: variable low
* WAN Traffic Failover: variable high, tested as high as 50mbit/s 

If you want to use **SMS-initiated PPP**, you will need both a voice and data plan.

You'll also want to consider what type of network connection and addresses are available. If you have your own IpSec VPN device, you can use the service provider's public internet APN and build a tunnel after the initial connection. Or, if your company has already established an APN with a provider, then you can provision your SIM cards to authenticate to that address range.

# What is an APN anyway?

An Access Point Name (APN) is the name of a gateway between the cellular network and another private or public network, for example, a VPN or the public Internet. It is required to get data from the Local Manager back to the Control Center or User.

It will also be **required** later in the Local Manager configuration as part of the modem's initialization string.

# How do I install the SIM card?

An improperly installed SIM card will prevent the modem from working, so make sure it is installed correctly before installing the modem in the Local Manager.

To install the SIM card, follow the white marking around the SIM card slot on the modem.

<div class='danger' />Modem cards are not hot-swappable. Shut down the Uplogix 5000 using the front panel or with the **shutdown** command from the system resource. For an Uplogix 500, use the **shutdown** command from the CLI.</div>

![LTE Modem](http://uplogix.com/support/docs/img/lte_modem_sim1.jpg)

Note the notched corner on the upper left side of the white marking. This will coincide with the notch on your SIM card. On the slot itself, you'll notice six metal contacts; we need these to make contact with the chip on the SIM card (on reverse side of card shown in Picture.

Slide the card into the slot as shown below and make sure it is secure.

![LTE Modem](http://uplogix.com/support/docs/img/lte_modem_sim2.jpg)
 
# How do  I install the modem card in the Uplogix 500/5000?

Before installing the modem card, **ensure the Local Manager is powered off**. You will need a small Philips screwdriver.

The instructions below apply to both the 500 and 5000 Local Managers

![LTE Modem](http://uplogix.com/support/docs/img/lte_modem_install1.jpg)

**Step 1: **Remove the blank face plate from the front of the 5000 by removing the screws in the upper-right and lower-left corner.

![LTE Modem](http://uplogix.com/support/docs/img/lte_modem_install2.jpg)

Note the gray plastic rails that will hold the modem card and ensure proper alignment with the connector in the back.

![LTE Modem](http://uplogix.com/support/docs/img/lte_modem_install3.jpg)

**Step 2**: Slide the blue part of the modem card partway into the rails.

![LTE Modem](http://uplogix.com/support/docs/img/lte_modem_install4.jpg)

**Step 3: ** Route the gray antenna wires into the free space above the card. Make sure the wires don't get trapped inside the rails or around any edges of the green riser card. 

![LTE Modem](http://uplogix.com/support/docs/img/lte_modem_install5.jpg)

**Step 4: ** Push the modem card into the slot until it stops. It should not take any extra pressure to engage the connector in the back.

![LTE Modem](http://uplogix.com/support/docs/img/lte_modem_install6.jpg)

**Step 5: ** Attach the faceplate to the Local Manager using the two screws from Step 1.

![LTE Modem](http://uplogix.com/support/docs/img/lte_modem_install7.jpg)

**Step 6:** Attach your antenna(s) to the faceplate.

> The **MAIN** antenna connection is **REQUIRED**. The **AUX** connection is optional but recommended of optimal performance. Your antenna(s) may differ from the ones shown in the picture.

![LTE Modem](http://uplogix.com/support/docs/img/lte_modem_install9.jpg)

You may want to wait to attach the antennas until after the Local Manager is racked and installed in its final location.

# What's the best way to mount the antennas?

For best results, position the antennas at right angles and at least two feet apart.

# What do I next?

Now that you've **purchased and activated a SIM card**, **installed the SIM card**, and **installed the modem card**, you're now ready to proceed with the software configuration of the Local Manager.