---
layout: default
title: Configuring udev on Linux
parent: User manual
nav_order: 6
redirect_from:
  - /getting-started/linux-udev.html
---

# Configuring udev on Linux

In order for your keyboard to be detected on Linux, you need to set up a custom udev rule. Open a terminal and execute the following commands to set this up:

```
sudo mkdir -p /etc/udev/rules.d/
echo 'KERNEL=="hidraw*", SUBSYSTEM=="hidraw", MODE="0666", TAG+="uaccess", TAG+="udev-acl"' | sudo tee /etc/udev/rules.d/92-viia.rules
sudo udevadm control --reload-rules
sudo udevadm trigger
```

Afterwards, restart Vial GUI and your keyboard should be automatically detected.
