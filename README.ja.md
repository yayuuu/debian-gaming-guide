# Debian ゲーミング - ガイド
[![en](https://img.shields.io/badge/lang-en-red.svg)](README.md)
[![pl](https://img.shields.io/badge/lang-pl-red.svg)](README.pl.md)
[![zh](https://img.shields.io/badge/lang-zh-red.svg)](README.zh.md)
[![es](https://img.shields.io/badge/lang-es-red.svg)](README.es.md)
[![hi](https://img.shields.io/badge/lang-hi-red.svg)](README.hi.md)
[![pt](https://img.shields.io/badge/lang-pt-red.svg)](README.pt.md)
[![ru](https://img.shields.io/badge/lang-ru-red.svg)](README.ru.md)
[![de](https://img.shields.io/badge/lang-de-red.svg)](README.de.md)
[![fr](https://img.shields.io/badge/lang-fr-red.svg)](README.fr.md)
## ステップ 1 - インストール
1. ディスクイメージをダウンロード: https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-13.0.0-amd64-netinst.iso
2. ブータブルUSBドライブを作成します。Rufus や Etcher などのアプリケーションを使用できます。一部の古いプラットフォームでは、これらのアプリでブータブルUSBを作成してもシステムが起動しない場合があります。最後の手段として unetbootin (Linux) を使用できます。
3. インストール中に、インストーラーが root パスワードを求めますが、**このフィールドは空のままにしてください！**
4. ユーザー名とパスワードを入力して、システムのメインユーザーを作成します。
5. Debian が最初にインストールするパッケージを選ぶ際、好みのデスクトップ環境を選択します。KDE Plasma を推奨しますが、わかっている場合は他を選択しても構いません。

## ステップ 2 - Nvidia ドライバー（Nvidia カードを持っていない場合はスキップ可能）
ターミナルを開き、次のコマンドを実行します：
```
wget https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get install -y nvidia-open #RTX2000 シリーズ以降のカード用
sudo apt-get install -y cuda-drivers #GTX1000 シリーズ以前のカード用
```

## ステップ 3 - Flatpak
Flatpak は Linux 用の汎用ソフトウェア配布システムです。Flatpak リポジトリを設定すると、システムの組み込みストアから多くの便利なアプリケーションを直接インストールできます。
```
sudo apt install flatpak
sudo apt install plasma-discover-backend-flatpak #KDE Plasma を使用している場合
sudo apt install gnome-software-plugin-flatpak #Gnome を使用している場合
flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## ステップ 4 - Backports
Backports リポジトリを使用すると、Debian の安定版で特定のパッケージを更新できます。更新すべき重要なパッケージには、カーネル、mesa、pipewire、flatpak があります。
```
echo "deb http://deb.debian.org/debian trixie-backports main" | sudo tee /etc/apt/sources.list.d/backports.list
sudo apt update
```

Backports リポジトリからパッケージをインストールするには：
```
sudo apt install -t trixie-backports <パッケージ>
```

カーネルの更新：
```
sudo apt install -t trixie-backports linux-headers-amd64 linux-image-amd64
```

Mesa の更新：
```
sudo apt install -t trixie-backports libegl-mesa0
```

同様に、flatpak や pipewire を更新する場合は `<パッケージ>` を flatpak または pipewire に置き換えてください。

**注意:** 現在 (2025年8月11日) の時点で、backports にはこれらのパッケージの新しいバージョンはまだありません。更新可能なパッケージ一覧はこちら: https://packages.debian.org/trixie-backports/
