# 人感センサーを LINE Notify に通知しよう

![74bfb8515c6e0611801269cd16d73af9](https://i.gyazo.com/74bfb8515c6e0611801269cd16d73af9.jpg)

人感センサーを LINE Notify に通知してみましょう。

## つないでみる

![4dd5af256639b05059a5014812221352](https://i.gyazo.com/4dd5af256639b05059a5014812221352.jpg)

スターターキットにある人感センサを動かしてみましょう。

ドキュメントは https://obniz.com/ja/sdk/parts/Keyestudio_PIR/README.md にあります。

![1af5c0b3cd1056378a9e863afa798ed2](https://i.gyazo.com/1af5c0b3cd1056378a9e863afa798ed2.jpg)

このように S の刻印を 0 番ピン穴に合わせて挿しこみます。

## シンプルにセンサー単体で動かしてみる

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
    <h1>PIR</h1>

    <div id="obniz-debug"></div>

    <script>

      // 今回の obniz を指示するための設定
      const obniz = new Obniz("OBNIZ_ID_HERE");
      // 接続後、センサーを動かす
      obniz.onconnect = async function () {
        obniz.display.clear();
        obniz.display.print("[PIR]");
        // PIR の呼び出し
        var sensor = obniz.wired("Keyestudio_PIR", {signal:0, vcc:1, gnd:2});
        // 人の気配があるかを検知
        sensor.onchange = function(val){
          if(val){
              obniz.display.clear();
              obniz.display.print("(0o0)< Moving!");
              console.log("Moving!");
          } else {
              obniz.display.clear();
              obniz.display.print("(-_-)");
              console.log("Nothing moving");
          }
        }
      }
      
    </script>
  </body>
</html>
```

今回のプログラムを実行してみましょう。

![94fce9a30f48153897a63e3ae8051a4b](https://i.gyazo.com/94fce9a30f48153897a63e3ae8051a4b.jpg)

手をかざすと動きがあった判断してに、このように (0o0)< Moving! と知らせてくれます。人感センサーは、熱源の動きを判断します。

## 人感センサーを LINE Notify と連携してみる

人感センサーの反応をLINE Notify と連携してみましょう。

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

      // 接続後、センサーを動かす
      obniz.onconnect = async function () {
        obniz.display.clear();
        obniz.display.print("[PIR]");
        // PIR の呼び出し
        var sensor = obniz.wired("Keyestudio_PIR", {signal:0, vcc:1, gnd:2});
        // 人の気配があるかを検知
        sensor.onchange = function(val){
          if(val){
              obniz.display.clear();
              obniz.display.print("(0o0)< Moving!");
              console.log("Moving!");
              sendIFTTT("(0o0)< 動いたよ！");
          } else {
              obniz.display.clear();
              obniz.display.print("(-_-)");
              console.log("Nothing moving");
              sendIFTTT("(-_-)");
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

![74bfb8515c6e0611801269cd16d73af9](https://i.gyazo.com/74bfb8515c6e0611801269cd16d73af9.jpg)

こちらを実行して人感センサーに手をかざしてみると、LINE Notify にこのように  (0o0)< Moving! や (-_-) と知らせてくれます。

## 終了する

![458bed935aa2dbcef07333fb1c676b43](https://i.gyazo.com/458bed935aa2dbcef07333fb1c676b43.png)

右上の終了ボタンをクリックします。

![0dcad23a2030b258bb62570f6ca23ed1](https://i.gyazo.com/0dcad23a2030b258bb62570f6ca23ed1.jpg)

終了をすると obniz が処理待ちに戻ります。

## TIPS

![d35d834c4ecad8cfba42d6ab3be97bc4](https://i.gyazo.com/d35d834c4ecad8cfba42d6ab3be97bc4.png)

人感センサーは、反射板や金属物で遮蔽できます。センサー部分の検知範囲が広い場合は、アルミホイルで覆って必要な部分を爪楊枝などで穴をあけたり、粘土のようなもので検知したい範囲以外は覆ってしまうようなテクニックがあります。