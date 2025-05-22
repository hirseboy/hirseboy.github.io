---
title: Setting up ubuntu   
date: 2025-04-12 15:42:00 
categories: news blogging 
tags: ubuntu setup qt qtceator     # TAG names should always be lowercase
---

# Setting up Ubuntu

This posts is mainly for the purpose of documenting the setup of a clean Ubuntu. I am using a clean Ubuntu Version 24.04.2. Please update your system first.

```shell
sudo apt update && sudo apt upgrade
```

# Software 

## Qt

To install all qt specific modules run the following command with apt

```shell
sudo apt install qtbase5-dev qt5-qmake libqt5svg5-dev libqt5sql5 libqt5sql5-psql qtdeclarative5-dev qtlocation5-dev qtpositioning5-dev qml-module-qtlocation qml-module-qtpositioning
``` 

> ##### MIND
>
> Since we use some QML Features in our software, we also have to install the qml and location modules. 
> 
{: .block-warning }

## Build tools for c++

To install all needed build-tools for complining applications with gcc an c++ install the following packages:

```shell
sudo apt install build-essential g++ cmake
```

## SSH

To connect to other machines via SSH and mount remote filesystems, install the following packages:

```bash
sudo apt install openssh-client sshfs
```

> #### MIND
>
>   openssh-client: Provides the SSH client tools (ssh, scp, sftp) for connecting to remote systems.
>   sshfs: Allows you to mount remote filesystems over SSH using FUSE.
>

If you also want to allow incoming SSH connections to your machine (e.g., for remote access), install the SSH server as well:

```bash
sudo apt install openssh-server
```

## Dymola

Dymola can be downloaded [here](https://www.ltx.de/download/Dymola/Dymola2025x.html).

Setting up the license for TU Dresden:

Server: licenses.zih.tu-dresden.de
FlexLM-Port: 1277
Vendor-Daemon-Port: 27577


## flatpak

```shell
flatpak install flathub com.github.tchx84.Flatseal 
flatpak install flathub com.jetbrains.PyCharm-Community 
flatpak install flathub com.mattjakeman.ExtensionManager 
flatpak install flathub im.riot.Riot 
flatpak install flathub md.obsidian.Obsidian 
flatpak install flathub org.gimp.GIMP 
flatpak install flathub org.gnome.Shotwell 
flatpak install flathub org.gnome.World.PikaBackup 
flatpak install flathub org.kde.okular 
flatpak install flathub org.telegram.desktop 
flatpak install flathub us.zoom.Zoom 
```
