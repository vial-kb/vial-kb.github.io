---
layout: default
title: Step 2 - Porting to Vial
parent: Getting Started
nav_order: 2
---

# Porting a VIA keyboard to Vial

The second step is to port your VIA keyboard to Vial.

## Base your changes off `vial-kb/vial-qmk`

Vial is currently not included into the main QMK repository. As such, you will need to check out Vial's QMK fork and port your keyboard there. If you've started with the Part 1 of this tutorial, you should already be set.

## Enable Vial

In your `keymaps/via/rules.mk` add `VIAL_ENABLE = yes` as a new line after `VIA_ENABLE = yes`. <sup>[(example)](https://github.com/vial-kb/vial-qmk/blob/a88f05ea1e2d6bf32dee4dae3be50f5de28b7263/keyboards/xyz/g60/keymaps/via/rules.mk#L2)</sup>

## Set up JSON

Place your VIA JSON under `keymaps/via/vial.json` so that Vial build process can find it. <sup>[(example)](https://github.com/vial-kb/vial-qmk/blob/a88f05ea1e2d6bf32dee4dae3be50f5de28b7263/keyboards/xyz/g60/keymaps/via/vial.json)</sup>

## Set up unique keyboard ID

From the root of QMK, run `python3 util/vial_generate_keyboard_uid.py` in order to generate a unique Vial keyboard ID:

```
% python3 util/vial_generate_keyboard_uid.py
#define VIAL_KEYBOARD_UID {0xXX, 0xXX, 0xXX, 0xXX, 0xXX, 0xXX, 0xXX, 0xXX}
```

Then, add this `#define` to your keyboard's `config.h` as a new line. <sup>[(example)](https://github.com/vial-kb/vial-qmk/blob/a88f05ea1e2d6bf32dee4dae3be50f5de28b7263/keyboards/xyz/g60/config.h#L28)</sup>

## Set up a secure unlock combination

Vial needs a key combination in order to protect the user from a malicious host computer unknowingly changing security-sensitive settings, such as flashing a malicious firmware; for more information see [here](../security.md).

If you do not want to utilize this feature, you should set `VIAL_INSECURE = yes` in your `keymaps/via/rules.mk`.

Otherwise, you should proceed to configure `VIAL_UNLOCK_COMBO_ROWS` and `VIAL_UNLOCK_COMBO_COLS` definitions:

* You should configure a combo of at least 2 keys
* Suppose this is your KLE and you want to configure a combo of Escape+Enter:
![](../img/security-kle.png)
* The Escape key is located at [0, 0] and the Enter key is at [2, 13]
* So you should set in your `config.h` right below the `VIAL_KEYBOARD_UID` line:
  * `#define VIAL_UNLOCK_COMBO_ROWS { 0, 2 }`
  * `#define VIAL_UNLOCK_COMBO_COLS { 0, 13 }`
* Note that this feature works with multi-layout keyboards, however you should make sure that the keys you pick appear in every possible layout:
![](../img/security-user-prompt.png)

After you flash the firmware, check that the function works correctly by activating the "Security->Unlock" menu.

## Done!

You now should be able to compile the firmware, flash it, and have your keyboard auto-detected by Vial.
