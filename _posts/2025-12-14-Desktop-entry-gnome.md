---
title: Fixing broken icons in gnome (Dash)  
date: 2025-12-13 12:00:00 
categories: linux 
tags: gnome desktop  
---

# Fixing broken icons in gnome (Dash2Dock, etc.)

If the icon of a desktop application does not appear in Dash2Dock, it is due to a missing `StartupWMClass` entry in the `*.desktop` file. Use Looking Glass to find the correct name of the application.

Start Looking Glass via `Alt+F2`, then type `lg`, which will open a window. In this window, go to `Windows` and search for the exact application, copy the `wmclass` name, and enter it in the desktop file as `StartupWMClass=LicenseManager`.

![looking glass entry](/assets/img/looking-glass.png)

Then update the desktop file in `~/.local/share/applications` 

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

`StartupWMClass=` → Connects the window with the icon in the dock (very important!)