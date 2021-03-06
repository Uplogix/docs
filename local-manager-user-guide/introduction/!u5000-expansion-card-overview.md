The Uplogix 5000 may be customized by adding additional ports through the two modular expansion bays. The leftmost bay is designated slot 3 in the system and the rightmost bay as slot 2. Each expansion bay can be used to add 4, 8, or 16 serial ports or 8 dedicated Ethernet ports. Dedicated Ethernet ports are paired with serial ports to enhance management capabilities for some devices.

# Option Cards

## Sample 8 Port Serial Card

![](http://uplogix.com/support/docs/img/installing-a-local-manager/image019.png)

## Sample 16 Port Serial Card

![](http://uplogix.com/support/docs/img/installing-a-local-manager/image020.png)

The 16 Port Serial Card is used with 8-connector fan-out cables that have a v.68M connector for attaching to the card and 8 RJ45 connectors pinned as DCE. Two of these cables can be used to connect the card to up to 16 devices. 

## Sample 8-Connector Fan-out Cable

![](http://uplogix.com/support/docs/img/installing-a-local-manager/fan-out-cable_with-stickers.png)

The fan-out cables come with a set of stickers for labeling. Wrap the stickers on the ferrite bead near the RJ45 connectors as shown above. The stickers allow you to label the cables with both slot and port numbers for easier identification. 

## Sample 8 Port Dedicated Ethernet Card

![](http://uplogix.com/support/docs/img/installing-a-local-manager/image021.png)

# Ethernet Expansion Card Port Mapping

Dedicated Ethernet ports are used to make a direct Ethernet connection between the Local Manager and a managed device. For instance, the Local Manager can use Ethernet to move configuration and software image files back and forth between it and its managed devices. Dedicated Ethernet ports are always paired with serial ports in the system. The placement of an Ethernet expansion card in the system will determine which serial ports map to its Ethernet ports.

## Configuration A: One Ethernet expansion card, one serial expansion card

When an 8 or 16 port serial expansion card is installed in the right expansion bay (slot 2) and an 8 port Ethernet expansion card is installed in the left expansion bay (slot 3), the 8 dedicated Ethernet ports in slot 3 are paired with the first 8 serial ports (ports 2/1 to 2/8) in slot 2.

![](http://uplogix.com/support/docs/img/installing-a-local-manager/image022.png)

## Configuration B: One serial port expansion card, one Ethernet expansion card

When an 8 port Ethernet expansion card is installed in the right expansion bay (slot 2) and an 8 or 16 port serial expansion card is installed in the left expansion bay (slot 3), the first four dedicated Ethernet ports are paired with the first four fixed serial ports (ports 1/1 thru 1/4). The remaining Ethernet ports (ports 5-8) are paired with the first four serial ports on the serial port expansion card (ports 3/1 to 3/4).

![](http://uplogix.com/support/docs/img/installing-a-local-manager/image023.png)

## Configuration C: One Ethernet expansion card, no serial expansion card

When an 8 port Ethernet expansion card is installed in the right expansion bay (slot 2), the first four Ethernet ports are paired with the first four fixed serial ports (ports 1/1 to 1/4). The remaining fixed serial port (port 1/5) is not paired with a dedicated Ethernet port.

![](http://uplogix.com/support/docs/img/installing-a-local-manager/image024.png)