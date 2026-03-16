---
layout: default
title: Custom Keycode
parent: Porting guide
nav_order: 8
redirect_from:
  - /manual/custom_keycode.html
---

## Custom keycodes in QMK

QMK provides [a way](https://github.com/qmk/qmk_firmware/blob/master/docs/custom_quantum_functions.md) for user to redefine behavior for existing key or create new keycode.

For example, here 3 custom keycodes are defined within `keymap.c`. An `enum` block is used to assign each keycode a unique integer code, and then the behavior of each keycode is defined inside `process_record_user()`. The keycodes are then assigned inside the keymap as usual.

```c
enum blender_keycode {
    B_VPAN = SAFE_RANGE,
    B_DOLLY,
    B_UNDO,
};

bool process_record_user(uint16_t keycode, keyrecord_t *record) {
    switch (keycode) {
        case B_VPAN:
            if (record->event.pressed) { ... }
            return 0;
        case B_DOLLY:
            if (record->event.pressed) { ... }
            return 0;
        case B_UNDO:
            if (record->event.pressed) { ... }
            return 0;
    }
}
```

When you load a board with custom keycodes, they will appear as unique hexcode. You can use the "any key" button and type in values starting with `0x7E40` to assign them but this isn't very user friendly.

![](/img/vial_before.png)

## Custom keycodes in Vial

Vial provides a way to alias custom keycodes so that they appear as a named keycode you can assign in the GUI.

In `vial.json` you can create a new list named `customKeycodes` with each of the keycodes having three properties:

- `shortName`: the name that will appear on the key in the GUI; it needs to be short otherwise the text will overflow.
- `title`: a short description that will appear when you hover over the keycode
- `name`: appears before title

For those three keycodes you'd have something like this in your `vial.json`. Watch out for any syntax errors. The last item in the list should not have a comma.

```json
....
"customKeycodes": [
	{"name": "Vpan",
	 "title": "Viewport pan",
	 "shortName": "B_VPAN"
	},
	{"name": "Dolly",
	 "title": "Dolly zoom",
	 "shortName": "B_DOLLY"
	},
	{"name": "Undo",
	 "title": "",
	 "shortName": "B_UNDO"
	}
],
"matrix": { "rows": 6, "cols": 5 },
....
```

In the keymap.c file, replace `SAFE_RANGE` with `QK_KB_0`:

```c
enum blender_keycode {
    B_VPAN = QK_KB_0,
    B_DOLLY,
    B_UNDO,
};
```

Custom keycodes in the json file __must__ match what's inside the enum block, both in order and number of keycodes.

If everything goes smoothly the hexcode will be replaced with name of the keycode. You can access all your custom keycode inside the User tab. Do note that the firmware size will increase slightly (this example is ~100bytes).

![](/img/vial_after.png)

![](/img/user_tab.png)
