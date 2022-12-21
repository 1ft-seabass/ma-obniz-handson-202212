# はじめに

## 今日はobniz スターターキットで進めます

![cc9e7a2a227a0f14cd2dd02c5cf63d50](https://i.gyazo.com/cc9e7a2a227a0f14cd2dd02c5cf63d50.jpg)

今日はobniz スターターキットで進めます。以下のような準備ができていると思われます。

- obniz スターターキットがある（自分の obniz）
- obniz クラウドアカウントがある
- そのアカウントに自分の obniz を登録している
- 登録できているということは Wi-Fi がつながっている

## obniz とは

![f687197f0cd8b016587135a8fdcc686d](https://i.gyazo.com/f687197f0cd8b016587135a8fdcc686d.png)

obnizとは | すべての人にIoT開発の機会を、それがobniz（オブナイズ）の使命です
https://obniz.io/ja/how_obniz_works

本家の説明が分かりやすくを、こちらを軸に説明していきます。

## ドキュメントが豊富

![0a123a11c4c00be6c291ab3e486641f7](https://i.gyazo.com/0a123a11c4c00be6c291ab3e486641f7.png)

obnizスタートガイド - obniz Docs
https://obniz.com/ja/doc/guides/

obniz はドキュメントが分かりやすく作例も豊富です。

## 今回は obniz Cloud で動かします

obniz Cloud 上のプログラムエディタで進めます。

## 開発者コンソールにログインします

開発者コンソール https://obniz.com/ja/console にアクセスします。

![714ed02daf0d3d99258b47773ff00af0](https://i.gyazo.com/714ed02daf0d3d99258b47773ff00af0.png)

右上のサインイン/サインアップボタンをクリックしてログインします。

## obniz の電源を入れて Wi-Fi 接続を待ちます

![0fbb43564ae734a665af62e317210877](https://i.gyazo.com/0fbb43564ae734a665af62e317210877.png)

右メニューから管理＞デバイスをクリックして、今回登録した obniz が探します。

![4542f62008aee07f61407db7d86b4c77](https://i.gyazo.com/4542f62008aee07f61407db7d86b4c77.png)

登録されていて Offline であることを確認します。

![0dcad23a2030b258bb62570f6ca23ed1](https://i.gyazo.com/0dcad23a2030b258bb62570f6ca23ed1.jpg)

obniz に電源を入れます。このとき、ノートパソコンの上など金属面や通電してしまうところには置かないようにしましょう。QR コードが出ている状態になれば接続中です。

![8c78a67bf0fca8203b2e123ee2d89392](https://i.gyazo.com/8c78a67bf0fca8203b2e123ee2d89392.png)

デバイス管理でも Online になっていることを確認します。

![](https://obniz.com/ja/doc/reference/images/how_main_2x.png)

これで obniz クラウドと obniz デバイスがつながってプログラムで指示を出すことができます。

## obniz ID を確認

![0dcad23a2030b258bb62570f6ca23ed1](https://i.gyazo.com/0dcad23a2030b258bb62570f6ca23ed1.jpg)

obniz ID と書かれている XXX-XXXX という ID が指示を出すために必要です。メモしておきましょう。