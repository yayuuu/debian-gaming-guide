# Debian Gaming - Guide

[![pl](https://img.shields.io/badge/lang-pl-red.svg)](README.pl.md)
[![zh](https://img.shields.io/badge/lang-zh-red.svg)](README.zh.md)
[![es](https://img.shields.io/badge/lang-es-red.svg)](README.es.md)
[![hi](https://img.shields.io/badge/lang-hi-red.svg)](README.hi.md)
[![pt](https://img.shields.io/badge/lang-pt-red.svg)](README.pt.md)
[![ru](https://img.shields.io/badge/lang-ru-red.svg)](README.ru.md)
[![de](https://img.shields.io/badge/lang-de-red.svg)](README.de.md)
[![fr](https://img.shields.io/badge/lang-fr-red.svg)](README.fr.md)
[![ja](https://img.shields.io/badge/lang-ja-red.svg)](README.ja.md)
1. Download the disk image: https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-13.0.0-amd64-netinst.iso
2. Create a bootable USB drive. You can use applications like Rufus or Etcher. On some older platforms, even after creating a bootable USB with one of these applications, the system may still fail to boot. As a last resort, you can use unetbootin (Linux).
3. During installation, the installer will ask for the root password - LEAVE THIS FIELD EMPTY!
4. Create the system's main user by providing a username and password.
5. When choosing which packages Debian should install at the beginning, select your favorite desktop environment. I suggest KDE Plasma, but if you know what you're doing, you can choose another.

## Step 2 - Nvidia Drivers (you can skip if you don’t have an Nvidia card)
Open the terminal and run the following commands:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get install -y nvidia-open #for RTX2000 series cards or newer
sudo apt-get install -y cuda-drivers #for GTX1000 series cards or older
```

## Step 3 - Flatpak
Flatpak is a universal software distribution system for Linux. By setting up the Flatpak repository, you gain the ability to install many useful applications directly from the system’s built-in store.
```
sudo apt install flatpak
sudo apt install plasma-discover-backend-flatpak #if using KDE Plasma
sudo apt install gnome-software-plugin-flatpak #if using Gnome
flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Step 4 - Backports
The backports repository allows you to update certain packages on Debian’s stable version. Key packages worth updating include kernel, mesa, pipewire, and flatpak.
```
echo "deb http://deb.debian.org/debian trixie-backports main" | sudo tee /etc/apt/sources.list.d/backports.list
sudo apt update
```

To install a package from the backports repository, use the following command:
```
sudo apt install -t trixie-backports <package>
```

Kernel update:
```
sudo apt install -t trixie-backports linux-headers-amd64 linux-image-amd64
```

Mesa update:
```
sudo apt install -t trixie-backports libegl-mesa0
```

Similarly, to update flatpak or pipewire, replace `<package>` with flatpak or pipewire.

**Note:** As of today (11.08.2025), there are no newer versions of these packages in backports yet. A list of packages available for update can be found here: https://packages.debian.org/trixie-backports/

