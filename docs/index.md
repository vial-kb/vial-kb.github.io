---

layout: home
title: Home
nav_order: 1
---

# Vial
{: .my-1 }
### **Vial is an open-source cross-platform (Windows, Linux and Mac) GUI and a QMK fork for configuring your keyboard in real time.**
{: .mt-1 .mb-8 .text-grey-dk-100 .line-height-fix }

[Start Vial Web](https://vial.rocks/){: .btn .gettingStarted .blue target="_blank"}
[Download Vial](/download){: .btn .gettingStarted .blue}
[Read user manual](/manual/){: .btn .gettingStarted}
[Join our Discord server](https://discord.gg/zNKEUXTKwF){: .btn .gettingStarted}


Vial is a completely open project, with sources for all components publicly available on [GitHub](https://github.com/vial-kb).

Vial is decentralized: with Vial you do not have to submit your keyboard as a pull-request to any third-party repositories before it can be used in the GUI; instead, the keymap JSON definition is stored within the keyboard firmware and is retrieved at runtime.

## Is my keyboard compatible with Vial?

In order for a keyboard to work with Vial, it needs to have either via firmware or vial firmware flashed onto the microcontroller. This can be done easily if the keyboard has already been added to the [qmk keyboard repository](https://github.com/qmk/qmk_firmware/tree/master/keyboards).

### Where can I find Vial firmware?

For some keyboards, firmware has already been built and can be found [here](https://keyboard.gay/). However, most qmk-compatible keyboards do not have vial-compatible firmware and users must build this firmware themselves to make a keyboard vial-compatible. A guide to do this is [here](https://get.vial.today/docs/porting-to-via.html).

### How can I flash firmware onto my keyboard?

QMK has an excellent guide [here](https://docs.qmk.fm/#/newbs_flashing).

### [Ready to use Vial?](https://get.vial.today/manual/first-use.html)

Have a feature suggestion for Vial? Feel free to submit it at the dedicated [feedback website](https://feedback.vial.today/).

![](img/vial-win-1.png)
