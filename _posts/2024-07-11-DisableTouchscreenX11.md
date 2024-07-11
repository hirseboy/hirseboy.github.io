---
title: Disable touchscreen on Ubuntu
date: 2024-07-11 10:30:00 
categories: blogging 
tags: ubuntu xinput touchscreen     # TAG names should always be lowercase
---

![Terminal](/assets/img/xinput.png)

You can show a list with all input devices via

```shell 
xinput list
```

then you simply choose the device you want to disable - in our case it is:

```shell
⎜   ↳ Wacom Pen and multitouch sensor Finger touch	id=11	[slave  pointer  (2)]
```

To disable this device you just use `disable` with the specific ID:

```shell
xinput disable 11
```

