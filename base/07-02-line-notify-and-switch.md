# 内蔵スイッチを LINE Notify に通知しよう

![2ce5be23e2d71ab0891d120cafec9abe](https://i.gyazo.com/2ce5be23e2d71ab0891d120cafec9abe.png)

内蔵スイッチを左右に回したり押したりすると LINE Notify にメッセージが届く仕組みを作ります。

## LINE Notify に送るためには

![e615b4141fbe46aceac07a633e80323d](https://i.gyazo.com/e615b4141fbe46aceac07a633e80323d.png)

まず、obniz クラウドはブラウザから LINE Notify にアクセスしようとすると、この場合 LINE Notify のサーバーが obniz.com からのアクセスを許可していないのでクロスドメインの制約からアクセスすることができません。

- 参考資料
    - <a href="https://developer.mozilla.org/ja/docs/Web/HTTP/CORS" target="_blank">オリジン間リソース共有 (CORS) - HTTP | MDN</a>

![e633777352d16bc7f28530bb7bbe7202](https://i.gyazo.com/e633777352d16bc7f28530bb7bbe7202.png)

この制約はブラウザで限った話でして、サーバー間のやりとりでは、その制約は受けません。ですので、今回は IFTTT が橋渡しの役目をします。IFTTT Webhook サービスを使って obniz のデータを受けて IFTTT が LINE Notify に橋渡しをするという仕組みで進めます。

![07644da20127606b61c3fd369e98c217](https://i.gyazo.com/07644da20127606b61c3fd369e98c217.png)

これが、事前準備で作った仕組みですね。

## 自作のサーバーや AWS Lambda のような仕組みが使える場合

![30d4c87d86ec7b8662d30f6111e5cf01](https://i.gyazo.com/30d4c87d86ec7b8662d30f6111e5cf01.png)

もし、自作のサーバーや AWS Lambda のような仕組みが使えるのであれば、CORS を obniz.com に解放してあげれば、サーバーにアクセスできるようになるので、そういった開発がハッカソンで出来るのであればやってみましょう。

- AWS Lambda の例
    - <a href="https://docs.aws.amazon.com/ja_jp/apigateway/latest/developerguide/how-to-cors.html" target="_blank">REST API リソースの CORS を有効にする - Amazon API Gateway</a>
- Node.js の Express サーバーの例
    - Node.js + Express で複数オリジンに対応した CORS の実装サンプル
        - http://dotnsf.blog.jp/archives/1080458826.html

CORS を obniz.com に解放を狙い撃ちで行うのが大変なときは、一度 * （アスタリスク）で全開放して試すとハマりにくくておススメです。その上で、絞りましょう。

チーム内でそういった対応ができる場合は、ぜひ相談してみましょう～。

## IFTTT Webhook のキーの準備

![dac67d3ad447bc2b43c97b861bfa3f57](https://i.gyazo.com/dac67d3ad447bc2b43c97b861bfa3f57.png)

事前準備で準備した、こちらの IFTTT Webhook のキーを手元に準備します。メモしてない方は、再度 https://ifttt.com/maker_webhooks から Documentation ボタンをクリックして設定を確認しましょう。

## シンプルに LINE Notify だけする

![8cd2c0dd521d06ef897bed45b8137819](https://i.gyazo.com/8cd2c0dd521d06ef897bed45b8137819.jpg)

はじめに、トークンなどの設定がうまく揃っているか、スイッチの連携をせずシンプルに LINE Notify だけやってみましょう。

こちらを以前の内容は、すべて選択して消してから、エディタの内容を上書きします。

```html
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
    <script src="https://obniz.io/js/jquery-3.2.1.min.js"></script>
    <script src="https://unpkg.com/obniz@3.24.0/obniz.js" crossorigin="anonymous"></script>
  </head>
  <body>
    <h1>Simple LINE Notify!</h1>

    <div id="obniz-debug"></div>

    <script>

      // 今回の obniz を指示するための設定
      const obniz = new Obniz("OBNIZ_ID_HERE");
      // 今回使う IFTTT Webhook の自分のキー
      const IFTTT_WEBHOOK_YOUR_KEY = 'IFTTT_WEBHOOK_YOUR_KEY';
      // 今回使う IFTTT Webhook の Event Name
      const IFTTT_WEBHOOK_EVENT_NAME = 'line_notify';
      
      // 接続後、ディスプレイに指示を出す
      obniz.onconnect = async function () {
        // ディスプレイ表示
        obniz.display.clear();
        obniz.display.print("Simple");
        obniz.display.print("LINE Notify");
        obniz.display.print("with IFTTT!");

        // IFTTT Webhook に fetch 関数で送る ////////////////////////////

        // メッセージ内容を URLSearchParams で作る
        // 実際のメッセージは message 値
        const params = new URLSearchParams({
            value1: 'シンプルに送ってみました！',
            value2: 'value2',
            value3: 'value3',
        });
        // 送る文字列に変換
        const paramsString = params.toString();
        // 設定
        const config = {
            method: 'GET',
            mode: 'no-cors',
            headers: {
                'Content-Type': 'application/x-www-form-urlencoded'
            }
        };
        // IFTTT Webhook の URL をつくる
        const IFTTT_WEBHOOK_URL = `https://maker.ifttt.com/trigger/${IFTTT_WEBHOOK_EVENT_NAME}/with/key/${IFTTT_WEBHOOK_YOUR_KEY}?${paramsString}`;
        console.log("IFTTT_WEBHOOK_URL");
        console.log(IFTTT_WEBHOOK_URL);
        // 送信
        await fetch(IFTTT_WEBHOOK_URL, config);

        console.log("OK")

      }
      
    </script>
  </body>
</html>
```

コピーアンドペーストできたら、

```js
      // 今回使う IFTTT Webhook の自分のキー
      const IFTTT_WEBHOOK_YOUR_KEY = 'IFTTT_WEBHOOK_YOUR_KEY';
```

の 'IFTTT_WEBHOOK_YOUR_KEY' シングルクオーテーションの中を IFTTT Webhook のキーに変更します。

こちらを実行してみると、LINE Notify に「シンプルに送ってみました！」というメッセージが送られます。

![2ce5be23e2d71ab0891d120cafec9abe](https://i.gyazo.com/2ce5be23e2d71ab0891d120cafec9abe.png)

スマホの LINE アプリケーションを見てみると、今回送った LINE Notify にメッセージがこのように送られています！

## 今回の fetch は GET リクエストで no-cors モード

```js
        // 設定
        const config = {
            method: 'GET',
            mode: 'no-cors',
            headers: {
                'Content-Type': 'application/x-www-form-urlencoded'
            }
        };
```

IFTTT の Webhook は GET リクエストで application/x-www-form-urlencoded 形式でデータを受け付けることができるため、今回はこのようにしています。また、mode を no-cors を CORS に影響されないデータ送信方法なので、そう設定しています。

no-cors 送信は、データを送るだけなら問題なくできるので、今回は使えます。もし、データの受信も含めたやり取りをしたい場合は、前述の通り自前のサーバー側で CORS を許可しましょう。

- fetchのmodeについて - Qiita
    - https://qiita.com/ryokkkke/items/79f1d338e141d4b7201b

## メッセージを変更してみましょう

IFTTT Webhook には value1 value2 value3 という 3 つのメッセージを受け付けています。

```
        // メッセージ内容を URLSearchParams で作る
        // 実際のメッセージは message 値
        const params = new URLSearchParams({
            value1: 'シンプルに送ってみました！',
            value2: 'value2',
            value3: 'value3',
        });
```

こちらの `value1: 'シンプルに送ってみました！',` の部分がメッセージです。「シンプルに送ってみました！」の部分を変更してメッセージを変更してみましょう。

![117a7400f745a63b0c66fe5007d16346](https://i.gyazo.com/117a7400f745a63b0c66fe5007d16346.png)

なおメッセージの文言は、IFTTT の Applet 内で Message の項目で設定していました。

## 内蔵スイッチと連携してみる

![a49e987053d5f18cacf77f2d6f2b5370](https://i.gyazo.com/a49e987053d5f18cacf77f2d6f2b5370.jpg)

つづいて、内蔵スイッチと連携してみましょう。内蔵スイッチを左右に回したり押したりすると LINE Notify にメッセージが届く仕組みを作ります。

こちらを以前の内容は、すべて選択して消してから、エディタの内容を上書きします。

```html
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
    <script src="https://obniz.io/js/jquery-3.2.1.min.js"></script>
    <script src="https://unpkg.com/obniz@3.24.0/obniz.js" crossorigin="anonymous"></script>
  </head>
  <body>
    <h1>Simple LINE Notify!</h1>

    <div id="obniz-debug"></div>

    <script>

      // 今回の obniz を指示するための設定
      const obniz = new Obniz("OBNIZ_ID_HERE");
      // 今回使う IFTTT Webhook の自分のキー
      const IFTTT_WEBHOOK_YOUR_KEY = 'IFTTT_WEBHOOK_YOUR_KEY';
      // 今回使う IFTTT Webhook の Event Name
      const IFTTT_WEBHOOK_EVENT_NAME = 'line_notify';
      
      // 接続後、ディスプレイに指示を出す
      obniz.onconnect = async function () {
        console.log("[switch]");
        // ディスプレイ表示
        obniz.display.clear();
        obniz.display.print("[switch]");
        obniz.display.print("LINE Notify");
        obniz.display.print("with IFTTT!");
        // スイッチの動きを検出
        obniz.switch.onchange = function (state) {
          if (state === "push") {
            // 押されたとき
            console.log("push");
            // ディスプレイ表示
            obniz.display.clear();
            obniz.display.print("push");
            // メッセージを送る
            sendIFTTT("push");
          } else if (state === "right") {
            // 右に回したとき
            console.log("right");
            // ディスプレイ表示
            obniz.display.clear();
            obniz.display.print("right");
            // メッセージを送る
            sendIFTTT("right");
          } else if (state === "left") {
            // 左に回したとき
            console.log("left");
            // ディスプレイ表示
            obniz.display.clear();
            obniz.display.print("left");
            // メッセージを送る
            sendIFTTT("left");
          } else if (state === "none") {
            // 何もしていない時
            console.log("none");
            // ディスプレイ表示
            obniz.display.clear();
            obniz.display.print("none");
          }
        }
      }

      async function sendIFTTT(message) {
        // IFTTT Webhook に fetch 関数で送る ////////////////////////////

        // メッセージ内容を URLSearchParams で作る
        // 実際のメッセージは message 値
        const params = new URLSearchParams({
            value1: message,
            value2: 'value2',
            value3: 'value3',
        });
        // 送る文字列に変換
        const paramsString = params.toString();
        // 設定
        const config = {
            method: 'GET',
            mode: 'no-cors',
            headers: {
                'Content-Type': 'application/x-www-form-urlencoded'
            }
        };
        // IFTTT Webhook の URL をつくる
        const IFTTT_WEBHOOK_URL = `https://maker.ifttt.com/trigger/${IFTTT_WEBHOOK_EVENT_NAME}/with/key/${IFTTT_WEBHOOK_YOUR_KEY}?${paramsString}`;
        console.log("IFTTT_WEBHOOK_URL");
        console.log(IFTTT_WEBHOOK_URL);
        // 送信
        await fetch(IFTTT_WEBHOOK_URL, config);

        console.log("OK")

      }
      
    </script>
  </body>
</html>
```

コピーアンドペーストできたら、

```js
      // 今回使う IFTTT Webhook の自分のキー
      const IFTTT_WEBHOOK_YOUR_KEY = 'IFTTT_WEBHOOK_YOUR_KEY';
```

の 'IFTTT_WEBHOOK_YOUR_KEY' シングルクオーテーションの中を IFTTT Webhook のキーに変更します。

![a49e987053d5f18cacf77f2d6f2b5370](https://i.gyazo.com/a49e987053d5f18cacf77f2d6f2b5370.jpg)

こちらを実行して内蔵スイッチを右・左・押してみると、LINE Notify に left right push が送られます。

## 余分な文字を減らしてメッセージを整える

IFTTT で受け付けたメッセージが編集できます。

![117a7400f745a63b0c66fe5007d16346](https://i.gyazo.com/117a7400f745a63b0c66fe5007d16346.png)

このメッセージですと value2 value3 をメッセージを受け付けていますが、今回は value1 しか使いません。ちょっと整形してみましょう。

![51e9e7347eeafda5cd51f6885e95d05c](https://i.gyazo.com/51e9e7347eeafda5cd51f6885e95d05c.png)

IFTTT の今回の Applet に移動します。IFTTT にアクセスして上部メニューの My Applet から Applet 一覧を表示し、今回の Applet をクリックします。

![5baf9f537672a38595a2cf98fa76cbec](https://i.gyazo.com/5baf9f537672a38595a2cf98fa76cbec.png)

今回の Applet の右上の Settings ボタンをクリックして設定を表示します。

![30bdaeed0d6937d7fdfd6fa7ae05ff73](https://i.gyazo.com/30bdaeed0d6937d7fdfd6fa7ae05ff73.png)

Then の LINE の設定をクリックします。

![8d4dcaf734d3f98922edcfa9f8824439](https://i.gyazo.com/8d4dcaf734d3f98922edcfa9f8824439.png)

設定が表示されたら Message のフィールドをクリックすると `{{Value1}}` を囲われた部分が、Webhook から来た値 Value1 と置き換えます。

![00141bc7bac7dd00615a54253b926db2](https://i.gyazo.com/00141bc7bac7dd00615a54253b926db2.png)

ちなみに、右下の Add ingredient をクリックすると、Webhook からもらえる値の一覧が表示されクリックすると `{{　}}` つきで入力できます。（今回は特に追加で入れるのではなく、減らしていくで操作する必要はありません）

![2e12095b7d448dc033dccd0471f4ec65](https://i.gyazo.com/2e12095b7d448dc033dccd0471f4ec65.png)

ということで、Message フィールド内をこのように編集します。 `{{Value1}}` だけのシンプルなものです。編集できたら Update action をクリックします。

![cd7be3a76681f8c66c9dde80911ac261](https://i.gyazo.com/cd7be3a76681f8c66c9dde80911ac261.png)

前のページに戻って、Edit Applet の画面に戻るので Update ボタンをクリックして設定を反映します。

これで準備が完了です。

![d1ced7251548897899282086f0ff416b](https://i.gyazo.com/d1ced7251548897899282086f0ff416b.jpg)

再度 obniz を実行してみると、メッセージの内容がシンプルになります！

このように、obniz クラウドからはシンプルに値を送り IFTTT 側で、メッセージを調整することができます。

## 終了する

![458bed935aa2dbcef07333fb1c676b43](https://i.gyazo.com/458bed935aa2dbcef07333fb1c676b43.png)

右上の終了ボタンをクリックします。

![0dcad23a2030b258bb62570f6ca23ed1](https://i.gyazo.com/0dcad23a2030b258bb62570f6ca23ed1.jpg)

終了をすると obniz が処理待ちに戻ります。