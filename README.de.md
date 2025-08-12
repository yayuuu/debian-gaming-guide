# Debian Gaming - Anleitung
[![en](https://img.shields.io/badge/lang-en-red.svg)](README.md)
[![pl](https://img.shields.io/badge/lang-pl-red.svg)](README.pl.md)
[![zh](https://img.shields.io/badge/lang-zh-red.svg)](README.zh.md)
[![es](https://img.shields.io/badge/lang-es-red.svg)](README.es.md)
[![hi](https://img.shields.io/badge/lang-hi-red.svg)](README.hi.md)
[![pt](https://img.shields.io/badge/lang-pt-red.svg)](README.pt.md)
[![ru](https://img.shields.io/badge/lang-ru-red.svg)](README.ru.md)
[![fr](https://img.shields.io/badge/lang-fr-red.svg)](README.fr.md)
[![ja](https://img.shields.io/badge/lang-ja-red.svg)](README.ja.md)
## Schritt 1 - Installation
1. Lade das Festplatten-Image herunter: https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-13.0.0-amd64-netinst.iso
2. Erstelle ein bootfähiges USB-Laufwerk. Du kannst Programme wie Rufus oder Etcher verwenden. Auf einigen älteren Plattformen kann es vorkommen, dass das System auch nach dem Erstellen eines bootfähigen USB-Laufwerks mit einer dieser Anwendungen nicht startet. Als letzten Ausweg kannst du unetbootin (Linux) verwenden.
3. Während der Installation fragt der Installer nach dem Root-Passwort – **LASS DIESES FELD LEER!**
4. Erstelle den Hauptbenutzer des Systems, indem du einen Benutzernamen und ein Passwort angibst.
5. Bei der Auswahl der Pakete, die Debian zu Beginn installieren soll, wähle deine bevorzugte Desktop-Umgebung. Ich empfehle KDE Plasma, aber wenn du weißt, was du tust, kannst du auch eine andere auswählen.

## Schritt 2 - Nvidia-Treiber (kann übersprungen werden, wenn du keine Nvidia-Karte hast)
Öffne das Terminal und führe die folgenden Befehle aus:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get install -y nvidia-open #für RTX2000-Serie oder neuer
sudo apt-get install -y cuda-drivers #für GTX1000-Serie oder älter
```

## Schritt 3 - Flatpak
Flatpak ist ein universelles Softwareverteilungssystem für Linux. Durch das Einrichten des Flatpak-Repositorys kannst du viele nützliche Anwendungen direkt aus dem integrierten Store installieren.
```
sudo apt install flatpak
sudo apt install plasma-discover-backend-flatpak #wenn du KDE Plasma benutzt
sudo apt install gnome-software-plugin-flatpak #wenn du Gnome benutzt
flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Schritt 4 - Backports
Das Backports-Repository ermöglicht es dir, bestimmte Pakete in der stabilen Debian-Version zu aktualisieren. Wichtige Pakete, die aktualisiert werden sollten, sind Kernel, mesa, pipewire und flatpak.
```
echo "deb http://deb.debian.org/debian trixie-backports main" | sudo tee /etc/apt/sources.list.d/backports.list
sudo apt update
```

Um ein Paket aus dem Backports-Repository zu installieren, verwende:
```
sudo apt install -t trixie-backports <paket>
```

Kernel-Update:
```
sudo apt install -t trixie-backports linux-headers-amd64 linux-image-amd64
```

Mesa-Update:
```
sudo apt install -t trixie-backports libegl-mesa0
```

Ebenso kannst du flatpak oder pipewire aktualisieren, indem du `<paket>` durch flatpak oder pipewire ersetzt.

**Hinweis:** Stand heute (11.08.2025) gibt es noch keine neueren Versionen dieser Pakete in Backports. Liste verfügbarer Pakete: https://packages.debian.org/trixie-backports/
