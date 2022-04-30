---
layout: default
title: Configuring udev on Linux
parent: User manual
nav_order: 5
redirect_from:
  - /getting-started/linux-udev.html
---

# Configuring `udev` rules for Vial on Linux

In order for your keyboard to be detected by Vial on Linux, you need to set up a custom `udev` rule. VIA and Vial both use the `hidraw` linux driver to directly communicate configurations to your keyboard. In most situations it should be safe to use a generalized `udev` rule for all `hidraw` devices, but in other cases where you prefer or are required to restrict access on a device basis, it is possible to create a `udev` rule specifically for your keyboard.

The following guides will show you how to implement these `udev` rules. You will require root access to create the files necessary.

## Generalized `udev` rule

For a generalized access rule for `hidraw` devices, write this text to `/etc/udev/rules.d/99-vial.rules`:


```
KERNEL=="hidraw*", SUBSYSTEM=="hidraw", MODE="0660", GROUP="users", TAG+="uaccess", TAG+="udev-acl"
```

This rule makes the assumption that you are already in the `users` group, however, you can replace this group with any that you'd like, ideally with a group for human users on your system. This rule is tagged with `uaccess` and `udev-acl`, which applies user session and ACL restrictions if already configured.

## Device-specific `udev` rules

### Finding the vendor and product IDs

Configuring device specific udev rules will requrie knowing the USB vendor and product ID of your keyboard. The easiest way to find this is using the `lsusb` command. It will list information about all of your connected USB devices. Here is a sample output for the Keychron Q2 Revision 0110:
```
Bus 001 Device 049: ID 3434:0110 Keychron Keychron Q2
```
The first four hex numbers next to `ID` is the vendor ID, and the next four hex numbers after the colon is the product ID. In this case, the Keychron Q2's vendor ID is `3434` and it's product ID is `0110`.

#### Where is my keyboard in `lsusb`?

Depending on your keyboard, the device name may be missing, or may not be the name of your keyboard at all. This is due to the fact that a majority of QMK compatible keyboards are not made by major companies with vendor ID's registered with the USB-IF. As a result, the IDs are sometimes set to arbitrary or unofficial values, or use the ID's supplied by the microcontroller's USB interface.

To find out which device is your keyboard, run `lsusb` with your keyboard plugged in and then run it again while disconnected. You should be able to find the different device between the two outputs.

### Creating the `udev` rule

To create a rule for your specific keyboard, use this template:

```
# Name of your keyboard
KERNEL=="hidraw*", SUBSYSTEM=="hidraw", ATTRS{idVendor}=="XXXX", ATTRS{idProduct}=="XXXX", MODE="0660", GROUP="users", TAG+="uaccess", TAG+="udev-acl"
```

Replace the vendor and product ID with the ones you found for your keyboard using [lsusb](#finding-the-vendor-and-product-ids). Write this rule to `/etc/udev/rules.d/99-vial.rules` as root.

The following is an example udev rule for the Keychron Q2:

```
# Keychron Q2
KERNEL=="hidraw*", SUBSYSTEM=="hidraw", ATTRS{idVendor}=="3434", ATTRS{idProduct}=="0110", MODE="0660", GROUP="users", TAG+="uaccess"
```

## Reloading `udev`

In order for your new `udev` rules to take effect, you must reload the `udev` rules. The standard way to do this is to run the following command as root:

```
udevadm control --reload-rules && udevadm trigger
```

If this command doesn't work, or it's not available, check that you are root or using a privledge escalation tool like `sudo`, and make sure to read your distribution's handbook/manual.