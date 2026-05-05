---
layout: default
title: Custom build
parent: User manual
nav_order: 1000
---

# Custom build

While Vial provides a default set of features and limits, the firmware can be customized by modifying the source files before compilation. 

Generally, the process for creating a custom Vial build is:

1. [Set up your build environment.]({% link manual/install.md %}#setting-up-your-build-environment)

2. Edit the `config.h`, `rules.mk`, `keymap.c`, etc. files in your `vial` keymap folder to adjust feature limits, enable additional QMK features, or make other customizations.

3. [Rebuild and flash]({% link manual/install.md %}#building-firmware) the customized firmware to your keyboard.

   *Tip:* Use the Vial configurator to save your current Vial keymap to .vil file before flashing (File &rarr; Save current layout). Then after flashing, load the saved keymap to restore it. 


## Adjusting feature limits

Vial sets default limits on the maximum number of keymap layers and on the number of combos and other feature entries. If the keyboard's microcontroller has sufficient free space, you can edit `config.h` to increase these limits. Or conversely, limits may be decreased to recover memory.

To adjust these limits, add or modify the following definitions in the `config.h` file in your `vial` keymap folder:

* `DYNAMIC_KEYMAP_LAYER_COUNT`: Defines the maximum number of layers. Increasing this allows for more layers but consumes more memory.
* `DYNAMIC_KEYMAP_MACRO_COUNT`: Number of macros.
* `VIAL_TAP_DANCE_ENTRIES`: Number of Tap Dance entries.
* `VIAL_COMBO_ENTRIES`: Number of combos.
* `VIAL_KEY_OVERRIDE_ENTRIES`: Number of Key Overrides.
* `VIAL_ALT_REPEAT_KEY_ENTRIES`: Number of Alt Repeat Key entries.

*Example*:
```c
#define DYNAMIC_KEYMAP_LAYER_COUNT 16  
#define DYNAMIC_KEYMAP_MACRO_COUNT 32  
#define VIAL_TAP_DANCE_ENTRIES 32      
#define VIAL_COMBO_ENTRIES 32          
#define VIAL_KEY_OVERRIDE_ENTRIES 32   
#define VIAL_ALT_REPEAT_KEY_ENTRIES 32 
```

After adjusting limits, rebuild and flash the firmware to apply them.


## Custom keycodes and macros

Vial supports user-defined keycodes that appear in the configurator, under the User tab, allowing you to assign them in the keymap just like standard keys. See [Custom keycodes in Vial]({% link docs/custom_keycode.md %}#custom-keycodes-in-vial) for details. As in mainline QMK, handle your custom keys in `process_record_user()` in `vial/keymap.c`. See [QMK's macros documentation](https://docs.qmk.fm/feature_macros) for explanation and examples of how to do this.


## Enabling Core QMK Features

Vial supports many, but not all, core QMK features out of the box. Features such as [Swap Hands](https://docs.qmk.fm/features/swap_hands) or [Autocorrect](https://docs.qmk.fm/features/autocorrect), which are disabled in a default build, can be enabled by adding the appropriate definitions as specified in the QMK documentation.

> Important
> {: .label .label-red }
> QMK features enabled in this manner **lack GUI support** in the Vial configurator. While the feature may operate correctly on the keyboard, you will not be able to configure the feature's settings or assign its specific keycodes through the standard palette in the GUI. You can still use the "Any" key in the configurator to assign keycodes numerically.

*Examples:*

* To enable [Autocorrect](https://docs.qmk.fm/features/autocorrect), add this line in `rules.mk`:

  ```
  AUTOCORRECT_ENABLE = yes
  ```

* To enable [Speculative Hold](https://docs.qmk.fm/tap_hold#speculative-hold), add this line in `config.h`:

  ```c
  #define SPECULATIVE_HOLD
  ```

*Troubleshooting*: If the build fails with a message like "`firmware is too large!`," too many features are enabled to fit in flash memory. [See this page]({% link docs/firmware-size.md %}) for tips on reducing firmware size.

Some features define keys specific to that feature. Unfortunately, Vial is unaware of features outside of what it explicitly supports and won't show their keys in the configurator. It is yet possible to assign such keys numerically through [Any key]({% link manual/any-key.md %}#numeric-entry) arbitrary keycode entry.


## QMK Community Modules

[QMK Community Module](https://docs.qmk.fm/features/community_modules) allow for sharing and using third-party features. It is possible to use modules in a custom Vial build.

1. Copy the modules under `vial-qmk/modules/<author_name>/<module_name>`.
2. In your `vial` keymap folder, create or add to the `keymap.json` file to specify which modules to enable.
3. Follow the module's documentation for any further setup instructions.
 
Here too, modules lack GUI support in the Vial configurator. You will not be able to configure the module's settings in the configurator. If the module defines keycodes, you will need to use the [Any key]({% link manual/any-key.md %}#numeric-entry) in the configurator and assign keycodes numerically.

