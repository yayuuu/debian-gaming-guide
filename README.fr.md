# Debian Gaming - Guide
[![en](https://img.shields.io/badge/lang-en-red.svg)](README.md)
[![pl](https://img.shields.io/badge/lang-pl-red.svg)](README.pl.md)
[![zh](https://img.shields.io/badge/lang-zh-red.svg)](README.zh.md)
[![es](https://img.shields.io/badge/lang-es-red.svg)](README.es.md)
[![hi](https://img.shields.io/badge/lang-hi-red.svg)](README.hi.md)
[![pt](https://img.shields.io/badge/lang-pt-red.svg)](README.pt.md)
[![ru](https://img.shields.io/badge/lang-ru-red.svg)](README.ru.md)
[![de](https://img.shields.io/badge/lang-de-red.svg)](README.de.md)
[![ja](https://img.shields.io/badge/lang-ja-red.svg)](README.ja.md)
## Étape 1 - Installation
1. Télécharge l'image disque : https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-13.0.0-amd64-netinst.iso
2. Crée une clé USB bootable. Tu peux utiliser des applications comme Rufus ou Etcher. Sur certaines anciennes plateformes, même après avoir créé une clé USB bootable avec l'une de ces applications, le système peut ne pas démarrer. En dernier recours, tu peux utiliser unetbootin (Linux).
3. Pendant l'installation, l'installateur te demandera le mot de passe root – **LAISSE CE CHAMP VIDE !**
4. Crée l'utilisateur principal du système en fournissant un nom d'utilisateur et un mot de passe.
5. Lors du choix des paquets à installer au départ, sélectionne ton environnement de bureau préféré. Je recommande KDE Plasma, mais si tu sais ce que tu fais, tu peux en choisir un autre.

## Étape 2 - Pilotes Nvidia (peut être ignoré si tu n'as pas de carte Nvidia)
Ouvre le terminal et exécute les commandes suivantes :
```
wget https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get install -y nvidia-open #pour les cartes série RTX2000 ou plus récentes
sudo apt-get install -y cuda-drivers #pour les cartes série GTX1000 ou plus anciennes
```

## Étape 3 - Flatpak
Flatpak est un système universel de distribution de logiciels pour Linux. En configurant le dépôt Flatpak, tu peux installer de nombreuses applications utiles directement depuis la boutique intégrée du système.
```
sudo apt install flatpak
sudo apt install plasma-discover-backend-flatpak #si tu utilises KDE Plasma
sudo apt install gnome-software-plugin-flatpak #si tu utilises Gnome
flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Étape 4 - Backports
Le dépôt backports permet de mettre à jour certains paquets dans la version stable de Debian. Les paquets clés à mettre à jour incluent le noyau, mesa, pipewire et flatpak.
```
echo "deb http://deb.debian.org/debian trixie-backports main" | sudo tee /etc/apt/sources.list.d/backports.list
sudo apt update
```

Pour installer un paquet depuis le dépôt backports :
```
sudo apt install -t trixie-backports <paquet>
```

Mise à jour du noyau :
```
sudo apt install -t trixie-backports linux-headers-amd64 linux-image-amd64
```

Mise à jour de Mesa :
```
sudo apt install -t trixie-backports libegl-mesa0
```

De même, pour mettre à jour flatpak ou pipewire, remplace `<paquet>` par flatpak ou pipewire.

**Remarque :** À ce jour (11.08.2025), il n'existe pas encore de versions plus récentes de ces paquets dans backports. Liste disponible ici : https://packages.debian.org/trixie-backports/
