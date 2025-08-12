# Juegos en Debian - Guía
[![en](https://img.shields.io/badge/lang-en-red.svg)](README.md)
[![pl](https://img.shields.io/badge/lang-pl-red.svg)](README.pl.md)
[![zh](https://img.shields.io/badge/lang-zh-red.svg)](README.zh.md)
[![hi](https://img.shields.io/badge/lang-hi-red.svg)](README.hi.md)
[![pt](https://img.shields.io/badge/lang-pt-red.svg)](README.pt.md)
[![ru](https://img.shields.io/badge/lang-ru-red.svg)](README.ru.md)
[![de](https://img.shields.io/badge/lang-de-red.svg)](README.de.md)
[![fr](https://img.shields.io/badge/lang-fr-red.svg)](README.fr.md)
[![ja](https://img.shields.io/badge/lang-ja-red.svg)](README.ja.md)
## Paso 1 - Instalación
1. Descarga la imagen del disco: https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-13.0.0-amd64-netinst.iso
2. Crea una unidad USB de arranque. Puedes usar aplicaciones como Rufus o Etcher. En algunas plataformas más antiguas, incluso después de crear un USB de arranque con una de estas aplicaciones, el sistema puede no arrancar. Como último recurso, puedes usar unetbootin (Linux).
3. Durante la instalación, el instalador pedirá la contraseña de root - ¡DEJA ESTE CAMPO VACÍO!
4. Crea el usuario principal del sistema proporcionando un nombre de usuario y una contraseña.
5. Al elegir qué paquetes debe instalar Debian al principio, selecciona tu entorno de escritorio favorito. Sugiero KDE Plasma, pero si sabes lo que haces, puedes elegir otro.

## Paso 2 - Controladores Nvidia (puedes omitir si no tienes una tarjeta Nvidia)
Abre la terminal y ejecuta los siguientes comandos:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get install -y nvidia-open #para tarjetas serie RTX2000 o más nuevas
sudo apt-get install -y cuda-drivers #para tarjetas serie GTX1000 o más antiguas
```

## Paso 3 - Flatpak
Flatpak es un sistema de distribución de software universal para Linux. Configurando el repositorio de Flatpak, puedes instalar muchas aplicaciones útiles directamente desde la tienda integrada del sistema.
```
sudo apt install flatpak
sudo apt install plasma-discover-backend-flatpak #si usas KDE Plasma
sudo apt install gnome-software-plugin-flatpak #si usas Gnome
flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Paso 4 - Backports
El repositorio backports te permite actualizar ciertos paquetes en la versión estable de Debian. Paquetes clave que vale la pena actualizar incluyen kernel, mesa, pipewire y flatpak.
```
echo "deb http://deb.debian.org/debian trixie-backports main" | sudo tee /etc/apt/sources.list.d/backports.list
sudo apt update
```

Para instalar un paquete desde el repositorio backports, usa:
```
sudo apt install -t trixie-backports <paquete>
```

Actualizar kernel:
```
sudo apt install -t trixie-backports linux-headers-amd64 linux-image-amd64
```

Actualizar Mesa:
```
sudo apt install -t trixie-backports libegl-mesa0
```

Del mismo modo, para actualizar flatpak o pipewire, reemplaza `<paquete>` con flatpak o pipewire.

**Nota:** A día de hoy (11.08.2025), todavía no hay versiones más recientes de estos paquetes en backports. Lista disponible aquí: https://packages.debian.org/trixie-backports/
