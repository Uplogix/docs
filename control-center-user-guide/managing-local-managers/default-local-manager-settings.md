<!-- THIS FILE IS NOT USED -->
<div class='ucc' />Inventory > Group > System > Default Port Settings</div>
<div class='ucc' />Inventory > Local Manager Summary > System > Default Port Settings</div>

# Overview

Port Settings determine how the Local Manager interacts with managed devices. These settings can be defined on a single Local Manager or a group of Local Managers.
 	
To set up standard configurations on Inventory Groups, your role must have either Local Manager configuration permissions on the affected Local Managers or the **config hierarchy** permission. If your role includes the **config hierarchy** permission, only configurations for empty inventory groups can be set up. For more about roles and permissions, see [Managing privileges](http://uplogix.com/docs/control-center-user-guide/accounts-and-security/privileges).

# Adding Port Settings

To create default Local Manager settings:

Select an Inventory Group or Local Manager and click *Default Port Settings* under the *System* configuration menu.

![Uplogix Control Center Port Settings](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-inventory-port-settings.png)

Uplogix provides a list of possible managed devices that can be modified to your liking. A *Default* list of settings is also available for managed devices not matching any other criteria.

Port settings can be set to apply to managed devices based on make, model, os name, and os version, or any combination of the four.

For example, the *cisco ios* list applies to devices with the make of *cisco* and an os of *ios*. New lists can be created by clicking the *Add* button.

# Editing Port Settings

Create a new list or select an existing one. For more information on the various options, see [Configuring Port Settings for Managed Devices](http://uplogix.com/docs/local-manager-user-guide/configuring-managed-devices/configuring-port-settings) in the Local Manager User Guide section.

![Uplogix Control Center Port Settings Cisco](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-inventory-port-settings-cisco.png)

To modify a setting, click the checkbox to enable it, and then use the dropdown menu or text input box to enter a new value.

# Saving Port Settings

In addition to the *Save* button, the Control Center provides a *Force update on children* option to overwrite the port settings on any children or child groups that may have modified the port settings from their default state. This **will not** update any port settings that have been modified through the Local Manager's CLI.