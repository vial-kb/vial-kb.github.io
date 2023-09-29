---
layout: default
title: Build Vial Firmware - 3 - Select GUI Functions
parent: Porting guide
nav_order: 4
redirect_from:
  - /gettingStarted/build-firmware-3.html
  - /getting-started/build-firmware-3.html
---

> Information
> {: .label .label-green }
> `vial-qmk` provides several examples of most common microcontroller configurations set up for Vial usage. You can check them out at [`vial-qmk/keyboards/vial_example`](https://github.com/vial-kb/vial-qmk/tree/vial/keyboards/vial_example).

# Selecting what Functions to enable in Vial GUI

By default, Vial replaces *some* of QMK's functions with Vial specific functions, enabling the appropriorate tabs in the Vial GUI. To control what functions to compile in, you set defentitions in the `keymaps/vial/rules.mk` file like shown below.

Example `rules.mk` file:
```
# Copyright TestUser
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
  * add `#define DYNAMIC_KEYMAP_LAYER_COUNT xx` to `keymaps/vial/config.h` to adjust the number of layers.
  * Defaults is 4.
* The `Layout` section allows you to select optional layout's for your keyboard, such as different bottom row configurations.
* The `Matrix tester` section allows you to check that your keys are working properly.

### Additional sections
* `Macros` section, allows configuring macros that can be used to perform a pre-programmed sequence of actions or steps.
  * Add `#define DYNAMIC_KEYMAP_MACRO_COUNT xx` to `keymaps/vial/config.h` to adjust the available amount.
  * Default is 16.
  * QMK Documentation : [Macros](https://docs.qmk.fm/#/feature_macros?id=macros)
* `QMK_SETTINGS = yes`, allows various settings for functions like Tap-Hold, Auto Shift etc.
  * QMK Documentation : [Magic/Command](https://docs.qmk.fm/#/feature_command?id=command), [Auto Shift](https://docs.qmk.fm/#/feature_auto_shift?id=auto-shift-why-do-we-need-a-shift-key), [Tap Hold](https://docs.qmk.fm/#/tap_hold?id=tap-hold-configuration-options) 
* `TAP_DANCE_ENABLE = yes`, allows a single key to do multiple things.`
  * Add `#define VIAL_TAP_DANCE_ENTRIES xx` to `keymaps/vial/config.h` to adjust the available amount.
  * Default is 32.
  * QMK Documentation : [Tap Dance](https://docs.qmk.fm/#/feature_tap_dance?id=tap-dance-a-single-key-can-do-3-5-or-100-different-things)
* `COMBO_ENABLE = yes`, allows you to combine 2-4 simultaneous key-presses (chording) into a different output.
  * Add `#define VIAL_COMBO_ENTRIES xx` to `keymaps/vial/config.h` to adjust the available amount.
  * Default is 32.
  * QMK Documentation : [Combos](https://docs.qmk.fm/#/feature_combo?id=combos)
* `KEY_OVERRIDE_ENABLE = yes`, allows you to override modifier-key combinations to send a different modifier-key combination or perform completely custom actions. 
  * Add `#define VIAL_KEY_OVERRIDE_ENTRIES xx` to `keymaps/vial/config.h` to adjust the available amount.
  * Default is 32.
  * QMK Documentation : [Key Overrides](https://docs.qmk.fm/#/feature_key_overrides?id=key-overrides)
