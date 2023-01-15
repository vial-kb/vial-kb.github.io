---
layout: default
title: Rotary encoder support
parent: Porting guide
nav_order: 4
redirect_from:
  - /gettingStarted/encoders.html
  - /getting-started/encoders.html
---


# Rotary encoders

Vial implements optional GUI configuration for rotary encoders. This allows users to set up  separate keycode actions for clockwise and counterclockwise encoder rotations. Encoders fully support QMK layers, so different keycodes can be used for different layers.

You will need to port your keyboard over to Vial before encoders are supported. Follow [Step 1](/porting-to-via.md) and [Step 2](/porting-to-vial.md) to get started.

In order to enable encoder support in your firmware, follow these steps:

## 1. Add QMK encoder support to `config.h`

Follow [QMK documentation](https://docs.qmk.fm/#/feature_encoders?id=encoders) in order to configure encoders. Note that you do not need to implement any encoder callbacks, the only changes should be within the `config.h` and `rules.mk` files.

## 2. Enable QMK Encoder Map

Follow [QMK documentation](https://docs.qmk.fm/#/feature_encoders?id=encoder-map) in order to enable the `ENCODER_MAP` feature in your `vial` keymap.

## 3. Add Vial encoders as part of KLE keymap

In Vial JSON an encoder is defined as either **two or three** 1u switches, representing the possible actions it can have. 
**Not having both rotary switches defined makes the JSON invalid.**


**An encoder with no clickable button:**

![](../img/encoders-kle.png)

**An encoder with a clickable button:**

![](../img/encoders-kle2.png)

**Dual encoders with buttons:**

![](../img/dual-encoders-kle.png)

**Multiple encoders combined with matrix:**

Notice that in this example, the top row of switches marked red, are intended to be replaced by the encoders button action.

![](../img/multiple-encoders-kle.png)

### Encoder Legends
**Center legend**
- The two switches for the CW and CCW rotary actions both have a center legend of `e`.
 
**Top Legend**
- The top legend denotes the rotary index and action. **NOT the matrix position, or switch index.** This is separate from the matrix, and should not be confused with each other. `Encoder Index, Rotary action (0 = CCW, 1 = CW)`

**Clickable button**
- The bottom 1u switch represents the actual clickable button, and is usually part of the normal matrix, **having a normal index** not related to the actual encoder, but likely which key the encoder replaces, or where it is placed.


### KLE import
Exporting the json from KLE will introduce the following lines to your file, these relate to the encoders (Example of two encoders):
```
  ["0,0\n\n\n\n\n\n\n\n\ne",
  "0,1\n\n\n\n\n\n\n\n\ne"],
  
  ["2,0\n\n\n\n\n\n\n\n\ne",
  "2,1\n\n\n\n\n\n\n\n\ne"],
```
Enclose any associated x w h with double quotes `"`, as KLE json and vial json has slight differences in notation.


## Complete examples

### **9 Key macro pad example**
Building a basic 9 key macro pad and a rotary encoder (without button) will produce the following. <sup>[(example KLE file)](http://www.keyboard-layout-editor.com/#/gists/f6c1df29df0d44744d9a4dafe26178ef)</sup>

![](../img/basic-91.png)

```json
{
    "name": "NinetyOne",
    "vendorId": "0xXXXX",
    "productId": "0xXXXX",
    "lighting": "none",
    "matrix": {
        "rows": 3,
        "cols": 3
    },
    "layouts": {
        "keymap": [
        [
          { "y": 0.25, "x": 0.5 },
          "0,0\n\n\n\n\n\n\n\n\ne",
          "0,1\n\n\n\n\n\n\n\n\ne"],
        [ {"y": 0.25},
          "0,0", "0,1", "0,2"],
          ["1,0", "1,1", "1,2"],
          ["2,0", "2,1", "2,2"]
        ]
    }
}

```
### A macropad with 16 keys and 3 encoders

[Example KLE file](http://www.keyboard-layout-editor.com/##@@=0,0&=0,1&=0,2&=0,3&_x:0.25%3B&=0,0%0A%0A%0A%0A%0A%0A%0A%0A%0Ae&=0,1%0A%0A%0A%0A%0A%0A%0A%0A%0Ae&_x:0.25%3B&=1,0%0A%0A%0A%0A%0A%0A%0A%0A%0Ae&=1,1%0A%0A%0A%0A%0A%0A%0A%0A%0Ae%3B&@=1,0&=1,1&=1,2&=1,3&_x:0.75%3B&=0,4&_x:1.25%3B&=1,4%3B&@=2,0&=2,1&=2,2&=2,3%3B&@_y:-0.75&x:4.5%3B&=2,0%0A%0A%0A%0A%0A%0A%0A%0A%0Ae&_w:1.75&h:1.75%3B&=2,4&=2,1%0A%0A%0A%0A%0A%0A%0A%0A%0Ae%3B&@_y:-0.25%3B&=3,0&=3,1&=3,2&=3,3)

![](../img/bigmacro.png)

```json
{
    "name": "BIGMAC",
    "vendorId": "0xXXXX",
    "productId": "0xXXXX",
    "lighting": "none",
    "matrix": {
        "rows": 4,
        "cols": 5
    },
    "layouts": {
        "keymap": [
			[
				"0,0","0,1","0,2","0,3",
				
				{"x":0.25},
				"1,0\n\n\n\n\n\n\n\n\ne",
				"1,1\n\n\n\n\n\n\n\n\ne",
			
				{"x":0.25},
				"0,0\n\n\n\n\n\n\n\n\ne",
				"0,1\n\n\n\n\n\n\n\n\ne"
			],
			
			[
				"1,0","1,1","1,2","1,3",
				{"x":0.75},"0,4",
				{"x":1.25},"1,4"
			],
			[
				"2,0","2,1","2,2","2,3"
			],
			[
				{"y":-0.75,"x":4.5},
				"2,0\n\n\n\n\n\n\n\n\ne",
				{"w":1.75,"h":1.75},"2,4",
				"2,1\n\n\n\n\n\n\n\n\ne"],
			[
				{"y":-0.25},"3,0","3,1","3,2","3,3"
			]
        ]
    }
}
```


## Done!

Compile and flash the firmware, and you should be able to configure encoders in the UI:

![](../img/encoders-ui.png)
