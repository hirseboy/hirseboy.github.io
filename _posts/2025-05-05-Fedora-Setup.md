---
title: Switching to Fedora 42  
date: 2025-04-12 15:42:00 
categories: news blogging 
tags: fedora gnome flatpak     # TAG names should always be lowercase
---

# Fedora Installation Tutorial

We are using **Fedora 42** with GNOME (not KDE). You can download Fedora from the official [website](https://fedoraproject.org/workstation/).  
**Note:** Fedora 42 uses **Wayland only** – X11 support has been removed. This can cause issues with **Nvidia GPUs**, such as low frame rates or external monitor problems.  
So far, support has been solid. By default, the system and applications run on the integrated GPU, and you can easily launch programs with the dedicated GPU.  
Previously, I had to use `prime select <nvidia|intel>`, which also heavily drained the battery in Nvidia mode.

> This guide will be updated continuously.

## RPM Package Manager

Some useful `rpm/dnf` commands for those used to `apt`:

```sh
sudo dnf install <program>            # Install packages
sudo dnf reinstall <program>          # Reinstall packages
sudo dnf upgrade                      # Upgrade all packages
sudo dnf remove <package>             # Remove packages
```

## Flatpak

We use **Flatpak** for most application installations.

### Add Flathub

```sh
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

### Install applications

```sh
flatpak install flathub im.riot.Riot
flatpak install flathub com.visualstudio.code
flatpak install flathub com.syntevo.SmartGit
flatpak install flathub com.mattjakeman.ExtensionManager
flatpak install flathub org.gnome.World.PikaBackup
flatpak install flathub com.nextcloud.desktopclient.nextcloud
flatpak install flathub io.qt.QtCreator
flatpak install flathub org.keepassxc.KeePassXC
flatpak install flathub org.mozilla.firefox
flatpak install flathub com.brave.Browser
flatpak install flathub org.kde.okular
```

> Note: Okular automatically used my signing certificate. If not, go to `Settings > Configure Backends > PDF` and select the certificate database from Firefox/Thunderbird using the `NSS` module.
{: .prompt-info }

![Okular with certificate for signing PDFs](/assets/img/fedora-certificate.png)

### Optional: VSCodium (Open Source VSCode)

```sh
flatpak install flathub com.vscodium.codium
```

## UI Customization

### Icon Theme: Colloid

Install the [Colloid Icon Theme](https://github.com/vinceliuice/Colloid-icon-theme):

```sh
git clone https://github.com/vinceliuice/Colloid-icon-theme
cd Colloid-icon-theme
./install.sh -d ~/.local/share/icons
```

Switch theme using `gnome-tweaks`.

### GNOME Tweaks

```sh
sudo dnf install gnome-tweaks
```

With gnome-tweaks you can reenable the minimize and maximize buttons of the windows. For this open `tweaks` and go to `Window` and then enable `minimize` and `maximize`.

![Gnome tweaks with enabling min/max buttons](/assets/img/fedora-gnome-tweaks.png)


### GNOME Extensions

Use [Extension Manager](https://flathub.org/apps/com.mattjakeman.ExtensionManager) to install GNOME extensions.

Recommended extensions:

- Astra Monitor / TopHat (shows CPU temperature)
- [Blur My Shell](https://extensions.gnome.org/extension/3193/blur-my-shell/) – modern look
- Dash to Dock (or alternatives)
- [AATWS (Alt-Tab Switcher)](https://extensions.gnome.org/extension/4412/advanced-alttab-window-switcher/)
- Weather or Not – weather in top bar

## Geany with Dark Mode (Flatpak UI Theme)

```sh
flatpak install org.gtk.Gtk3theme.Adwaita-dark
flatpak override --user --env=GTK_THEME=Adwaita:dark org.geany.Geany
flatpak info --show-permissions org.geany.Geany
```

You can also set the variable using Flatseal:

```ini
GTK_THEME=Adwaita:dark
```

![Flatseal with environement variables  ](/assets/img/fedora-flatseal.png)

## Programming

### Qt & Qt Creator

Install Qt5:

```sh
sudo dnf install qt5-*-devel
sudo dnf install qt-creator
sudo dnf install mesa-libGLU-devel
```

> `qt5-*-devel` installs all Qt5 development packages. Use carefully!
{: .prompt-warning }

Optional Qt6:

```sh
sudo dnf install qt6-qtbase-devel qt6-qttools-devel
```

#### Qt Creator Launch Options for NVIDIA

Under `Projects > Run > Environment`:

```sh
QT_QPA_PLATFORM=xcb
__NV_PRIME_RENDER_OFFLOAD=1
__GLX_VENDOR_LIBRARY_NAME=nvidia
```

This ensures proper rendering with XWayland and Nvidia, fixing misaligned UI elements.

### C++ / Compiler / Tools

```sh
sudo dnf install gcc-c++
sudo dnf install libstdc++-static
sudo dnf install cmake
sudo dnf install git clang make gdb
```

## OpenModelica

```sh
sudo dnf config-manager addrepo --from-repofile=https://build.openmodelica.org/rpm/fc41/omc.repo
sudo dnf install openmodelica-nightly
```

## EduVPN

```sh
curl -O https://app.eduvpn.org/linux/v4/rpm/app+linux@eduvpn.org.asc
sudo rpm --import app+linux@eduvpn.org.asc

cat << 'EOF' | sudo tee /etc/yum.repos.d/python-eduvpn-client_v4.repo
[python-eduvpn-client_v4]
name=eduVPN for Linux 4.x (Fedora $releasever)
baseurl=https://app.eduvpn.org/linux/v4/rpm/fedora-$releasever-$basearch
gpgcheck=1
EOF

sudo dnf install eduvpn-client
rm app+linux@eduvpn.org.asc  # Optional cleanup
```

## Nvidia Driver

### Option 1: RPMFusion

```sh
sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install akmod-nvidia
sudo dnf install xorg-x11-drv-nvidia-cuda
```

### Option 2: Manual (Not recommended)

Alternative method [here](https://github.com/oddmario/NVIDIA-Fedora-Driver-Guide) (⚠️ not tested).

## Migrating from Snap to Flatpak

Example: Migrate Thunderbird settings

```sh
mkdir -p ~/.var/app/org.mozilla.Thunderbird/.thunderbird
cp -r ~/snap/thunderbird/common/.thunderbird/* ~/.var/app/org.mozilla.Thunderbird/.thunderbird/
```

## Backups

### Pika Backup (via Flatpak)

```sh
flatpak install flathub org.gnome.World.PikaBackup
```

> Simple and secure incremental backups with encryption.

## Fixing Missing Icons in DashtoDock / AATWS

If a desktop application's icon does **not** appear in **Dash to Dock**, it is usually due to a missing `StartupWMClass` entry in the application's `.desktop` file.

### Step 1: Find the correct `WM_CLASS` using LookingGlass

Launch LookingGlass with `Alt+F2`, then type `lg` and press Enter.  
A debug window will appear.

1. Go to the `Windows` tab.
2. Find the running application in the list.
3. Copy the exact value of `wmclass`.

You will use this value in your `.desktop` file as `StartupWMClass`.

![LookingGlass Screenshot](/assets/img/fedora-lg.png)

### Step 2: Update the `.desktop` file

Locate or create the `.desktop` file in `~/.local/share/applications`.

Example:

```ini
[Desktop Entry]
Name=License Manager
Comment=Building Energy Performance and District Simulation
Exec=/run/media/hirth/Daten/Git/VICUS/LizenzManager/bin/release/LicenseManager
Icon=/run/media/hirth/Daten/Git/VICUS/LizenzManager/LicenseManager/resources/gfx/Logo.svg
Terminal=false
Type=Application
Categories=Science
StartupNotify=true
StartupWMClass=LicenseManager
```

### What does `StartupWMClass` do?

The `StartupWMClass` entry connects the application's window to the correct icon in the dock.  
It is **essential** for proper icon display when using Dash to Dock or similar extensions.

---

## Notes (so far) for Fedora 42 on ThinkPad X1 Extreme Gen 5

- Hardware compatibility is very good  
- For more stable Nvidia support, consider disabling hybrid graphics in BIOS  
- Fedora 42 runs smoothly on Wayland, but some older apps/games may still need XWayland  
- Wayland still kinda slow, but ok
