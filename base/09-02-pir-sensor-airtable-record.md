# 人感センサーのデータを Airtable に送ってみよう

<img width="612.75" alt="2022-12-23 17.03.33.png (10.0 kB)" src="https://img.esa.io/uploads/production/attachments/3062/2022/12/23/8131/df5a1018-810d-4172-b442-def3fb8bd354.png">

人感センサーのデータを Airtable に送ってみましょう。

## つないでみる

![4dd5af256639b05059a5014812221352](https://i.gyazo.com/4dd5af256639b05059a5014812221352.jpg)

スターターキットにある人感センサを動かしてみましょう。

ドキュメントは https://obniz.com/ja/sdk/parts/Keyestudio_PIR/README.md にあります。

![1af5c0b3cd1056378a9e863afa798ed2](https://i.gyazo.com/1af5c0b3cd1056378a9e863afa798ed2.jpg)

このように S の刻印を 0 番ピン穴に合わせて挿しこみます。

## obniz を動かしてみる

人感センサーのデータを Airtable に送ってみましょう。

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
    <h1>PIR sensor record to Airtable</h1>

    <div id="obniz-debug"></div>

    <script>

      // 今回の obniz を指示するための設定
      const obniz = new Obniz("OBNIZ_ID_HERE");
      // 今回使う IFTTT Webhook の自分のキー
      const IFTTT_WEBHOOK_YOUR_KEY = 'IFTTT_WEBHOOK_YOUR_KEY';
      // 今回使う IFTTT Webhook の Event Name
      const IFTTT_WEBHOOK_EVENT_NAME = 'airtable_record';

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
              sendIFTTT("動作検知");
          } else {
              obniz.display.clear();
              obniz.display.print("(-_-)");
              console.log("Nothing moving");
              sendIFTTT("--");
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

<img width="612.75" alt="2022-12-23 17.03.33.png (10.0 kB)" src="https://img.esa.io/uploads/production/attachments/3062/2022/12/23/8131/df5a1018-810d-4172-b442-def3fb8bd354.png">

こちらを実行して人感センサーに手をかざしてみると、Airtable の Name フィールドに、動作検知したら `動作検知`。動きが無くなれば `--` と記録してくれます。

## 終了する

![458bed935aa2dbcef07333fb1c676b43](https://i.gyazo.com/458bed935aa2dbcef07333fb1c676b43.png)

右上の終了ボタンをクリックします。

![0dcad23a2030b258bb62570f6ca23ed1](https://i.gyazo.com/0dcad23a2030b258bb62570f6ca23ed1.jpg)

終了をすると obniz が処理待ちに戻ります。
