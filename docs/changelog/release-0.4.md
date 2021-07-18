---
layout: default
title: v0.4
parent: Changelog
nav_order: -4
---

# Version 0.4

Vial version 0.4 was released on July 18, 2021.

## RGB Matrix

The new Lighting implementation, VialRGB, builds upon QMK RGB Matrix feature.

![](/img/release-0.4/rgb_matrix.png)

It provides a simple interface to configure all of available RGB Matrix effects, color, speed and brightness.

## RGB Direct Control

In addition to RGB Matrix effects, VialRGB also provides direct LED control with a script running on your computer. You can find an example script [here](https://gist.github.com/xyzz/c91ae462197d4ef30d034bb6ff4c945e).

## Tap Dance

The new Vial Tap Dance feature exposes QMK's Tap Dance functionality in a user-friendly way.

![](/img/release-0.4/tap_dance.png)

You can configure up to four different keycodes, including macros or layer keys, to be executed when a key is tapped, held, double-tapped or tapped and then held.

## Combos

Similarly, Vial Combos let you take control of QMK's Combos without having to compile the firmware yourself.

![](/img/release-0.4/combos.png)

Hitting these keys together will change them into a different keycode.

## QMK Settings

Having to recompile QMK in order to change Grave Escape behavior, or Tap-Hold timings is annoying. The new Vial QMK Settings feature exposes a subset of QMK settings, typically configured with `#define` statements, and provides an interface to configure them in real time. The following settings are currently implemented:

### Grave Escape

No longer do you have to suffer from Ctrl-Shift-GrEsc not opening Task Manager on Windows. Simply check the box to configure Grave Escape just the way you like it:

![](/img/release-0.4/qs_grave_escape.png)

### Tap-Hold

![](/img/release-0.4/qs_tap_hold.png)

### Auto Shift

Were you ever curious to try Auto Shift, but found compiling the firmware too difficult? Now this unique QMK feature is just a click away.

![](/img/release-0.4/qs_autoshift.png)

### Combo

![](/img/release-0.4/qs_combo.png)

### One Shot Keys

![](/img/release-0.4/qs_osk.png)

### Mouse Keys

These settings let you configure how the mouse is emulated when using mouse movement keycodes such as `KC_MS_L`.

![](/img/release-0.4/qs_mouse_keys.png)

## GUI Improvements

The "Layout" tab will now show a preview of the physical key layout.

![](/img/release-0.4/layout_editor.png)

## EEPROM Emulation Improvements

The EEPROM emulation algorithm used on STM32 processors was improved to allow for 4096 bytes of EEPROM while consuming the same amount of flash as before.

## STM32F4 EEPROM Emulation Support

Further to the above, the new release's emulated EEPROM driver also supports STM32F4 processors. A new `vial_example` keyboard is available under `vial_example/vial_stm32f401` to use as a reference.

## Bug Fixes

Several minor bugs have been fixed in this release and new, more exciting bugs, have been implemented.
