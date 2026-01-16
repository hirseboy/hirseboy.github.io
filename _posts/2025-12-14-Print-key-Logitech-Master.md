---
title: Fixing Logitech Master 3S printing key with Linux with solaar  
date: 2025-12-13 12:00:00 
categories: linux 
tags: logitech keyboard solaar print 
---

I ran into the same on Fedora. First make sure you have [Solaar](https://github.com/pwr-Solaar/Solaar) installed.

- Then, in Solaar, select the keyboard in the left column.

![Devices overview](/assets/img/print-keyboard-1.png)

- In the right column, click the padlock icon for `Key/Button Diversion` until it is unlocked.

![Unlock key redirection](/assets/img/print-keyboard-2.png)

- In the dropdown, select `Screenshot` and change `Regular` to `Diverted`.
- Click the padlock icon to lock it again.
- Click the `Rule Editor` button in the lower right of Solaar.
- Under `User-defined rules`, right-click to insert a new rule.
- Right-click the new rule, and select `Condition` -> `Key`
- Specify `Screenshot` as the key, keeping `Key down` selected.
- Right-click again, and `Insert below` -> `Action` -> `Key press`
- Specify `Print` as they key

![Set the new print key](/assets/img/print-keyboard-3.png)

Make sure that the `Key press` action is after / below the `Screenshot (pressed)` condition, and save the changes.

This maps the `Screenshot` key (F7 on my MX Mechanical) to the Print Screen button, and that in turn fires the Ubuntu screenshot tool.

I have noticed that by default, that button emulates a left-shift + opt / start + s key combination, which doesn't do anything on Ubuntu 22.04.