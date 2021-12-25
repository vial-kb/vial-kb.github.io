---
layout: default
title: Reducing firmware size
parent: Porting guide
nav_order: 7
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

### Reducing number of dynamic keymap layers

If you are running out of EEPROM, you can reduce the number of dynamic keymap layers. The default layer count is 4. To reduce it, define in your `config.h` file:

```
#define DYNAMIC_KEYMAP_LAYER_COUNT 2
```
