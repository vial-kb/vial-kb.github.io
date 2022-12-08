---
layout: default
title: Setting up your development environment
parent: Porting guide
nav_order: 10
redirect_from:
  - /vial-qmk-setup.html
  - /vial-qmk-setup/
---

# Setting up your Vial development environment

You probably want to have BOTH the QMK development environment setup as well as the Vial version of it, at the end of this guide. Mainly since whatever keyboard you work with is likely present in QMK, 
and it's always a great idea to be able to compile and test the QMK source, simply to verify that it is infact working with latest version etc. before you spend effort porting it to Vial. Or, if you are 
infact creating a new firmware from scratch for a keyboard you yourself have designed, it will likely need both QMK and Vial support in the end.

And since you are perhaps planning on making changes to the source, beyond *just* the keymaps, it's highly recommended to fork the QMK main Git, and have version handling on your own edits.

## Prerequisite

* 	A basic knowledge in working in a command prompt. (The QMK guide below links to applicable guides.)
* 	A working QMK development environment.
	* 	Follow [QMK's guide](https://docs.qmk.fm/#/newbs_getting_started?id=setting-up-your-qmk-environment) and pick your OS.
	*	It's highly recommended to follow the 'advanced' [instructions](https://docs.qmk.fm/#/getting_started_github) and create your own fork of QMK (and of Vial).
	

## Cloning the Vial-QMK Git

To create the folder tree for Vial-QMK, it is far better to use Git tools to clone the folder, including all the tools/files needed, than download a .zip and then have to add the tools on top afterwards.

Start in your home folder and enter the following command:
```git clone https://github.com/vial-kb/vial-qmk/ ```

This creates the folder tree for Vial-QMK, and the next step is to 'install' or setup the Vial-QMK. Issue this command **inside** the Vial-QMK main folder. 
This does the same thing as in 'vanilla' QMK, and creates the links, PATH variables etc.
```qmk setup``` or with a forked vial-QMK ```qmk setup <github_username>/vial-qmk```
Followed by:
```make git-submodule```


> Important
> {: .label .label-red }
>Here is when things differ from with 'vanilla' QMK.

If you issue the normal compile command, as in the QMK guide:
```qmk compile -kb <keyboard> -km default```
You are infact still using 'vanilla' QMK, as the global PATH variable means you are compiling using QMK's framework, in the folder structure of QMK, ie the folders under /qmk-firmware/keyboard/

This is why you issue the 'make' command instead. And this agin have to be done **inside** the Vial-QMK main folder, otherwise it simply will not work.
```qmk make -kb <keyboard> -km vial```

Now, that you have set up your Vial environment succesfully, back to the [porting guide](http://https://get.vial.today/docs/porting-to-vial.html)!
