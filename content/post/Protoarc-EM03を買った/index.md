---
title: "Protoarc EM03を買った"
date: 2023-12-15T02:09:25+09:00
draft: false
image: "https://rlysleepycontents.blob.core.windows.net/images/IMG_20231215_110508.jpg"
categories: [gadget]
---

### この記事は [あらた界隈 Advent Calendar 2023](https://adventar.org/calendars/9714) 13日目の記事です。 

## あらすじ

最近外出先 or バイト先でPCを利用する機会が多いので、外出時持って歩く用のトラックボールを購入しました。

- ちなみに自宅ではKensingtonのExpert Mouseを使っている

ProtoArcという謎メーカーから出ていたEM03というトラックボールのご紹介です。

- [アメリカに会社があるらしい](https://cybersocean.net/protoarc-em01rev/)けど、まあたぶん中華でしょう。気にしないけど。

## 本体の紹介

![](https://rlysleepycontents.blob.core.windows.net/images/664062785856208896/1185040195851128974/IMG_20231215_110508.jpg?ex=658e29af&is=657bb4af&hm=0e070059bf6cd7a2d2c2fab56e887b923ccff121dedd5eb015843e85fbe48cae&=&format=webp&width=1170&height=659)

形状は非常に Microsoft謹製の例のトラックボールに似通っており、如何にもエルゴノミクスな感じです。

質感は見たとおりのマットな仕上がりで、古いThinkpadとかの天板を想像させる肌触りで非常に好きです。

- 劣化したときのことはあまりかんがえたくないです汗

![](https://rlysleepycontents.blob.core.windows.net/images/664062785856208896/1185040196618703031/IMG_20231215_110526.jpg?ex=658e29af&is=657bb4af&hm=52b52dc1c4009ac5614a611f3da3d27c369a8b8a6425ad092f070bae6834a5e2&=&format=webp&width=1170&height=659)

主なボタンの数は、左クリック & 中クリック(ホイール押下) & 進む & 戻る & 右クリック の5つです。

- 個人的には ELECOM製のHUGEを使っていた過去があるので、右クリックの隣にもう一つボタンが欲しいところ

- 一般的な用途で困ることはないでしょう。

スマホのカメラがぶっ壊れてるのでうまく撮れませんでしたが、ボールの支持球は白いセラミック製？です。

- 油が切れると滑りが悪くなるので、鼻の脂を注油してやるといい感じです。(社不Tips)

![](https://rlysleepycontents.blob.core.windows.net/images/664062785856208896/1185040212053721098/IMG_20231215_110626.jpg?ex=658e29b3&is=657bb4b3&hm=4f8574b58102c58777e5a80dd7f87711e6b47cb870f981a09134138ef25a2e6f&=&format=webp&width=1170&height=659)

裏面には イルミネーションパターン変更ボタン & モード切替ボタン & 2.4GHzのUSBレシーバー & 電源スイッチがあります。

- イルミネーションは消灯含む5パターンあり、専用ソフトで設定とかはできないそうです。

- 接続モードは、2.4GHzレシーバー & Bluetooth & 左記を同時接続？ の3つあります。

  - Bluetoothでペアリングする際は2番に合わせた状態で、モード切替ボタンを長押しするとできます。

- 今めちゃ爪伸びてるから簡単に取れるけど、レシーバーは奥まで刺さるので爪短い人だと取るのが大変かもしれない

- DPIは200-400-800-1200-1600の5段階で切り替えできます。

  - ホイール押し込みと右クリック5秒同時押しで切替えできます。

## openSUSE Leap で使う

openSUSE Leap で本トラックボールを使うための設定を紹介します。

まず、Bluetoothを扱うために```Blueman```をインストールします。

```$ sudo zypper in blueman```

インストールが終わったら各位使ってるアプリケーションランチャより起動します。

- 本体裏面のモード切替ボタンを2番に合わせた状態で長押し、ペアリングモードにしておきます。

![](https://rlysleepycontents.blob.core.windows.net/images/664062785856208896/1185046119982579782/image.png?ex=658e2f34&is=657bba34&hm=425a2ed19394bdadb105231f457348b6c5c818899a752bc11d7c7cb844d8c561&=&format=webp&quality=lossless&width=719&height=370)

もう追加済みなので追加したことになってますが、こんな感じで周りのBluetoothデバイスが一覧に出てくると思うので、"ProtoArc EM03" を選択し、ペアリングします。

ペアリングが終わったら、通常通り使用できるはずです。

### ボールコロコロでスクロール

特定のボタンを押下しながらボールをコロコロすることで、画面のスクロールをできるようにする方法を書いておきます。

- Windowsだと```W10Wheel.NET```とかをインストールすればできるようになります

今回は```/usr/share/X11/xorg.conf.d/```配下に新規の設定ファイルを作ってやります。

``` console
$ sudo touch /usr/share/X11/xorg.conf.d/30-protoarc.conf
$ sudo vim /usr/share/X11/xorg.conf.d/30-protoarc.conf
```

設定したい特定のボタン番号は```xev```で調べて、下記における```"ScrollButton" "2"``` を書き換えてください。

- 今回は右クリック + ボールコロコロ でスクロールするようにしました。

  - 本当は左右同時クリックしている間をトリガーにしたかったけど、めっちゃめんどくさそうだったので我慢です

  - [実際にやってる人がいた](https://metrocrusader.blogspot.com/2015/05/linux-trackballemulate3buttons.html)んだけど、evdevのソース書換とかやってらんないので割愛

``` config:/usr/share/X11/xorg.conf.d/30-protoarc.conf
Section "InputClass"                                                                      
    Identifier  "ProtoArc EM03 Mouse"
    MatchProduct "ProtoArc EM03 Mouse"
    Driver      "libinput"
    Option      "ScrollMethod"  "Button"
    Option      "ScrollButton"  "3"
EndSection
```

ちなみにこの設定ファイルだと MatchProductで設定を適用するデバイスを絞っていますが、```xinput list```で確認することができます。

``` console
nick@x250suse/u/s/X/xorg.conf.d> xinput list
⎡ Virtual core pointer                      id=2  [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer                id=4  [slave  pointer  (2)]
⎜   ↳ Synaptics TM3075-002                      id=12 [slave  pointer  (2)]
⎜   ↳ TPPS/2 IBM TrackPoint                     id=13 [slave  pointer  (2)]
⎜   ↳ ProtoArc EM03 Mouse                       id=14 [slave  pointer  (2)]
⎜   ↳ ProtoArc EM03 Keyboard                    id=15 [slave  pointer  (2)]
⎣ Virtual core keyboard                     id=3  [master keyboard (2)]
    ↳ Virtual core XTEST keyboard               id=5  [slave  keyboard (3)]
    ↳ Power Button                              id=6  [slave  keyboard (3)]
    ↳ Video Bus                                 id=7  [slave  keyboard (3)]
    ↳ Sleep Button                              id=8  [slave  keyboard (3)]
    ↳ Integrated Camera: Integrated C           id=9  [slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard              id=10 [slave  keyboard (3)]
    ↳ ThinkPad Extra Buttons                    id=11 [slave  keyboard (3)]
    ↳ ProtoArc EM03 Keyboard                    id=16 [slave  keyboard (3)]
```

- なぜかキーボードとして認識されているのは謎

設定を書き換えてOSを再起動すると右クリック+コロコロでスクロールできるようになっているはずです。
