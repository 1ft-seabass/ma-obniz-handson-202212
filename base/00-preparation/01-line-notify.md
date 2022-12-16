# LINE Notify アクセストークン作成

## LINE アカウント確認

<img src="https://guide.line.me/ja/install_5.png" width="200" />

LINE アカウント自体の作成とスマホアプリインストールを確認します。

もし、自分のスマホに LINE スマホアプリがあり、すでに LINE でチャットができているのならこの作業はしなくて OK です。

## LINE Notify サイトログイン

LINE Notify サイトにログインしアカウント確認をします。

![image](https://i.gyazo.com/c45ee309aa6793bc12f67c24f3a905ce.png)

https://notify-bot.line.me/ja/ に、まずアクセスします。

![image](https://i.gyazo.com/043d433bfa913e2edaee4bb917e92bb2.png)

右上のログインをクリック。

![image](https://i.gyazo.com/d2a7444465cb56a81eedb3e957403806.png)

下部の QR コードログインをクリックします。（メールアドレス・パスワードは、おそらくみなさん設定していないのと、いまから設定をやるとなると、PCとアプリを行き来して、まあまあ大変になるので今回は避けます。）

![image](https://i.gyazo.com/a6834bc86db3d0f024a0cb5886664883.png)

QR コードが表示されます。 LINE アプリでスキャンするとログインできます。QR コードのスキャン方法は下部のリンクをクリックすると表示されます。

![image](https://i.gyazo.com/e3856b10d3a1b933f284f7f81f3fac64.png)

## LINE Notify 設定の取得

LINE Notify 設定しトークンの取得を行います。

![image](https://i.gyazo.com/bf26cdcf093a783aee4ff510ec9ddb68.png)

ログインすると、右上にアカウント名が出るのでクリックします。

![image](https://i.gyazo.com/7cdb07c7e588bac278a5fb0b2dbc9d83.png)

マイページをクリック。

![image](https://i.gyazo.com/0c48f49af1be4e5e7c789366c0b838cf.png)

マイページの下の方に「アクセストークンの発行(開発者向け)」というエリアがあるのでスクロールします。

![image](https://i.gyazo.com/bbba9909e0437e487718479953b198ff.png)

トークンを発行するボタンをクリックします。

![9dffc69323ea1282c052f5293b526e01](https://i.gyazo.com/9dffc69323ea1282c052f5293b526e01.png)

トークンを発行するウィンドウが表示されるので、以下のように対応します。

- トークン名を記入してください (通知の際に表示されます)
  - `First Notify` と入力
- 通知を送信するトークルームを選択してください
  - `1:1でLINE Notifyから通知を受け取る` を選択

こちらを対応すると、発行するボタンが押せるようになるのでクリックします。

![image](https://i.gyazo.com/abee7f38d2db6897c61cdb42fc29a83c.png)

このようにトークンが表示されるのでメモしましょう。

**このページから移動すると、新しく発行されたトークンは二度と表示されないので気をつけましょう**

メモしたらウィンドウを閉じるボタンをクリックして閉じます。

## LINE Notify 設定の確認

LINE で LINE Notify 設定されたかメッセージ確認を行います。

![a4b7b97567fe7842b7ccb7a1f2b84e7b](https://i.gyazo.com/a4b7b97567fe7842b7ccb7a1f2b84e7b.png)

リストに追加されたことを確認しておきます。

![image](https://i.gyazo.com/07a33eec5562fc6fd67e52aeaa5c2bc9.png)

今回選択した LINE Notify 先のアカウントにこのようなメッセージが来ていることも確認します。このように、LINE Notify API のアクセストークンの発行されると LINE アプリに Personal Access Token 発行の通知が来ます。

![081989e0296c7c8878b161bbb9a8c3c3](https://i.gyazo.com/081989e0296c7c8878b161bbb9a8c3c3.png)

こちらで準備完了です。お疲れ様でした。