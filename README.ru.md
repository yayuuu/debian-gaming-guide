# Игры на Debian - Руководство
[![en](https://img.shields.io/badge/lang-en-red.svg)](README.md)
[![pl](https://img.shields.io/badge/lang-pl-red.svg)](README.pl.md)
[![zh](https://img.shields.io/badge/lang-zh-red.svg)](README.zh.md)
[![es](https://img.shields.io/badge/lang-es-red.svg)](README.es.md)
[![hi](https://img.shields.io/badge/lang-hi-red.svg)](README.hi.md)
[![pt](https://img.shields.io/badge/lang-pt-red.svg)](README.pt.md)
[![de](https://img.shields.io/badge/lang-de-red.svg)](README.de.md)
[![fr](https://img.shields.io/badge/lang-fr-red.svg)](README.fr.md)
[![ja](https://img.shields.io/badge/lang-ja-red.svg)](README.ja.md)
## Шаг 1 - Установка
1. Скачайте образ диска: https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-13.0.0-amd64-netinst.iso
2. Создайте загрузочную USB-флешку. Вы можете использовать приложения, такие как Rufus или Etcher. На некоторых старых платформах, даже после создания загрузочной флешки с помощью этих приложений, система может не загружаться. В качестве последнего средства можно использовать unetbootin (Linux).
3. Во время установки установщик попросит ввести пароль root - **ОСТАВЬТЕ ЭТО ПОЛЕ ПУСТЫМ!**
4. Создайте основного пользователя системы, указав имя пользователя и пароль.
5. При выборе пакетов, которые Debian должен установить изначально, выберите предпочитаемое графическое окружение. Я рекомендую KDE Plasma, но если вы знаете, что делаете, можете выбрать другое.

## Шаг 2 - Драйверы Nvidia (можно пропустить, если у вас нет видеокарты Nvidia)
Откройте терминал и выполните следующие команды:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get install -y nvidia-open #для карт серии RTX2000 и новее
sudo apt-get install -y cuda-drivers #для карт серии GTX1000 и старее
```

## Шаг 3 - Flatpak
Flatpak — это универсальная система распространения программного обеспечения для Linux. Настроив репозиторий Flatpak, вы сможете устанавливать множество полезных приложений прямо из встроенного магазина системы.
```
sudo apt install flatpak
sudo apt install plasma-discover-backend-flatpak #если используете KDE Plasma
sudo apt install gnome-software-plugin-flatpak #если используете Gnome
flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Шаг 4 - Backports
Репозиторий backports позволяет обновлять некоторые пакеты в стабильной версии Debian. Ключевые пакеты, которые стоит обновить: kernel, mesa, pipewire, flatpak.
```
echo "deb http://deb.debian.org/debian trixie-backports main" | sudo tee /etc/apt/sources.list.d/backports.list
sudo apt update
```

Чтобы установить пакет из репозитория backports, используйте команду:
```
sudo apt install -t trixie-backports <пакет>
```

Обновление ядра:
```
sudo apt install -t trixie-backports linux-headers-amd64 linux-image-amd64
```

Обновление Mesa:
```
sudo apt install -t trixie-backports libegl-mesa0
```

Аналогично, для обновления flatpak или pipewire замените `<пакет>` на flatpak или pipewire.

**Примечание:** На сегодняшний день (11.08.2025) в backports пока нет новых версий этих пакетов. Список доступных пакетов: https://packages.debian.org/trixie-backports/
