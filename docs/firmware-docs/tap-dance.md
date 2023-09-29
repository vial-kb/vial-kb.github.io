---
layout: default
title: Auto-Populating Tap Dance
parent: Porting guide
nav_order: 8
---

# Auto-Populating Tap Dance

Vial made some changes to the tap dance logic, so you can't simply use [QMK code](https://docs.qmk.fm/#/feature_tap_dance) for it. But if you're familiar with setting up tap dances using the UI, you can edit your keymap so it uses Vial's system and automatically populates the entries after flashing the firmware, so you don't have to load a layout manually after every firmware update.

In our example, we want to toggle between layers when tapping, and sending `CAPS_LOCK` on hold.

In your `keymap.c` file, add the keycode `TD(0)` to the layout - tap dances in Vial go from 0 to 31.
Further down, add:
```c
void keyboard_post_init_user(void) {
    vial_tap_dance_entry_t td = { TG(1),
                                  KC_CAPSLOCK,
                                  KC_NO,
                                  KC_NO,
                                  TAPPING_TERM };
    dynamic_keymap_set_tap_dance(0, &td); // the first value corresponds to the TD(i) slot
}
```
The arguments for `vial_tap_dance_entry_t` are the same as in Vial's UI:

![vial screenshot](https://user-images.githubusercontent.com/82843921/201093073-968be14a-bba4-4b14-baee-71eb58ae87d2.png)
