<!-- 5.4 -->

For the best and most secure experience, Uplogix Local Managers should always run the latest version of LMS. Uplogix generally releases two new versions of software each year, but may also release patches if important bugfixes or security updates are required.

To ensure proper operation of the Local Manager with the Control Center, both need to be running the same minor revision of software. That is, **the first two numbers of the version** need to be the same.

For example, a 5.4.5 Local Manager will work fine with a 5.4.1 Control Center. A 5.3 Local Manager, however, will not synchronize with a 5.4.x Control Center.

# About the Upgrade

Here's what happens when you upgrade a Local Manager:

1. The bin file is downloaded to the Local Manager
2. The bin file is decrypted and verified
3. Upgrade files are unpacked onto the filesystem
4. The Local Manager restarts to perform the upgrade.

The Local Manager will be available until Step 4. During the upgrade, the operating system will be up and responding to pings, but SSH will be unavailable until the upgrade is complete.

# Download Software

Visit your Uplogix Support Site account page at uplogix.com/support/account.

<div class='warning' />An active maintenance contract is required to access the Uplogix Support Site account page and/or download software. If your maintenance contract has expired, please contact Uplogix Support.</div>

Find the section marked *Software Downloads*.

![Support Site Software Downloads](http://uplogix.com/support/docs/img/lm-user-guide/software_downloads.png)

Click the lms.bin link for your desired software version to generate a download link.

![Support Site Download Link](http://uplogix.com/support/docs/img/lm-user-guide/download_ready.png)

Click the link to download the bin file to your desktop.

Files downloaded from the Support Site are automatically tagged with the version number for easy organization. Documentation will refer to the file as an **lms.bin** file, but you will be working with your tagged version, for example, **lms5.4.bin**.

# Upgrading via SCP, FTP, and HTTP

SCP, FTP, and HTTP require the lms.bin file to be staged on an appropriate server. Push the file to an SCP, FTP, or HTTP server.

> The Control Center can be used as an SCP target because of its Linux operation system. Use a program like WinSCP or pscp to transfer the bin file to /home/emsadmin.

<div class='warning' />While possible, please do not use the Uplogix Support Site as an HTTP target if you upgrade a large number of Local Managers.</div>

Log into your Local Manager and use the **config update** command to initiate the upgrade. You will need to specify the IP address or hostname of the target and the path to the file.

For example:

```
config update scp user@198.51.100.172:lms5.4.bin
```

or


```
config update ftp user@198.51.100.172:lms4.7.bin
```

or

```
config update http http://198.51.100.172/lms5.4.bin
```

# Upgrading via the Control Center

To upgrade Local Managers from the Control Center, please refer to *Control Center User Guide*, [Upgrading Local Managers](http://uplogix.com/docs/control-center-user-guide/managing-deployment/upgrading-local-managers).

# Upgrading from a USB flash drive

Flash drives are a useful alternative if the Local Manager isn't on the network or is in a remote location.

## Prepare USB Drive

The flash drive should be formatted with the FAT16 filesystem. If the drive is formatted with FAT32, it must be removed from the Local Manager after it reboots to complete the upgrade.

## Add "upgrade.mnf" File (optional)

If you will be upgrading via the front panel (Uplogix 5000 Local Manager only), you will need a properly configured MNF file in the root of the flash drive.

```
[user@linux EnvoyOS]$ cat upgrade.mnf
ENVOY_BIN=lms5.4.bin
VERSION=5.4.0
```

If you will be upgrading via the command line, you will need to know the exact filename of the upgrade file.

## Add Software Image

Copy the Uplogix LMS software image to the root directory of your flash drive. If using an MNF file, ensure that the filename matches the ENVOY_BIN line exactly.

## Plug in USB Drive

Use a free USB slot on the front of the Local Manager. Allow a few seconds for the system to recognize the new drive.

## USB Upgrade via Front Panel

> An upgrade.mnf file is required for front-panel upgrades.

Press the center button on the keypad to enter the Local Manager menu.

Scroll down and select *Update*.

Verify that *Update to [version]?* message matches intended version.

Scroll left and select *Yes*.

The upgrade will now continue on its own. While the software is transferred to the Local Manager, the LCD will begin displaying status information again. Allow several minutes for the software to be copied over and for the upgrade to begin.

## USB Upgrade via CLI

Log into the Local Manager.

Run **config update usb [filename]**. If the filename is not specified, the appliance will attempt to discover this information via the MNF file.

The Local Manager will then copy the file over, verify it, and begin the upgrade.