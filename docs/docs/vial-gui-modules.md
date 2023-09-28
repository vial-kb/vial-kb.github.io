---
layout: default
title: Build Vial Firmware - 3 - Select GUI Tabs
parent: Porting guide
nav_order: 3
redirect_from:
  - /gettingStarted/vial-gui-modules.html
  - /getting-started/vial-gui-modules.html
---

> Information
> {: .label .label-green }
> `vial-qmk` provides several examples of most common microcontroller configurations set up for Vial usage. You can check them out at [`vial-qmk/keyboards/vial_example`](https://github.com/vial-kb/vial-qmk/tree/vial/keyboards/vial_example).

# Selecting what Tabs/Sections to enable in Vial GUI

By default, Vial replaces *some* of QMK's functions with Vial specific functions, enabling the tabs in the Vial GUI. To control what parts to compile in, you set defentitions in the `keymaps/vial/rules.mk`file like shown below.

Example `rules.mk` file:
```
# Copyright 
# SPDX-License-Identifier: GPL-2.0-or-later

# Minimum needed for VIAL compatability (both are needed!)
VIA_ENABLE = yes
VIAL_ENABLE = yes

# Needed to map encoders in Vial
ENCODER_MAP_ENABLE = yes

# Additional Vial GUI modules
TAP_DANCE_ENABLE = yes
QMK_SETTINGS = yes
KEY_OVERRIDE_ENABLE = yes
COMBO_ENABLE = yes
```

## Available GUI sections
### Default sections
* The `Keymap` section is always included, and is the main part where you map keys.
* The `Layout` section allows you to select optional layout's for your keyboard, such as different bottom row configurations.
* The `Matrix tester` section allows you to check that your keys are working properly.

### Additional sections
* `Macros` section, allows configuring macros that can be used to perform a pre-programmed sequence of actions or steps.
* `QMK_SETTINGS = yes` allows setting various settings like Tap-Hold timing, Auto Shift timing, etc.
* `TAP_DANCE_ENABLE = yes` allows a single key to do multiple things.
* `COMBO_ENABLE = yes` allows you to combine 2-4 simultaneous key-presses into a different output.
