# Overview

This guide focuses on the Uplogix software-based Service Level Verification (SLV) management module. When licensed for each Local Manager, the SLV module ensures consistent, high levels of IT service by synthetically measuring the performance of critical network services and applications from the end-user’s perspective and comparing the results to drive automation decisions.

You can use SLV to execute Voice over IP (VoIP) calls, web transactions, and TCP SYN/ACK handshakes to verify end-to-end network functionality.

This topic focuses on the activation, configuration, and usage of SLV from the Control Center. To use SLV from the Local Manager CLI, see [Using Service Level Verification](#).

# Installing an SLV License

Service Level Verification is an optional, add-on feature available for purchase from Uplogix. Contact your account executive or [support@uplogix.com](mailto:support@uplogix.com) for more information.

Once you have purchased a license, you will need to install it on the Control Center.

<div class='ucc' />Administration > Licenses</div>

![UCC Licenses Page](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-administration-licenses.png)

Click *Add* and paste in the entire contents of the license. 

![UCC Licenses Page - Add a License](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-administration-licenses-add.png)

Click *Save* to return to the Licenses page. If the *Choose Systems* button was previously gray, it should be enabled now.

![UCC Licenses Page - License Installed](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-administration-licenses-installed.png)

# Assigning Licenses

SLV is licensed on a per-Local Manager basis, so it is necessary to specify which Local Managers in your deployment should be enabled with SLV.

Click the *Choose Systems* button from the Licenses page to view a list of your Local Managers.

![UCC Licenses Page - Choose Systems](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-administration-licenses-choose-systems.png)

Local Managers with SLV enabled will have a checked box next to them. To enable SLV on a new system, check the box and click *Save*. The number of used and available SLV licenses is displayed for reference. If you have more Local Managers than SLV licenses, you can move a license to a different system by unchecking one box and checking another.

Once you click *Save*, allow up to 30 seconds (default heartbeat interval) for the license to be synchronized with the Local Manager.

# 

