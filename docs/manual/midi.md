---
layout: default
title: MIDI
parent: User manual
nav_order: 6
---

# MIDI

MIDI can be used to send MIDI commands thru USB MIDI interface.

**QMK** has 2 systems for MIDI, **BASIC** and **ADVANCED**
With MIDI BASIC you only can use notes keycodes (keys inside the red polygon) but not other keycodes like octave shift, channel change, modulation, etc.

![](../img/vial-midi.png)

## QMK configuration

To configure **QMK** to you've to add the following lines to the proper files on QMK keyboard folder

On **rules.mk**

```
DYNAMIC_MACRO_ENABLE = yes
```

To enable the **BASIC** or **ADVANCED** **MIDI** to add one of the following lines to the `config.h`

```
#define MIDI_BASIC
```

or

```
#define MIDI_ADVANCED
```

To enable **BASIC** or **ADVANCED** **MIDI** on **VIAL** it is necessary to add one of these lines to the `vial.json` file

```
"midi": "basic"
```

or

```
"midi": "advanced"
```

# More info

More detailed information about QMK MIDI can be found in the [offical QMK documenation](https://docs.qmk.fm/#/feature_midi).
