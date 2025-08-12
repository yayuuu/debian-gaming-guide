# Debian Gaming - Guia
[![en](https://img.shields.io/badge/lang-en-red.svg)](README.md)
[![pl](https://img.shields.io/badge/lang-pl-red.svg)](README.pl.md)
[![zh](https://img.shields.io/badge/lang-zh-red.svg)](README.zh.md)
[![es](https://img.shields.io/badge/lang-es-red.svg)](README.es.md)
[![hi](https://img.shields.io/badge/lang-hi-red.svg)](README.hi.md)
[![ru](https://img.shields.io/badge/lang-ru-red.svg)](README.ru.md)
[![de](https://img.shields.io/badge/lang-de-red.svg)](README.de.md)
[![fr](https://img.shields.io/badge/lang-fr-red.svg)](README.fr.md)
[![ja](https://img.shields.io/badge/lang-ja-red.svg)](README.ja.md)
## Passo 1 - Instalação
1. Baixe a imagem do disco: https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-13.0.0-amd64-netinst.iso
2. Crie um pendrive bootável. Você pode usar aplicativos como Rufus ou Etcher. Em algumas plataformas mais antigas, mesmo após criar um pendrive bootável com um desses aplicativos, o sistema pode não iniciar. Como último recurso, você pode usar o unetbootin (Linux).
3. Durante a instalação, o instalador pedirá a senha do root - **DEIXE ESTE CAMPO EM BRANCO!**
4. Crie o usuário principal do sistema fornecendo um nome de usuário e senha.
5. Ao escolher quais pacotes o Debian deve instalar no início, selecione seu ambiente gráfico favorito. Sugiro KDE Plasma, mas se você souber o que está fazendo, pode escolher outro.

## Passo 2 - Drivers Nvidia (pode pular se não tiver placa Nvidia)
Abra o terminal e execute os seguintes comandos:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get install -y nvidia-open #para placas série RTX2000 ou mais recentes
sudo apt-get install -y cuda-drivers #para placas série GTX1000 ou mais antigas
```

## Passo 3 - Flatpak
Flatpak é um sistema universal de distribuição de software para Linux. Ao configurar o repositório Flatpak, você poderá instalar muitos aplicativos úteis diretamente pela loja integrada do sistema.
```
sudo apt install flatpak
sudo apt install plasma-discover-backend-flatpak #se usar KDE Plasma
sudo apt install gnome-software-plugin-flatpak #se usar Gnome
flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Passo 4 - Backports
O repositório backports permite atualizar certos pacotes na versão estável do Debian. Pacotes importantes para atualizar incluem kernel, mesa, pipewire e flatpak.
```
echo "deb http://deb.debian.org/debian trixie-backports main" | sudo tee /etc/apt/sources.list.d/backports.list
sudo apt update
```

Para instalar um pacote do repositório backports:
```
sudo apt install -t trixie-backports <pacote>
```

Atualizar kernel:
```
sudo apt install -t trixie-backports linux-headers-amd64 linux-image-amd64
```

Atualizar Mesa:
```
sudo apt install -t trixie-backports libegl-mesa0
```

Da mesma forma, para atualizar flatpak ou pipewire, substitua `<pacote>` por flatpak ou pipewire.

**Nota:** Até a data de hoje (11.08.2025), ainda não há versões mais recentes desses pacotes no backports. Lista disponível em: https://packages.debian.org/trixie-backports/
