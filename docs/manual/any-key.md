---
layout: default
title: Any key
parent: User manual
nav_order: 10
---

# Any key

The Basic tab has a special <kbd>Any</kbd> key. This is an escape hatch, useful to enter arbitrary keycodes that are **known to be supported in your build on the firmware** but not otherwise accessible in the GUI. Assigning "`Any`" to a key opens a dialog box where you can entry an arbitrary keycode. Alternatively, double click a keymap key to open this dialog.

## Textual entry

One way to enter a keycode is by its name or syntax as would be used when editing a QMK `keymap.c` in C, provided this name is known to the configurator. See the [full list of QMK keycodes](https://docs.qmk.fm/keycodes) for known keycode names. Macro syntax like `LSFT(kc)` and `MT(mod, kc)` is supported as well. In this way, it is possible to enter certain keys like [LM layer mod](https://docs.qmk.fm/feature_layers) keys and modifier combinations that are not otherwise exposed.

*Examples:*

| Syntax                          | Meaning                                    |
|---------------------------------|--------------------------------------------|
| `KC_ENT`                        | Enter key                                  |
| `C(KC_V)`                       | Left Ctrl + V                              |
| `C(S(KC_V))`                    | Left Ctrl + Left Shift + V                 |
| `RSA(KC_V)`                     | Right Shift + Right Alt + V                |
| `LM(2, MOD_LSFT)`               | Layer 2 + Left Shift layer mod switch.     |
| `OSM(MOD_LSFT | MOD_LGUI)`      | One-shot Left Shift + Left GUI             |
| `MT(MOD_RSFT | MOD_RALT, KC_A)` | Right Shift + Right Alt on hold, A on tap  |

Refer to the [QMK documentation](https://docs.qmk.fm) for full explanation of keycode syntax.


## Numeric entry

Another way to enter a key is numerically by its 16-bit keycode. Even when the key isn't known to the configurator by name, it is yet possible to enter the key in this way. It's a tedious process, but it does work to assign keys that would be otherwise unavailable. Of course, this only works provided you determine the correct numeric value for the keycode and your build of the firmware supports that keycode. Otherwise, the key will likely do nothing.

### How to determine numeric keycodes?

One way to deduce the numeric keycode values is by referring to the firmware source files that define them. The keycodes are defined in [quantum/keycodes.h](https://github.com/vial-kb/vial-qmk/blob/vial/quantum/keycodes.h), whereas preprocessor macros like `LSFT(kc)` are defined in [quantum/quantum\_keycodes.h](https://github.com/vial-kb/vial-qmk/blob/vial/quantum/quantum_keycodes.h).

*Example:* Suppose we have made a [custom build]({% link manual/custom-build.md %}) of Vial in which [Swap Hands](https://docs.qmk.fm/features/swap_hands), which Vial does not natively support, has been enabled by adding "`SWAP_HANDS_ENABLE = yes`" in `vial/rules.mk`. Swap Hands defines several feature-specific keys, such as `SH_MON`, `SH_OS`, and `SH_T(kc)`, which the configurator does not know.

> Important
> {: .label .label-red }
> The numeric values of the keycodes may differ between different versions of QMK. Verify keycode values for your version of the firmware.

We can find `SH_MON` and `SH_OS` (aka `QK_SWAP_HANDS_MOMENTARY_ON` and `QK_SWAP_HANDS_ONE_SHOT`) in `quantum/keycodes.h`:

```c
QK_SWAP_HANDS_MOMENTARY_ON = 0x56F2,
QK_SWAP_HANDS_MOMENTARY_OFF = 0x56F3,
QK_SWAP_HANDS_OFF = 0x56F4,
QK_SWAP_HANDS_ON = 0x56F5,
QK_SWAP_HANDS_ONE_SHOT = 0x56F6,
// (more codes...)
```

This shows the keycodes (expressed in hexadecimal) are `SH_MON = 0x56F2` and `SH_OS = 0x56F6`. We can therefore assign `SH_MON` to a key in the configurator by first assigning `Any`, then entering `0x56F2`. Since the configurator does not recognize the keycode, it displays as the raw numeric value `0x56F2` in the GUI. The key does nevertheless function as `SH_MON` on the keyboard itself.

Determining the keycode for `SH_T(kc)` is more complicated. Being a preprocessor macro, its definition is in `quantum/quantum_keycodes.h`:

```c
#define SH_T(kc) (QK_SWAP_HANDS | ((kc)&0xFF))
```

in which `QK_SWAP_HANDS` is `0x5600` (based on referring back to `quantum/keycodes.h`). For the key's "`kc`" placeholder, we can numerically substitute the keycode for any Basic key. For instance with `KC_A = 0x0004`, the full keycode for `SH_T(KC_A)` is `0x5604`.

