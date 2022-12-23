# 超音波距離センサーを LINE Notify に通知しよう

![7cb0862217779ad0839c94dd359f365c](https://i.gyazo.com/7cb0862217779ad0839c94dd359f365c.jpg)

超音波距離センサーを LINE Notify に通知してみましょう。

## つないでみる

![ea6b803818c4c007e54a0fb321bcaf2c](https://i.gyazo.com/ea6b803818c4c007e54a0fb321bcaf2c.jpg)

スターターキットにある超音波距離センサーをつなぎます。

ドキュメントは https://obniz.com/ja/sdk/parts/HC-SR04/README.md にあります。

![7c8af2aa5ae307a9a95b6ac559fa0f32](https://i.gyazo.com/7c8af2aa5ae307a9a95b6ac559fa0f32.jpg)

このように、GND を 0 番ピンに合わせて挿しこみます。

![a621fe75d0993420dee8ffb009f5ae66](https://i.gyazo.com/a621fe75d0993420dee8ffb009f5ae66.jpg)

しっかり最後まで差し込みましょう。

## 超音波距離センサーを LINE Notify と連携してみる

超音波距離センサーの反応をLINE Notify と連携してみましょう。

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

      // 接続後、ディスプレイに指示を出して、センサー取得
      obniz.onconnect = async function () {
        console.log("[distance]");
        // ディスプレイ表示
        obniz.display.clear();
        obniz.display.print("[distance]");
        const hcsr04 = obniz.wired("HC-SR04", {gnd:0, echo:1, trigger:2, vcc:3});
        // 1秒ごとチェック
        obniz.onloop = async function () {
          // 距離取得
          const distanceMM = await hcsr04.measureWait();
          // 小数点切り捨て + mm から cm に変換
          const distanceCM = Math.floor(distanceMM / 10);
          console.log(`${distanceCM} cm`);
          // ディスプレイ表示
          obniz.display.clear();
          obniz.display.print(`${distanceCM} cm`);
          // 50 cm 以下だったら LINE Notify に通知
          if(distanceCM < 50){
            sendIFTTT('50 cm 以内に物体が近づいたよ！こわい！');
          }
          // 1秒ごと待つ
          await obniz.wait(1000);
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

![7cb0862217779ad0839c94dd359f365c](https://i.gyazo.com/7cb0862217779ad0839c94dd359f365c.jpg)

こちらを実行して超音波距離センサーに 50 cm 以内で手を近づけると、LINE Notify にこのように知らせてくれます。

## 変化した時だけ通知する場合

先ほどのプログラムですと、手をかざしていると 1 秒ごとに通知が来てしまいます。

変化があるときだけ行う場合は、以下のようにしましょう。

こちらを以前の内容は、すべて選択して消してから、エディタの内容を上書きして 'IFTTT_WEBHOOK_YOUR_KEY' シングルクオーテーションの中を IFTTT Webhook のキーに変更します。

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

      // 以前の状態の記録
      let previousStatus = 0;
      // 現在の状態の記録
      let currentStatus = 0;

      // 接続後、ディスプレイに指示を出して、センサー取得
      obniz.onconnect = async function () {
        console.log("[distance]");
        // ディスプレイ表示
        obniz.display.clear();
        obniz.display.print("[distance]");
        const hcsr04 = obniz.wired("HC-SR04", {gnd:0, echo:1, trigger:2, vcc:3});
        // 1秒ごとチェック
        obniz.onloop = async function () {
          // 距離取得
          const distanceMM = await hcsr04.measureWait();
          // 小数点切り捨て + mm から cm に変換
          const distanceCM = Math.floor(distanceMM / 10);
          console.log(`${distanceCM} cm`);
          // ディスプレイ表示
          obniz.display.clear();
          obniz.display.print(`${distanceCM} cm`);
          // 50 cm 以下だったら LINE Notify に通知
          if(distanceCM < 50){
            currentStatus = 1;  // 物体あり
          } else {
            currentStatus = 0;  // 物体なし
          }
          // 状態が変わったら通知
          if(currentStatus != previousStatus){
            if(currentStatus == 1){
              sendIFTTT('50 cm 以内に物体が近づいたよ！こわい！');
            } else {
              sendIFTTT('物体なし');
            }
            // 状態の記録
            previousStatus = currentStatus;
          }
          // 1秒ごと待つ
          await obniz.wait(1000);
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

previousStatus と currentStatus の値で状態を管理して、状態が変わったら、通知を送るようにしています。こうすることで、常に余分な通知せず、より良い仕組みを作ることができます。

![e97611242a73bd964f8282e55260a193](https://i.gyazo.com/e97611242a73bd964f8282e55260a193.jpg)

実行してみると、状態が変わった時だけ通知していて、物体なしの状態が続いても物体ありから変化したときにも送られてます。

## 終了する

![458bed935aa2dbcef07333fb1c676b43](https://i.gyazo.com/458bed935aa2dbcef07333fb1c676b43.png)

右上の終了ボタンをクリックします。

![0dcad23a2030b258bb62570f6ca23ed1](https://i.gyazo.com/0dcad23a2030b258bb62570f6ca23ed1.jpg)

終了をすると obniz が処理待ちに戻ります。
