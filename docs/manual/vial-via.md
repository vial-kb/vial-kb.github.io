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
> No, Vial and VIA are NOT the same. They both aim to do roughly the same, and they both work sort of the same for the end user.
And yes, they both originated from QMK in the beginning, and is sort of working as a layer on top of QMK. But they are in fact two separate entities with separate functions, being developed by different sets of people. 
The fact that your VIA keyboard shows up in VIAL (in some instances) and you can remap basic keys, does NOT infact mean you are 'running Vial firmware'. 
There is a vast difference between the app or web-app on your computer, and the firmware on your keyboard.

## But my keyboard manufacturer/seller/(?) said its VIA and VIAL compatible!

Well, VIAL uses some of the same protocol as VIA does, and infact many VIA compatible keyboards (up until VIA protocol 9) will show up in Vial and work to some extent, ie you can remap basic keys. 
This is called VIA compatibility mode, and means you have *limited* functionality. To find out if your keyboard is infact in compatability mode, check the VIAL app, open the 'About' menu, and select 
your keyboard to show the information about it. 

If it says 'VIA protocol: 9' ONLY, the keyboard is infact running a VIA firmware in compatability mode, and with limited functions.

```VIA protocol: 9```
 
 If the information however says VIA and Vial protocol, and displays a Vial ID, the keyboard is running a native Vial firmware, and have access to Vial only functions.
 
```VIA protocol: 9
Vial protocol: 5
Vial keyboard ID: 59B215D1919C0574```

### Side loading a .JSON file

Yes, you can sideload keyboard defenitions in .JSON files to get the keyboard working in Vial, but it still only means it's in VIA compatability mode. 
You will need to go through the porting procedure to have the full benefits of Vial.
 
[Port your keyboard](http://https://get.vial.today/docs/porting-to-via.html).

