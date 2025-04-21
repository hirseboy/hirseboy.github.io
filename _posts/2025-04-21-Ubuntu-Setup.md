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


## Dymola

Dymola can be downloaded [here](https://www.ltx.de/download/Dymola/Dymola2025x.html).

Setting up the license for TU Dresden:

Server: licenses.zih.tu-dresden.de
FlexLM-Port: 1277
Vendor-Daemon-Port: 27577


## flatpak

```shell
flatpak install flathub com.github.tchx84.Flatseal -y
flatpak install flathub com.jetbrains.PyCharm-Community -y
flatpak install flathub com.mattjakeman.ExtensionManager -y
flatpak install flathub im.riot.Riot -y
flatpak install flathub io.github.mimbrero.WhatsAppDesktop -y
flatpak install flathub md.obsidian.Obsidian -y
flatpak install flathub org.freecad.FreeCAD -y
flatpak install flathub org.gimp.GIMP -y
flatpak install flathub org.gnome.Evolution -y
flatpak install flathub org.gnome.Fractal -y
flatpak install flathub org.gnome.Shotwell -y
flatpak install flathub org.gnome.World.PikaBackup -y
flatpak install flathub org.kde.kcachegrind -y
flatpak install flathub org.kde.krita -y
flatpak install flathub org.kde.okular -y
flatpak install flathub org.ksnip.ksnip -y
flatpak install flathub org.librecad.librecad -y
flatpak install flathub org.telegram.desktop -y
flatpak install flathub us.zoom.Zoom -y
```
