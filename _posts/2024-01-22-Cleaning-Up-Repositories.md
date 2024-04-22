---
title: Cleaning up apt repositories   
date: 2024-01-22 10:30:00 
categories: news blogging 
tags: apt repositories     # TAG names should always be lowercase
---

# How to clean repositories?
- `apt clean` → cleans the packages and install script in /var/cache/apt/archives/
- `apt autoclean` → cleans obsolete deb-packages, less than clean
- `apt autoremove` → removes orphaned packages which are not longer needed from the system, but not purges them, use the `--purge` option together with the command for that.


> ##### WARNING
>
> `--purge` removes also the configuration files, so be careful!
{: .block-warning }