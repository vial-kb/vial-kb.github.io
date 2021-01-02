---
layout: default
title: Encoders
parent: Getting Started
nav_order: 3
---


# Vial encoders

Vial implements optional GUI configuration for rotary encoders. This allows users to set up  separate keycode actions for clockwise and counterclockwise encoder rotations. Encoders fully support QMK layers, so different keycodes can be used for different layers.

In order to enable encoder support in your firmware, follow these steps:

## Configure encoders in `config.h`

Follow [QMK documentation](https://docs.qmk.fm/#/feature_encoders?id=encoders) in order to configure encoders. Note that you do not need to implement any encoder callbacks, the only changes should be within the `config.h` and `rules.mk` files.

## Enable Vial encoders in `rules.mk`

Add `VIAL_ENCODERS_ENABLE = yes` to your `keymaps/via/rules.mk` file.

## Add Vial encoders as part of KLE keymap

Set up encoders as 1u switches:
* the center legend should be "e"
* the top left legend is "encoder_index,encoder_rotation", for example "0,0" for rotating encoder at index 0 counterclockwise, and "0,1" for rotating encoder at index 0 clockwise<sup>[(example)](http://www.keyboard-layout-editor.com/#/gists/604ca4b3942891950597cbaceac8bced)</sup>

![](../img/encoders-kle.png)

## Done!

Compile and flash the firmware, and you should be able to configure encoders in the UI:

![](../img/encoders-ui.png)
