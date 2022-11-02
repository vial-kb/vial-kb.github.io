---
layout: default
title: Reducing firmware size
parent: Porting guide
nav_order: 6
---

# Reducing firmware size

By default Vial enables every supported feature. As a result, on low-powered chips such as AVR series you might experience running out of flash memory, RAM, or EEPROM.

```
quantum/dynamic_keymap.c:102:1: error: static assertion failed: "Dynamic keymaps are configured to use more EEPROM than is available."
_Static_assert(DYNAMIC_KEYMAP_EEPROM_MAX_ADDR >= DYNAMIC_KEYMAP_MACRO_EEPROM_ADDR + 100, "Dynamic keymaps are configured to use more EEPROM than is available.");
```

```
 * The firmware is too large! 30768/28672 (2096 bytes over)
 [ERRORS]

make[1]: *** [tmk_core/rules.mk:469: check-size] Error 1
make: *** [Makefile:530: yd60mq:vial] Error 1
Make finished with errors
```

If that happens to your keyboard, you can try utilizing of the options below to make the firmware fit.

### Enable LTO

To enable LTO, add the following line to your `keymaps/vial/rules.mk`:

```
LTO_ENABLE = yes
```

LTO makes the compiler work harder when optimizing your code, resulting in a smaller firmware size; it rarely exposes buggy code in a way which could break certain firmware functionality. Make sure to test your keyboard firmware after enabling this option.

### QMK Settings

To turn off this feature, add the following line to your `keymaps/vial/rules.mk`:

```
QMK_SETTINGS = no
```

### Dynamic Tap Dance

To reduce RAM and EEPROM usage, you can define the following in your `config.h`: `#define VIAL_TAP_DANCE_ENTRIES 4`.

To turn off this feature, add the following line to your `keymaps/vial/rules.mk`:

```
TAP_DANCE_ENABLE = no
```

### Dynamic Combos

To reduce RAM and EEPROM usage, you can define the following in your `config.h`: `#define VIAL_COMBO_ENTRIES 4`.

To turn off this feature, add the following line to your `keymaps/vial/rules.mk`:

```
COMBO_ENABLE = no
```

### Dynamic Key Overrides

To reduce RAM and EEPROM usage, you can define the following in your `config.h`: `#define VIAL_KEY_OVERRIDE_ENTRIES 4`.

To turn off this feature, add the following line to your `keymaps/vial/rules.mk`:

```
KEY_OVERRIDE_ENABLE = no
```

### Reducing number of dynamic keymap layers

If you are running out of EEPROM, you can reduce the number of dynamic keymap layers. The default layer count is 4. To reduce it, define in your `config.h` file:

```
#define DYNAMIC_KEYMAP_LAYER_COUNT 2
```

# Using a different bootloader

```
 * The firmware is too large! 30768/28672 (2096 bytes over)
 [ERRORS]

make[1]: *** [tmk_core/rules.mk:469: check-size] Error 1
make: *** [Makefile:530: yd60mq:vial] Error 1
Make finished with errors
```

**If you have already done all of the above, and you still see this message trying to compile your firmware on an AVR such as the popular Atmega32u4 (used on Pro Micro), it might be time to break out of the mould a little.** 

Almost all of these controllers are delivered with the Caterina bootloader, and while this bootloader is very stable and plain **just works!** in all situtations, it's also fairly old code and quite large, using ~3500kB of your codespace. Most of it for features you will never really use.

Changing your bootloader to a more modern, more slim-lined one that does exactly what is needed and nothing else, can save you a whole lot of codespace for your keymap and functions.

### Potential drawbacks
**Changing the bootloader makes your firmware somewhat 'non-standard'**, so sharing them means the other user also have to swap to your preffered bootloader. It also requires you to use an ISP programmer (or another arduino) to flash the controller with the bootloader once, before it can be used as normal flashing the code over USB. (This is very similar to recovering the bootloader in the event of a bricked Pro Micro).

### What do I gain?
Codespace, glorious codespace!

### What bootloader is recommended?
There are several that should work and reduce the size to various amounts, some adding functions you might like, some being slimmed down. 
* [LUFA-DFU](https://github.com/abcminiuser/lufa) is a popular one that is slightly smaller than Caterina, and adds features (size depends on what features you enable).
* [QMK-DFU](https://github.com/qmk/lufa) is a fork maintained by the QMK team and also adds features.
* [nanoBoot](https://github.com/osamuaoki/nanoBoot) is a _tiny_ 512kB HID bootloader, that does exactly _one_ thing, allowing you to hold reset on plug-in, and enter the bootloader/flashing, in the exact same way as Caterina does. 



