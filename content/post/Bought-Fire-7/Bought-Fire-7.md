---
title: "Bought Fire 7"
date: 2023-02-28T21:15:44+09:00
draft: false
image: https://i.imgur.com/6kkSNGY.jpg
---

# Amazon Fire 7 (2022) を買った
## まえがき
![](https://i.imgur.com/6kkSNGY.jpg)

近所のハドフで Amazon Fire 7 の2022年モデルが3000円とかで売ってたので車載用にすべく購入した。
ここでは、Fire 7 にやったことやすることを記録します。

### Fire 7 (2022) の諸元
|画面サイズ/解像度|SoC|RAM/ROM|
|---|---|---|
|7インチ/1024x600|MediaTek MT8168V/B|2GB/16GB|

わたしが買ったのは2022年のモデルで、これは第12世代にあたります。
ROM容量が16GB、ディスプレイが _1024x600_ と、本当に令和最新版7インチタブレットかよ と言いたくなるスペックではありますが、まあ車載モニター的な使いかたならいいでしょう...

## レビュー
- 安すぎてヤバイ
    - ハドフ驚異の3000円
        - 顔が神になりました
- やはりスペックがアレすぎて重い
    - けど本体は軽いので◎
- サイズ感がほどよい
    - やっぱ7インチタブはいいね
    - せめてディスプレイはHD以上であってほしいところではある
- Fire OSはクソ
    - ホームランチャーすら変えれないってどういうことYO
        - まあなんなりとやれば変えれるからいいんだけどね
    - ~~OTAアップデート無効化できないとかちらっと聞いたけどマジ？~~
        - たぶん無効化できた

## やったこと

### インスコしたアプリとか
- [Revanced](https://github.com/revanced)の導入
    - 伴ってRevanced MicroG, ReVanced Managerも導入
    - パッチあてるのにスッゲェ時間かかった
- [F-Droid](https://f-droid.org/ja/) 経由でいれたもの
    - VLC for Android
    - DuckDuckGo Browser
    - Aurora Store (Playストア代替)
- X-plore File Manager

### 設定とか
- ロック画面での広告表示を消す
    - 設定→Amazonアプリの設定→広告→ロック画面の広告 をオフ
- 開発者オプション
    - 有効化
        - 設定→端末オプション→Fireタブレットのバージョン情報→シリアル番号 を連打
            - 以降、設定→端末オプション→開発者オプション にアクセスできるようになります
    - 弄ったとこ
        - USBデバッグをオンにする
        - 描画→アニメーションのスケール関連を0.5x
            - なしにしてもいいけど個人的に0.5xにする派なので
        - ハードウェアアクセラレーションレンダリング→ハードウェアオーバーレイを無効にする をオン
            - 電池の食い具合とご相談
        - アプリ→バックグラウンドプロセスの上限→4
            - RAMが2GBしかないので...

### adbまわり
openSUSE Leap 15.4 では、[hardware](https://software.opensuse.org/download.html?project=hardware&package=android-tools)リポジトリを購読し、**android-tools** パッケージをインストールすることでadbコマンドを使えるようになります

開発者オプションよりUSBデバッグを有効化し、USBケーブルでPCとFire7を接続します。

- ホームのランチャーを変える
    - ```addb shell pm disable-user com.amazon.firelauncher``` をすることで純正のランチャーを無効化することができます
    - あとはなんなりと好みのランチャーを拾ってきてインスコ後、ホームボタンを押下することで、既定のランチャーとして設定することができます。
        - 筆者はNova Launcherを入れました
- OTAアップデートの無効化
    - ```adb shell pm disable-user --user 0 com.amazon.device.software.ota```
```adb shell pm disable-user --user 0 com.amazon.device.software.ota.override```

### 車載関連
弊フィット(CBA-GD3)に車載するにあたって、GDフィットはdinスペース上部にエアコン吹き出し口があるため、そこに装着することにした
- 1din空いてるスロットに[コレ](http://beatsonic.co.jp/accessories/qbg15.php)がよさそうだったけど結構高いのでやめた(本体より高いってどういうことよ!!!!)

近所のオートバックスのセコハン市場で1つ300円だったので、スマホホルダーを購入(2つ)

そして装着
![](https://i.imgur.com/bZrfMsO.jpg)

ちょうど電源ボタンのあるところにホルダーが当たってスリープしてしまうため後日削るなり、よしなにしたいと思っている
基本的にホールドされており、大事故でもおこさぬ限り落下しなそうなので当面これで運用しようと思う

## 今後やりたいこと / アイデアなど
- OBD2ドングルを買って計器として使う
    - ***ELM327***がよさそう？
- でかいMicroSDにいろいろをぶちこんで月々の通信料を節約
- 動作が重いのでswapファイルを扱えるようにする
    - rootedな環境じゃないとダメ？説もある
    - 現状Fire7をrootedにする方法はない模様
- あわよくばROM焼きか？
