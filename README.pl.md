# Debian Gaming - poradnik
[![en](https://img.shields.io/badge/lang-en-red.svg)](README.md)
[![zh](https://img.shields.io/badge/lang-zh-red.svg)](README.zh.md)
[![es](https://img.shields.io/badge/lang-es-red.svg)](README.es.md)
[![hi](https://img.shields.io/badge/lang-hi-red.svg)](README.hi.md)
[![pt](https://img.shields.io/badge/lang-pt-red.svg)](README.pt.md)
[![ru](https://img.shields.io/badge/lang-ru-red.svg)](README.ru.md)
[![de](https://img.shields.io/badge/lang-de-red.svg)](README.de.md)
[![fr](https://img.shields.io/badge/lang-fr-red.svg)](README.fr.md)
[![ja](https://img.shields.io/badge/lang-ja-red.svg)](README.ja.md)
## Krok 1 - instalacja
1. Pobierz obraz dysku: https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-13.0.0-amd64-netinst.iso
2. Utwórz bootowalny dysk USB. Możesz użyć takich aplikacji jak Rufus lub Etcher. W przypadku niektórych starszych platform może się zdarzyć, że po utworzeniu bootowalnego USB jedną z tych aplikacji, nadal nie da zbootować systemu. Jako ostatnią deskę ratunku można użyć unetbootin (linux).
3. Podczas instalacji, instalator będzie pytał o podanie hasła roota - POZOSTAW TO POLE PUSTE!
4. Utwórz głównego użytkownika systemu podając nazwę użytkownika i hasło.
5. Wybierając jakie pakiety Debian ma zainstalować na początku, wybierz swoje ulubione środowisko graficzne. Sugeruję aby było to KDE Plasma, jeśli jednak wiesz co robisz, możesz wybrać inne.

## Krok 2 - sterowniki Nvidia (możesz pominąć, jeśli nie posiadasz karty Nvidia)
Otwórz terminal i wykonaj następujące polecenia:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get install -y nvidia-open #dla kart z serii RTX2000 lub nowsze
sudo apt-get install -y cuda-drivers #dla kart z serii GTX1000 lub starsze
```

## Krok 3 - Flatpak
Flatpak to uniwersalny system dystrybucji oprogramowania na linuxa. Dzięki skonfigurowaniu repozytorium flatpak, dostajemy możliwość instalowania wielu przydatnych aplikacji prosto z wbudowanego w system sklepu.
```
sudo apt install flatpak
sudo apt install plasma-discover-backend-flatpak #jeśli używasz KDE Plasma
sudo apt install gnome-software-plugin-flatpak #jeśli używasz Gnome
flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Krok 4 - Backports
Repozytorium backports pozwala aktualizować niektóre pakiety na wersji stabilnej debiana. Kluczowe pakiety, które warto aktualizować, to kernel, mesa, pipewire, flatpak.
```
echo "deb http://deb.debian.org/debian trixie-backports main" | sudo tee /etc/apt/sources.list.d/backports.list
sudo apt update
```

Aby zainstalować pakiet z repozytorium backports użyj następującego polecenia:
```
sudo apt install -t trixie-backports <pakiet>
```

Aktualizacja kernela:
```
sudo apt install -t trixie-backports linux-headers-amd64 linux-image-amd64
```

Aktualizacja Mesa:
```
sudo apt install -t trixie-backports libegl-mesa0
```

Podobnie wygląda aktualizacja flatpak lub pipewire, jako nazwę pakieto nalezy podać właśnie flatpak lub pipewire.

Uwaga! Na dzień dzisiejszy (11.08.2025) nie ma jeszcze nowszych wersji tych pakietów w backports. Listę dostępnych do aktualizacji pakietów można znaleźć tutaj: https://packages.debian.org/trixie-backports/
