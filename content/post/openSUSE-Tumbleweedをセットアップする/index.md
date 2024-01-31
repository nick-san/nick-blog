---
title: "OpenSUSE Tumbleweedをセットアップする"
date: 2024-01-31
draft: false
image: "https://media.discordapp.net/attachments/664062785856208896/1202273930581123124/image.png?ex=65ccdbda&is=65ba66da&hm=12e075d50f3bd346350b4e3c3b3ee2cdbc1136e4b7e4f53e919218eae3f2688a&=&format=webp&quality=lossless&width=1440&height=423"

---

今回はわたくしのメイン環境である母艦PCのOSを再インストールしたので、やったことのまとめです。

- openSUSE Leap 15.4 を使っていましたが、なんやかんやしているうちにNetworkのサービスを消し飛ばしてしまい詰んだので、いっそTumbleweedをクリーンインストールするかーとなりました(死)

- Tumbleweedを選んだ深い理由はありませんが、メイン環境と言いつつそんなに最近使っていないので、なにかあっても困らないのと、単純に新しいパッケージが提供され続けるのがいいなぁと思ったことくらいです。

## インストールメディアの作成

母艦には別のディスク(SSD)にWindows10が入っているので、そちらで [公式サイト](https://get.opensuse.org/tumbleweed/#download) からISOイメージをダウンロードし、 [Rufus](https://rufus.ie/ja/) でUSBメモリにイメージを焼きます。

- 現状のopenSUSE環境からのバックアップも忘れずに。

## インストール開始

PCを再起動し、然るべきキーを押下してbootメニューを起動し、openSUSEのインストールメディア(USB)を起動します。

- インストール的な選択肢を選ぶとYaSTが起動するので、画面の通りに進めていきます。

以下、YaSTの項目でのわたくしの設定を書き記します。

### ディスク

今回はちゃんと/homeとルートディレクトリを分け、Btrfsでフォーマットしたうえでスナップショットも有効化し、Swapも潤沢に確保しています

- 今まで/homeとルートディレクトリを分けていなったので環境破壊のたびに困ったことになっていました(エチョ)

### デスクトップ

[i3](https://i3wm.org/) を使用する予定なので、「汎用デスクトップ」を選択しています。

- ちなみに「汎用デスクトップ」を選択すると [IceWM](https://ice-wm.org/) がインストールされます。

## 入れたパッケージたち

以下は、openSUSE のインストール終了後に入れたパッケージたちです。

- 基本的に ```zypper``` で入れれるものオンリーですが、パッケージ名が他のディストロと違ったり違わなかったりするのでよしなに GOOGLE IT.

### お好みセット

- [Terminator](https://gnome-terminator.org/)
  - ターミナルはかれこれずっとこれを使っています。
- [fish](https://fishshell.com/)
  - シェルもかれこれずっとこれを使っています。
- [i3](https://i3wm.org/)
  - wmはかれこれずっとこれを使っています。
  - アプリランチャとして [rofi](https://github.com/davatorium/rofi) を入れています。
  - NetworkManager-applet
- [nemo](https://github.com/linuxmint/nemo)
  - GUIファイラーはかれこれずっとこれを使っています。
    - 使用感が気に入っているのと、余計なのが同時に入らないのですき
- [flameshot](https://flameshot.org/)
  - スクショを撮るやつ 便利
- [VLC](https://www.videolan.org/vlc/index.ja.html)
  - [Packman Repo](http://packman.links2linux.org/) を追加してやると幸せになれると思います。
- [lxappearance](https://github.com/lxde/lxappearance)
  - GTKの外観を簡単に変えるやつ LXDEの一部だけど、これだけ入れることも可能
- [picom](https://github.com/yshui/picom)
  - ウインドウの透過とかをやるやつ
- [fcitx5](https://github.com/fcitx/fcitx5)
  - ラップトップではfcitx-SKKを使っていますが、母艦では使ってないです。
- [unar](https://github.com/ashang/unar)
  - いろんな形式のアーカイブをよしなにしてくれるやつ

### ファイル共有

- [Samba](https://www.samba.org/)
  - ```yast2-samba-server``` を入れると必要なものが全部入る + YaSTで設定できるようになるのでオススメ
  - ```YaST ファイヤウォール``` から然るべき設定を変えて、```systemctl``` でサービスを有効化しましょう

### 入ってないだと❓

- Git
- pulseaudio
  - pavucontrol 音量ミキサー的なやつ
  - pasystray ステータスバーのアプレット

### ブラウザとか

- Firefox はかれこれ使い始めて10年くらい
  - アドオン
    - [Vimium](https://addons.mozilla.org/en-GB/firefox/addon/vimium-ff/) Vimライクなキーバインドを使えるようにするやつ

### ぜったいいる
- [screenfetch](https://github.com/KittyKatt/screenFetch)
  - 黒い画面にカタカタ... ッッターン つってドヤ顔をするやつ
- [sl](https://github.com/mtoyoda/sl)
  - SL = 蒸気機関車
