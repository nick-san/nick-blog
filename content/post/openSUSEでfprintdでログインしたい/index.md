---
title: "OpenSUSEでfprintdでログインしたい"
date: 2023-12-24
draft: false
image: "https://rlysleepycontents.blob.core.windows.net/images/IMG_20231215_232619.jpg"
---

**この記事は[openSUSE Advent Calendar 2023](https://adventar.org/calendars/9615) 24日目の記事です。**

- 見事に遅刻いたしました、申しわけない!!!

みなさんこんにちは。

今回は弊ラップトップのopenSUSEでfprintdによる指紋認証ログインをできるようにしてみました。

### 動作環境

- openSUSE Leap 15.5

  - LightDM, LightDM-Greeter

- Thinkpad X250 指紋リーダ付き

  - ```lsusb```上では指紋リーダは```Validity Sensors, Inc. VFS 5011 fingerprint sensor```と表記

## 実際の手順


### パッケージのインストール

まず必要パッケージのインストールです。

```sudo zypper install fprintd fprintd-pam``` 

- fprintについては[こちら](https://wiki.archlinux.jp/index.php/Fprint)をご覧ください。

  - 一言で言うと、ラップトップの指紋リーダを[PAM](https://wiki.archlinux.jp/index.php/PAM)で扱うパッケージです。

  - ```fprintd```はdaemonとして動作する```fprint```という認識で合ってるはず。

(ちなみに筆者はfprintd-pamをインストールするのを忘れておりnか月くらいなんでうごかないんだろうとなっておりました)

### PAMの設定ファイルの編集
```config
$ sudo vim /etc/pam.d/lightdm

#%PAM-1.0
auth sufficient pam_fprintd.so #これを追加する

auth   include  xdm
account  include  xdm
password include  xdm
session  include  xdm
```

```config:
$ sudo vim /etc/pam.d/lightdm-greeter

#%PAM-1.0
# LightDM PAM configuration used only for the greeter session

auth sufficient pam_fprintd.so #これを追加する

auth     required       pam_permit.so
account  required       pam_permit.so
password include        common-password
session  required       pam_loginuid.so
session  include        common-session

```

### 指紋の追加

認証に使う指紋の追加です。

```fprintd-enroll```コマンドを実行すると指紋リーダが光るので、数回指をスライドさせます。

```Enroll result: enroll-completed``` と表示されれば指紋の追加は完了です。

- ちなみに: ```fprintd-enroll -f right-middle-finger User``` と入力すると、Userの右手中指を指定して登録することができます。

### 動作確認

![](https://rlysleepycontents.blob.core.windows.net/images/664062785856208896/1185226801618890872/IMG_20231215_232619.jpg?ex=658ed779&is=657c6279&hm=201a326c663f459395838e46f3b46b9c4e5e5a95256faaf0d23e26b983e15f70&=&format=webp&width=719&height=405)

手順が全て終わったら、ログアウトしてLightDM-Greeterの画面で指紋認証でログインできるかテストします。

- 指紋リーダが光っている状態で、指をスライドさせ、Loginボタン押下でログインできれば完了です。
