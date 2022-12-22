# IFTTT 準備

## IFTTT とは

![d8a987c6fc09b42bb8ba8f83a6ad8c26](https://i.gyazo.com/d8a987c6fc09b42bb8ba8f83a6ad8c26.png)

「if this then that」（もしこれが起こったらあれする）というシンプルなコンセプトに基づく、さまざまな API と API をつなぐ「レシピ」を作成し共有することができます。頭文字を取って IFTTT イフト と言います。

レシピの「this」の部分は「Facebookで写真をタグ付けした時」「Webhook でデータが来たとき」といった「きっかけ」になります。「that」の部分は「LINE Notify メッセージの送信」「Twitter にメッセージを作成」「Airtable にデータを保存」といった「アクション」になります。

ユーザーが使用するさまざまなサービスで有効にすることで「きっかけ」と「アクション」に使うことができます。今回はアカウントを作り Webhook、LINE Notify、Airtable を有効にしましょう。

- 参考文献
    - https://ja.wikipedia.org/wiki/IFTTT

## アカウント作成

![04b48a54893926c165c3c16e7f4c0691](https://i.gyazo.com/04b48a54893926c165c3c16e7f4c0691.png)

https://ifttt.com/ にアクセスして右上の Get Started ボタンをクリックします。

![3d3974e5792697f7670242d39839db66](https://i.gyazo.com/3d3974e5792697f7670242d39839db66.png)

Get started with IFTTT のページに移動します。Or use your email to sign up or log in のところの sign up をクリックします。

![50f3f91a3fbd9f6d13017da501587098](https://i.gyazo.com/50f3f91a3fbd9f6d13017da501587098.png)

メールアドレスでのサインアップページです。

![f96f81bb06683c1bb5f4cbb86c084757](https://i.gyazo.com/f96f81bb06683c1bb5f4cbb86c084757.png)

メールアドレスとパスワードを決めて Get started ボタンをクリックします。

![91a429a74ea68d362f105b9f417a5f3f](https://i.gyazo.com/91a429a74ea68d362f105b9f417a5f3f.png)

Neither  を選択して Continue ボタンをクリックします。

![27defc0973e837909d23c61a37b303fc](https://i.gyazo.com/27defc0973e837909d23c61a37b303fc.png)

Date & Time をクリックして Continue ボタンをクリックします。

![cb06bf7aa9c7f0baf059df6b0b16909d](https://i.gyazo.com/cb06bf7aa9c7f0baf059df6b0b16909d.png)

Not now をクリックします。

![c7a44b1df2f3ba92f1a510a2dec45f9d](https://i.gyazo.com/c7a44b1df2f3ba92f1a510a2dec45f9d.png)

Get started をクリックします。

![2ce3e0e65c0ad0575a9dd3a2e9667551](https://i.gyazo.com/2ce3e0e65c0ad0575a9dd3a2e9667551.png)

Explore のページに移動したら、あとは、メール認証だけです。今回登録したメールアドレスのメールボックスを見に行きましょう。

![6cabffc6624616525693d3a804ecbf03](https://i.gyazo.com/6cabffc6624616525693d3a804ecbf03.png)

このように今回登録したメールアドレスのメールボックスにメールが来るはずなので Confirm your email ボタンをクリックします。もしも、数分経って見当たらない場合は、迷惑メールに振り分けられている場合もあるので、確認してみましょう。

![8cce51ca468d07f0ca2d08163d14cbeb](https://i.gyazo.com/8cce51ca468d07f0ca2d08163d14cbeb.png)

Explore のページがブラウザで開いて認証完了です。

![7e63d8a01102bbae124a28eefb92048d](https://i.gyazo.com/7e63d8a01102bbae124a28eefb92048d.png)

また、もう少し待っていると Welcome to IFTTT のメールも来ます。これで、よりアカウント登録が完了したことが分かります！

## Webhook integrations の有効化

![8e502783f7a97b0b6e5977a943f7e7d5](https://i.gyazo.com/8e502783f7a97b0b6e5977a943f7e7d5.png)

https://ifttt.com/explore で、サービス検索をします。

![91daaa6006cab39287068832f76ae8f3](https://i.gyazo.com/91daaa6006cab39287068832f76ae8f3.png)

Webhook で検索して Webhooks をクリックします。

![ca57144010dd0ad73fa58a0185c7399c](https://i.gyazo.com/ca57144010dd0ad73fa58a0185c7399c.png)

Webhooks integrations の詳細が表示されます。Connect ボタンをクリックしましょう。

![02cf5072b534ed5b997341f52921af87](https://i.gyazo.com/02cf5072b534ed5b997341f52921af87.png)

無事 Connect できると、このように Create ボタンを Documentation ボタンが表示されます。

## Webhook integrations キーのメモ

![02cf5072b534ed5b997341f52921af87](https://i.gyazo.com/02cf5072b534ed5b997341f52921af87.png)

Documentation ボタンをクリックします。

![dac67d3ad447bc2b43c97b861bfa3f57](https://i.gyazo.com/dac67d3ad447bc2b43c97b861bfa3f57.png)

Your key is のページが表示されるので、Your key is の下部の赤矢印のキーを最初から最後までコピーします。コピー漏れに気をつけましょう。

これは当日使います。テキストエディタでメモして保存しておきましょう。

## LINE integrations の有効化

LINE Notify の設定を済ませてから有効化しましょう。

![8e502783f7a97b0b6e5977a943f7e7d5](https://i.gyazo.com/8e502783f7a97b0b6e5977a943f7e7d5.png)

https://ifttt.com/explore で、サービス検索をします。

![cdf7895eff7aa55bcb166aadd268ad80](https://i.gyazo.com/cdf7895eff7aa55bcb166aadd268ad80.png)

LINE で検索して LINE をクリックします。

![47e69917edfc1527f1f3b2b5760ee29a](https://i.gyazo.com/47e69917edfc1527f1f3b2b5760ee29a.png)

https://ifttt.com/line の LINE サービスを関連付けるページです。Connect ボタンをクリックします。

![6dcc86ca9bdfa588ef228bfe37de804a](https://i.gyazo.com/6dcc86ca9bdfa588ef228bfe37de804a.png)

QR コードでログインします。

![2dadc692ebf32354324423bf3770b39a](https://i.gyazo.com/2dadc692ebf32354324423bf3770b39a.png)

同意して連携するボタンをクリックします。

![aa805b48325d98e38b047280509b9f97](https://i.gyazo.com/aa805b48325d98e38b047280509b9f97.png)

接続されると Create ボタンと Download ボタンがある、このような画面になり LINE integrations の設定が完了です。

## Airtable integrations の有効化

![8e502783f7a97b0b6e5977a943f7e7d5](https://i.gyazo.com/8e502783f7a97b0b6e5977a943f7e7d5.png)

https://ifttt.com/explore で、サービス検索をします。

![7d978aeb192e5ae06ffe551de9ceee30](https://i.gyazo.com/7d978aeb192e5ae06ffe551de9ceee30.png)

Airtable で検索して Airtable をクリックします。

![4d745cde667fb89f9251df67618d5cc6](https://i.gyazo.com/4d745cde667fb89f9251df67618d5cc6.png)

Webhooks integrations の詳細が表示されます。Connect ボタンをクリックしましょう。

![bad42826c94a6201df96798e826fa99d](https://i.gyazo.com/bad42826c94a6201df96798e826fa99d.png)

Airtable 側のログイン画面が表示されます。Airtable アカウントとパスワードを入力してログインします。なお、Airtable に既にログインしている場合は、自動的に接続されるようです。

![42929fc536d14abf772c62e3a99ef74b](https://i.gyazo.com/42929fc536d14abf772c62e3a99ef74b.png)

接続されると Create ボタンと Download ボタンがある、このような画面になり Airtable integrations の設定が完了です。