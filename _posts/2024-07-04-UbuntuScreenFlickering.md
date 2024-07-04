---
title: Screen flickering on Ubuntu
date: 2024-04-23 10:30:00 
categories: blogging 
tags: ubuntu bug intel     # TAG names should always be lowercase
---

The screen flickerung is coming from Panel Self Refresh (PSR), a power saving feature used by Intel iGPUs which is known to cause flickering in some instances. A temporary solution is to disable this feature using the [kernel parameter 364](https://wiki.archlinux.org/title/Kernel_parameter) `i915.enable_psr=0`. Here is how you can do It:

Edit the grub file:

```shell 
sudo nano /etc/default/grub
```

and add  to the end of the `GRUB_CMDLINE_LINUX_DEFAULT` line

```shell
“i915.enable_psr=0
```

then run:

```shell
sudo update-grub
```

to apply those changes and reboot.
