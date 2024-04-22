---
title: My Gnome setup
date: 2024-01-22 10:30:00 
categories: blogging 
tags: linux gnome extensions desktop     # TAG names should always be lowercase
---

Meine Standard-Desktopumgebung ist immernoch Gnome, da ich aus beruflichen Gründen Ubuntu nutze und ich damit auch mehr oder weniger zufrieden bin. Ich mag es, wenn ein System stabil läuft, ich aber trotzdem Möglichkeiten der Anpassung habe. Für alle Minimalisten, die jetzt wieder mit Arch-Linux kommen, die können ja gern dabei bleiben ;)

Ich bleibe erstmal bei einer Distro, die nicht super viel Aufwand in der Konfiguration benötigt und die trotzdem gut aussieht und mit der ich produktiv arbeiten kann. Da mir Gnome auch ganz gut gefällt und man sehr nah an dem Apple-look ist, aber gleichzeitig mannigfaltige Konfigurationen und Anpassungen hat, bleibe ich dabei! In diesem Artikel werde ich meine Anpassungen an der Umgebung dokumentieren und anderen zur Verfügung stellen! Have fun!

![Terminal](/assets/img/neofetch.png)

![Desktop Überblick](/assets/img/desktop.png)

## Vanilla Gnome statt Ubuntu-Desktop

Ich bevorzuge immer die Standard-Gnome-Umgebungen (auch bekannt als vanilla-gnome) und nicht die angepasst Ubuntu-Desktop-Version. Deswegen steigen wird direkt mal um auf das barbone Gnome!

Dazu kann man folgende Gnome-Pakete installieren:

```bash
sudo apt install vanilla-gnome-desktop vanilla-gnome-default-settings
```

Wenn man will, kann man dann noch den Ubuntu-Desktop entfernen. Dazu dient folgender Befehl:

```shell
sudo apt purge ubuntu-desktop
```

Warum nicht `remove`? Nun da purge auch die `config`files mitlöscht! Im Anschluss kann man dann auch noch die abhängigen Bibliotheken löschen! Wenn auch alle abhängigen Bibliotheken mit gelöscht werden sollen, die an den gelöschten Paketen hängen, dann kann noch `autoremove` durchgeführt werden. Auch hier kann `--purge` angehängt werden, wenn die assozierten configuration-files mit entfernt werden sollen.

```shell 
sudo apt autoremove (--purge)
```
## Erweiterungen

Gnome kann durch zahlreiche Erweiterungen verändert werden. Dazu benötigt man aber erst einmal den [Extension-Manager](https://github.com/mjakeman/extension-manager) der via [flatpak](https://www.flatpak.org/setup/Ubuntu) installiert werden kann (Der zweite Link führt zur Homepage auf der beschrieben wird, wie flatpak unter Ubuntu aufgesetzt wird, falls ihr das noch nicht gemacht habt). 

Ihr könnt dann den Extension-Manager installieren:
```shell
flatpak install flathub com.mattjakeman.ExtensionManager
```

Damit könnt ihr nun nach Extensions für Gnome suchen, ohne das ihr das im (nervigen) Browser machen müssten (kudos an https://mattjakeman.com/)!

Hier nun eine kurze Liste der Erweiterungen, die ich derzeit nutze: 
- [Astra Monitor](https://github.com/AstraExt/astra-monitor)
- [Blur my shell](https://github.com/aunetx/blur-my-shell)
- [ddterm](https://github.com/ddterm/gnome-shell-extension-ddterm)
- [AATWS](https://github.com/G-dH/advanced-alttab-window-switcher) 
- [Gnome 4x Overview UI Tune](https://github.com/axxapy/gnome-ui-tune) 

## zsh + powerlevel10k

Ich nutzte derzeit [oh my zsh](https://ohmyz.sh/) als mein Terminal mit [powerlevel10k](https://github.com/romkatv/powerlevel10k?tab=readme-ov-file#configuration-wizard), um es noch etwas schöner zu machen. `Oh my zsh` wird via `curl` oder `wget` installiert. Was es genau macht, seht ihr ja selbst im Befehl - es lädt ein shell-script herunter und führt es mittels `sh -c` aus.
Das Argument `-c` macht dabei folgendes:

```shell
-c              Read commands from the command_string operand instead of from 
				the standard input.  Special parameter 0 will be set from the 
				command_name operand and the positional parameters ($1, $2, 
				etc.)  set from the remaining argument operands.
```

curl:

```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

wget:

```shell
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

Danach installieren wird noch `powerlevel10k`

```shell
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

`p10k` wird mit folgendem Befehl konfiguriert, sollte aber nach Installation und Neustart des Terminals von alleine passieren!:

```shell
p10k configure
```

## Window ready - annoyance

Wenn `Fenster bereit` nervt und das Fenster nicht in den Fokus gerückt wird, dann kann man folgenden Befehl ausführen. Damit werden Fenster aus dem Kontext heraus in denn Focus gesetzt. Man kann als Parameter auch `strict` setzen, dann werden die Fenster immer in den Vordergrund gesetzt.

ACHTUNG: Bei mir funktioniert das mit Gnome 45 derzeit nicht

```shell
gsettings set org.gnome.desktop.wm.preferences auto-raise 'true'
gsettings set org.gnome.desktop.wm.preferences focus-new-windows 'smart'
```
or

```shell
gsettings set org.gnome.desktop.wm.preferences focus-new-windows 'strict'`
```

