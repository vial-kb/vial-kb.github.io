---
layout: default
title: Backlight and RGB lighting
parent: Porting guide
nav_order: 5
---

# Backlight and RGB lighting

Vial support several QMK lighting modes including single-color backlight, RGB lighting and RGB matrix.

### RGB Matrix / VialRGB

RGB matrix is a QMK lighting mode suitable for implementing per-key RGB lighting as well as a combination of per-key RGB and underglow. It is the recommended lighting mode for most purposes. In addition, Vial builds up on QMK RGB Matrix to provide direct RGB control with a script running on the computer.

In order to use RGB Matrix with Vial, first, follow [QMK documentation](https://docs.qmk.fm/#/feature_rgb_matrix) to enable and configure the feature. Then, add `VIALRGB_ENABLE = yes` to your `keymaps/vial/rules.mk` and `"lighting": "vialrgb",` to your `keymaps/vial/vial.json`.

If you are having issues with VialRGB direct control mode (e.g. running out of memory), you can disable it by adding `#define VIALRGB_NO_DIRECT`.

![](/img/lighting-rgb-matrix.png)

Vial GUI allows configuring RGB Matrix effect (the list of effects will be automatically constructed based on RGB effects you have enabled), color, brightness and speed. Additionally, a raw HID API is provided for third-party applications to directly control the lights. An example script is available [here](https://gist.github.com/xyzz/c91ae462197d4ef30d034bb6ff4c945e).

## Backlight

Backlight here refers to the single-color key backlighting, typically achieved by soldering 2-pin LEDs to every switch position. Vial's backlighting feature lets users control backlight brightness and enable or disable breathing backlight animation.

![](/img/lighting-backlight.png)

In order to use this feature, ensure that [QMK's Backlight](https://docs.qmk.fm/#/feature_backlight) is enabled (`BACKLIGHT_ENABLE = yes`). Make sure there's `#define BACKLIGHT_BREATHING` in your `config.h` so that the user can switch the breathing feature on and off in Vial GUI.

Finally, add `"lighting": "qmk_backlight",` to your `vial.json` in order to activate this feature on the GUI side.<sup>[(example)](https://github.com/vial-kb/vial-qmk/blob/2b2ff48c5d8d9b8995ca49eead031ae3691192e1/keyboards/ilumkb/primus75/keymaps/vial/vial.json#L5)</sup>

## RGB Lighting

RGB lighting is a lighting mode most suitable for keyboard underglow. Note that even if your keyboard only has underglow and no per-key RGB, it might be more suitable for your project to use RGB Matrix instead as that is a much more powerful feature.

To use this feature, first follow [QMK documentation](https://docs.qmk.fm/#/feature_rgblight) to enable RGB Lighting. Then, add `"lighting": "qmk_rgblight",` to your `vial.json`.<sup>[(example)](https://github.com/vial-kb/vial-qmk/blob/2b2ff48c5d8d9b8995ca49eead031ae3691192e1/keyboards/tw40/keymaps/via/vial.json#L5)</sup>

## Combining Backlight and RGB Lighting

You can also have a keyboard that implements both Backlight and RGB Lighting features. First, follow the sections above in order to configure QMK firmware enabling both features. Then, in your `vial.json`, use `"lighting": "qmk_backlight_rgblight",`.<sup>[(example)](https://github.com/vial-kb/vial-qmk/blob/2b2ff48c5d8d9b8995ca49eead031ae3691192e1/keyboards/yd60mq/keymaps/vial/vial.json#L5)</sup>
