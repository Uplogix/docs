<!-- 5.5 -->

This document contains instructions for using vSphere to deploy a virtual Uplogix Control Center (vUCC) to a VMware server.  Note: newer versions of VMware ESXi (v6+) no longer support all features of vSphere, but they still work for deploying our image.  You may use the newer HTML5 application to deploy the vUCC.  Requirements and steps are almost identical.

Prepare to have available disk (see [Requirements](#requirements)), two IP addresses on the same network with netmask and gateway, NTP server, and an optional DNS server.  You will also need to have downloaded the vUCC OVA file from the Uplogix Support Site.
 
# Requirements

* VMware host running ESX/ESXi version 4.1 or higher (Virtual Machine Version 7)
* Storage, memory, and CPUs appropriate for your deployment:

| Deployment Size | Storage | Memory | CPUs (2+ GHz)
|--|--|--|--| 
| >1000 Local Managers | 825 GB thick (SSD)	| 8 GB | 8 cores
| 250-999 Local Managers | ~650 GB thin (SAS/SSD) | 8 GB | 8 cores
|100-249 Local Managers	| ~550 GB thin (SAS/SSD) | 4 GB* / 8 GB default | 4 cores
|1-99 Local Managers | ~450 GB thin (SAS/SSD) | 4 GB* / 8 GB default | 2 cores
| Evaluation vUCC (<10 LMs) | ~65 GB thin (SATA) | 1 GB* / 8 GB default | 2 cores

*Requires vUCC application RAM settings to be adjusted - see [Adjusting Memory](#adjusting-memory)

* The OVA file is about 6GB that expands to 430GB when deployed with thin provisioning.  The maximum total disk size is 825GB.
* The evaluation OVA file is about 3GB that expands to 50GB when deployed with thin provisioning.  The maximum total disk size is 100GB. 
 
> Upgrades of the evaluation UCC are not supported.

* Thin provisioning may always be used, but when supporting a very large number of LMs, we recommend you use thick provisioning.  The space savings for using thin are minimal and thick provisioning will guarantee you have allocated enough disk space and remove any possible performance degradation as the disk grows.
* SSDs are always recommended regardless of deployment size.  The OVA will deploy quicker and the UCC will run with much lower latency.
* CPU cores may be adjusted without any changes to Uplogix configuration files.  Recommendations are specified above, but you may increase or decrease the number of cores based on your performance desires.  A restart of the VM is all that is needed after you change your VM properties.
* Memory may also be adjusted, but you must update an Uplogix configuration file - see [Adjusting Memory](#adjusting-memory).

# Deployment

Connect to your VM host and select **File > Deploy OVF Template...**.  Although this menu item says OVF, it will let you select OVA files as well.  An OVA file is just a package of the OVF file and VMDK files in the TAR format.

![vSphere Client Deploy OVF Template](http://uplogix.com/support/docs/img/5.4/vucc/image001.png)

## Select OVA

Select the vUCC OVA file you previously downloaded.

![Select OVA](http://uplogix.com/support/docs/img/5.4/vucc/image002.png) 

## Ignore Warning

Depending on the version of your VMware host, you may see a similar warning window below.  This is normal and will not impact the deployment of the vUCC.  Click Yes to proceed.

![Ignore Warning](http://uplogix.com/support/docs/img/5.4/vucc/image003.png)

## Select Datastore

Select a datastore with enough free space to handle your deployment (see [Requirements](#requirements)).

![Select Datastore](http://uplogix.com/support/docs/img/5.4/vucc/image004.png)

## Select Disk Format

Select **Thin Provision** or **Thick Provision** as appropriate to your deployment size for the disk format.  If you have determined that you should use thick provisioning, you may choose lazy or eager zeroed based on your own preferences.

![Select Disk Format](http://uplogix.com/support/docs/img/5.4/vucc/image005.png)

## Map Network

Map the source network to the destination network according to your needs.  The default is frequently acceptable.

![Map Network](http://uplogix.com/support/docs/img/5.4/vucc/image006.png)

## Finish

Ensure **Power on after deployment** is **not** selected.  Click Finish to begin the deployment of the vUCC.

![Finish](http://uplogix.com/support/docs/img/5.4/vucc/image007.png)

# Deployment Time

The progress bar is not very accurate with its time estimation.  Since the vUCC has 6 VMDKs (disks) inside the OVA, you will frequently see an estimate like *5 minutes remaining*, but then it will move on to the next disk and say the same estimate for remaining time.  Typical deployment times vary from 25 minutes (SSD RAID 10) to 3 hours (SAS RAID 5).  The deployment time is heavily dependent on the speed of the VMware host datastore and may increase when a datastore is heavily shared by other VMs.  Network speed is also a factor and we recommend you use a gigabit link.

![Deployment Time](http://uplogix.com/support/docs/img/5.4/vucc/image008.png) 
 
Once the deployment has completed successfully, click **Close**.

![Deployment Time](http://uplogix.com/support/docs/img/5.4/vucc/image009.png)

# Default Settings

The following shows the default settings for the vUCC.

![Default Settings](http://uplogix.com/support/docs/img/5.4/vucc/image010.png)

The following shows the default settings for the evaluation vUCC.

![Default Settings](http://uplogix.com/support/docs/img/5.4/vucc/image011.png)

# Edit Settings

If you need to edit any of the deployment settings, right-click on the VM's name.  Select **Edit Settings...** to change the number of CPU cores, memory, or network settings.

![Edit Settings](http://uplogix.com/support/docs/img/5.4/vucc/image012.png)

# Power On

Once the settings have been configured, power on the VM.  You can do this by right-clicking the VM name again or using the green “play” icon.

![Power On](http://uplogix.com/support/docs/img/5.4/vucc/image013.png)

# Automatic Startup

We recommend that you configure the vUCC for automatic startup and shutdown.  Version 5.4 of the vUCC contains open source vm tools which allow VMware to do a soft shutdown of the VM.  While problems usually do not occur with a hard power off, we recommend that you avoid it when possible.  Hard power off can occasionally cause file system corruption.

![Automatic Startup](http://uplogix.com/support/docs/img/5.4/vucc/image014.png)

# IP Configuration

After powering the VM on, click the **Console** tab.  Once the vUCC has finished booting, login as user *emsadmin* with password *password*.   You may miss the login prompt as information about the database writes to the console.  If you see *Database “UPLOGIX” warm started*, hit enter once and you will be presented with the login prompt.

To configure static IP addresses for the vUCC run the following commands:

* Enter sudo su - and enter *password* when prompted
* Enter /uplogix/embassy/netSetup.sh and follow the prompts to configure the IP addresses for the vUCC. 

![Test](http://uplogix.com/support/docs/img/5.4/vucc/image015.png)

# Adjusting Memory

If running the VM with anything other than 8 GB of RAM, the memory settings for the vUCC application will need to be changed:

* Enter **vi /etc/sysconfig/embassy.overrides**
* Move the cursor over the number 8 on the line which reads **RAM=8**
* Press **r**, then enter the number of gigs of RAM allocated to your VM
* Type **:wq **to save the file and exit from the editor
* Restart the vUCC application by entering the commands **ucc stop** and **ucc start**.

# Test

Launch a browser to the first IP address configured to verify successful installation.  The default user name is *administrator* and the default password is *password*.

![Test](http://uplogix.com/support/docs/img/5.4/vucc/image016.png)