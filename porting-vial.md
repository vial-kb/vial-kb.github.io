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

Then, add this line to your keyboard's `config.h` under `#define DESCRIPTION`. <sup>[(example)](https://github.com/vial-kb/vial-qmk/blob/a88f05ea1e2d6bf32dee4dae3be50f5de28b7263/keyboards/xyz/g60/config.h#L28)</sup>

## Done!

You now should be able to compile the firmware, flash it, and have your keyboard auto-detected by Vial.
