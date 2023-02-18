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


Vial is a completely open source project, with sources for all components publicly available on [GitHub](https://github.com/vial-kb).

Vial is decentralized: with Vial you do ***not*** have to submit your keyboard as a pull-request to any third-party repositories before it can be used in the GUI; instead, the keymap JSON definition is stored within the keyboard firmware and is retrieved at runtime. 

In order for a keyboard to work with Vial, Vial-compatible firmware must be flashed onto the microcontroller. 

> Note
> {: .label .label-blue }
> Firmware built for VIA is not the same as firmware built for Vial. While older versions of VIA firmware were partially-compatible with the Vial GUI, recent versions are not.

Please ask the vendor of your keyboard for binaries and/or source code for the keyboard firmware. Vendors are not required to make the source code to a keyboard using Vial public, but it is ***highly encouraged*** since it allows the end-users and community to diagnose the firmware and keyboard and add/subtract features as they are developed. User are ancouraged to in a ***friendly and courteous manner*** remind vendors of this.

If not: in many cases, if the QMK-based source code is available for your keyboard you can [create your own](https://get.vial.today/docs/porting-to-via.html). Don't forget to double-check [the Vial keyboard repository](https://github.com/vial-kb/vial-qmk); a user-submitted keymap may already be there.

Have a feature suggestion for Vial? Feel free to submit it at the dedicated [feedback website](https://feedback.vial.today/).

![](img/vial-win-1.png)

Remember, Vial is coded and documented by end users volunteering their time and efforts, so while we all very much appriciate your feedback and input, please respect that your exact ideas may not be the highest priority to include at any given moment. 

The first and foremost important priority of the project is to maintain a stable and updated tool that is compatible with the main QMK repository. Adding new features always comes second to this.
