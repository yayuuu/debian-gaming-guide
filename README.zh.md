# Debian 游戏 - 指南
[![en](https://img.shields.io/badge/lang-en-red.svg)](README.md)
[![pl](https://img.shields.io/badge/lang-pl-red.svg)](README.pl.md)
[![es](https://img.shields.io/badge/lang-es-red.svg)](README.es.md)
[![hi](https://img.shields.io/badge/lang-hi-red.svg)](README.hi.md)
[![pt](https://img.shields.io/badge/lang-pt-red.svg)](README.pt.md)
[![ru](https://img.shields.io/badge/lang-ru-red.svg)](README.ru.md)
[![de](https://img.shields.io/badge/lang-de-red.svg)](README.de.md)
[![fr](https://img.shields.io/badge/lang-fr-red.svg)](README.fr.md)
[![ja](https://img.shields.io/badge/lang-ja-red.svg)](README.ja.md)
## 步骤 1 - 安装
1. 下载磁盘映像: https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-13.0.0-amd64-netinst.iso
2. 创建可启动的 USB 驱动器。你可以使用 Rufus 或 Etcher 等应用程序。在一些较旧的平台上，即使使用这些应用程序创建了可启动 USB，系统仍可能无法启动。作为最后的手段，你可以使用 unetbootin (Linux)。
3. 安装过程中，安装程序会要求输入 root 密码 - **保持此字段为空！**
4. 创建系统的主要用户，输入用户名和密码。
5. 选择 Debian 在开始时要安装的软件包时，选择你喜欢的桌面环境。建议使用 KDE Plasma，但如果你知道自己在做什么，也可以选择其他。

## 步骤 2 - Nvidia 驱动程序（如果你没有 Nvidia 显卡可跳过）
打开终端并运行以下命令：
```
wget https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get install -y nvidia-open #适用于 RTX2000 系列或更新型号的显卡
sudo apt-get install -y cuda-drivers #适用于 GTX1000 系列或更旧型号的显卡
```

## 步骤 3 - Flatpak
Flatpak 是一种适用于 Linux 的通用软件分发系统。配置 Flatpak 仓库后，你可以直接从系统自带的应用商店安装许多实用程序。
```
sudo apt install flatpak
sudo apt install plasma-discover-backend-flatpak #如果使用 KDE Plasma
sudo apt install gnome-software-plugin-flatpak #如果使用 Gnome
flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## 步骤 4 - Backports
Backports 仓库允许你在 Debian 稳定版中更新某些软件包。值得更新的关键软件包包括内核、mesa、pipewire 和 flatpak。
```
echo "deb http://deb.debian.org/debian trixie-backports main" | sudo tee /etc/apt/sources.list.d/backports.list
sudo apt update
```

要从 backports 仓库安装软件包，请使用以下命令：
```
sudo apt install -t trixie-backports <软件包>
```

更新内核：
```
sudo apt install -t trixie-backports linux-headers-amd64 linux-image-amd64
```

更新 Mesa：
```
sudo apt install -t trixie-backports libegl-mesa0
```

同样地，要更新 flatpak 或 pipewire，请将 `<软件包>` 替换为 flatpak 或 pipewire。

**注意：** 截至今日 (2025 年 8 月 11 日)，backports 中还没有这些软件包的更新版本。可更新软件包列表见：https://packages.debian.org/trixie-backports/
