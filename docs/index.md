---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
title: Home
nav_order: 1
---

## What is Vial?

Vial is an open-source cross-platform (Windows, Linux and Mac) GUI and a QMK fork for configuring your keyboard in real time, similar to VIA.

If you're already familiar with VIA, the major difference is that Vial is a completely open project, with sources for all components publicly available on [GitHub](https://github.com/vial-kb).

Another big goal for the project was to reduce reliance on third parties when developing a new keyboard. With Vial, you do not have to submit your keyboard as a pull-request for QMK and/or VIA (which usually takes several months to be accepted) before it can be used in the GUI; rather, the keymap JSON defition is stored within the keyboard firmware and is retrieved at runtime.

Vial implements several additional quality-of-life features that are documented in the topics linked below.

![](img/vial-linux.png)

## Documentation topics

* [Porting a keyboard to VIA](/gettingStarted/porting-to-via.md)
* [Porting a VIA keyboard to Vial](/gettingStarted/porting-to-vial.md)
* [Implementing Vial encoder support](gettingStarted/encoders.md)
* [Vial security features and options](/security)
