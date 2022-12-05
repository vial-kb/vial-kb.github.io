---
layout: default
title: VIAL or VIA, what is the difference?
parent: User manual
nav_order: 9
redirect_from:
  - /gettingStarted/vial-via.html
  - /getting-started/vial-via.html
---


# VIAL or VIA, what is the difference, they both work the same?

> Important
> {: .label .label-red }
> No, Vial and VIA are NOT the same. They both aim to do roughly the same, and they both originated from QMK in the beginning, but they are in fact two separate entities, with separate functions. 
The fact that your VIA keyboard shows up in VIAL, does NOT infact mean you are 'running Vial firmware'.

## 1. But my keyboard manufacturer/seller/(?) said its VIA and VIAL compatible!

Well, VIAL uses some of the same protocol as VIA does, and infact many VIA compatible keyboards will show up in Vial and work to some extent, ie you can remap keys. 
This is called VIA compatibility mode, and means you have *limited* functionality.

However, when either VIA or Vial is updated and new features are added, these may or may not be carried over to the other. 

The fact that your keyboard is VIA compatible or works in VIA does not magically mean it's Vial compatible. And it especially does NOT mean that it supports specific Vial functions.
To support VIAL and take advantage of all of Vial's features, your keyboard needs to run a native VIAL firmware, specifically compiled for Vial, and flashed to the keyboard.


## 2. How do I know for sure if my keyboard is running native VIAL or in VIA compatability mode?

If the VIAL app, open the 'About' meny, and open the information about your keyboard. If it says 'VIA protocol: 9' ONLY, the keyboard is infact running a VIA firmware in compatability mode, and with limited functions.

```VIA protocol: 9```
 
 If the information however says VIA and Vial protocol, and displays a Vial ID, the keyboard is running a native Vial firmware, and have access to Vial only functions.
 
```VIA protocol: 9
Vial protocol: 5
Vial keyboard ID: 59B215D1919C0574```


### Side loading a .JSON file

Yes, you can sideload keyboard defenitions in .JSON files to get the keyboard working in Vial, but it still only means it's in VIA compatability mode. 
You will need to go through the porting procedure to have the full benefits of Vial.
 
[Port your keyboard](http://https://get.vial.today/docs/porting-to-via.html).

