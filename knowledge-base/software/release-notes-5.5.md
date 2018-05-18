<!-- 5.5 -->

Uplogix, Inc. is pleased to announce the release of version 5.5 software for the Uplogix Local Manager and the Uplogix Control Center.

The following software features, improvements, and fixes have been made in both the Local Manager and the Control Center software.

> This document covers LMS version 5.5 and all subsequent patch releases. Changes made in patch releases are marked with the version number.

<div class='warning' />This software will not run on EOL Local Managers, including the Uplogix 400, 430, and 3200. For more information, please contact Uplogix Support.</div>

# Uplogix Local Manager

## New Features and Improvements

### New Feature: IKEv2 VPN Support

IKEv2 addresses a number of shortcomings in IKEv1. The Local Manager utilizes certificates to authenticate to VPN servers like Cisco ASA, IOS, and pfSense/strongSwan.

### Improvement: Operating System

The operating system of the Local Manager has been rebuilt to use the latest embedded distribution technology.  The LMOS binary images are now 56MB, half the size of the previous release. The virtual Local Manager now includes open-vm-tools.

### Other Changes and Issues Addressed in This Release
 
* Made multiple Cisco driver speed and reliability improvements for pushing or pulling an OS or config.
* Added TLS 1.2 support with elliptical curve Diffie Hellman.
* TLS no longer supports traditional Diffie Hellman.
* FIPS mode no longer supports 3DES.
* The maximum length of the Local Manager hostname was increased from 22 to 63 characters.
* Updated APC driver to work with AOS v6.x.  Version '6' must be specified when initializing the port.
* Added new option to use DNS when provided by your PPP server.
* Local Manager no longer will get stuck on boot if Ethernet cable is accidentally plugged into console port.
* Improved automatic configuration of Verizon LTE modems.
* Improved support for large config and OS files on the Local Manager.
* Improved date consistency in 'Change' reports.
* Improved login responsiveness after a reboot.
* Addressed many Common Vulnerabilities and Exposures (CVEs). Consult the [CVE Database](https://uplogix.com/docs/cve) for more information.

## Known Issues in This Release

* Version 5.5 only supports the 500, 5000, and virtual Local Manager platforms.  Previous EOL models may continue to minimally heartbeat to the Control Center.

# Uplogix Control Center (UCC)

## New Features and Improvements

### New Feature: IKEv2 VPN Support

IKEv2 can be configured from the Control Center.  Previously, server and CA certificates could only be managed in FIPS mode.  Now, they can be managed at the inventory group and Local Manager level regardless of FIPS mode to configure IKEv2 certificates for VPN servers.

### New Feature: Schedule 'Pull OS' and 'Pull Config'

Tasks 'pull os' and 'pull config' can now be scheduled from a port or a filter.

### Improvement: Better Monitoring and Debug Tools

The Control Center now shows a warning message under the 'Administration' tab if database backups have not run in the last 48 hours.  A warning message will also be shown if any disk partition exceeds 90% usage.  Anonymous usage statistics can now be easily collected and submitted to Uplogix under a new page called 'Support Tools'.  At this time, statistics are **not** automatically sent to Uplogix.  Report subscriptions can now be tested from the 'Support Tools' page as well.

### Other Changes and Issues Addressed in This Release

* Login banner now supports preformatted text.
* Login banner also supports replacement tokens for build information.
* Improved log management to prevent HA (standby) environments from filling the /usr partition.
* Added TLS 1.2 support with elliptical curve Diffie Hellman.
* Dial-in now supports ECDHE_RSA.
* Fixed a memory issue when running large reports.
* Improved performance of the heartbeat protocol.
* Improved performance of the 'Inventory' page.
* Added IPT SLV reports that can be run from the inventory or at a system level.
* Addressed many Common Vulnerabilities and Exposures (CVEs). Consult the [CVE Database](https://uplogix.com/docs/cve) for more information.

## Known Issues in This Release

* Java applications launched from IE 11 on Windows 10 require 32-bit Java.  This affects all Java applications including the Uplogix SSH and Dial-in applications.  Oracle released an article about this issue https://java.com/en/download/faq/java_win64bit.xml.