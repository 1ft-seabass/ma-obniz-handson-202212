# MESH と連携しよう

## つなぎ方の解説

私のほうで、自前の MESH ボタンをつないでみた記事があるので、これを元に一連の流れを解説します。

![18c01af30384f682f476a4f0b01e29ef](https://i.gyazo.com/18c01af30384f682f476a4f0b01e29ef.jpg)

- MESH ボタンを 1.2.5 にアップデートして obniz とつなぐメモ
    - https://www.1ft-seabass.jp/memo/2022/12/06/mesh-version-up-meets-obniz-first-contact/

## 動きブロックでデモしてみます

![5e4be58b71d8ee1a298352c8d9b16a64](https://i.gyazo.com/5e4be58b71d8ee1a298352c8d9b16a64.jpg)

MESH 動きブロックと obniz を連携してみましょう。

最近購入した MESH であればバージョンが 1.2.5 になっているので、すぐ使えるはずです。

![81e6009bbbab6bf551a69a05e089fa1b](https://i.gyazo.com/81e6009bbbab6bf551a69a05e089fa1b.jpg)

このようにスイッチを押して起動します。LED が暗いところからフワッと明るく点灯すると電源オンです。

電源オンの具体的な LED の光り方や電池残量の確認法など、こまかな MESH の挙動は https://www.youtube.com/watch?v=G2e2s5kKBC0&list=PLQM9GimvERzs2NZBCkvk33cn4ccKAeEI7&index=6 こちらの動画を参考にしましょう。

MESH のパーツライブラリは https://obniz.com/ja/sdk/parts?q=MESH にあり、MESH 動きブロックは https://obniz.com/ja/sdk/parts/MESH_100AC/README.md にドキュメントがあります。

先ほどの記事でも触れましたが MESH のサンプルは、全部のコードが載っているわけではないので、サンプルコードを持って来て obniz クラウド用に書き加えます。

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
    <h1>MESH Move</h1>
    
    <script>

      // 今回の obniz を指示するための設定
      const obniz = new Obniz("OBNIZ_ID_HERE");

      // 接続後、MESH と接続
      obniz.onconnect = async function () {
        obniz.display.clear();
        obniz.display.print("[MESH Move]");

        const MESH_100AC = Obniz.getPartsClass('MESH_100AC');

        // BLE の初期化待ちコードを加えます
        await obniz.ble.initWait();

        obniz.ble.scan.onfind = async (peripheral) => {

          if (!MESH_100AC.isMESHblock(peripheral)) {
              return;
          }
          console.log('found');

          // Create an instance
          const moveBlock = new MESH_100AC(peripheral);

          // Connect to the Move block
          await moveBlock.connectWait();
          console.log(`connected: ${moveBlock.peripheral.localName}`);
          
          // Tap Event
          moveBlock.onTapped = (accele) => {
              console.log('tapped! (ax, ay, az) = (' + accele.x + ', ' + accele.y + ',' + accele.z + ')');
          };

          // Shake Event
          moveBlock.onShaked = (accele) => {
              console.log('shaked! (ax, ay, az) = (' + accele.x + ', ' + accele.y + ',' + accele.z + ')');
          };

          // Flip Event
          moveBlock.onFlipped = (accele) => {
              console.log('flipped! (ax, ay, az) = (' + accele.x + ', ' + accele.y + ',' + accele.z + ')');
          };
          
          // Orientation Event
          moveBlock.onOrientationChanged = (orientation, accele) => {
              console.log('orientation changed! ' + orientation + ', (ax, ay, az) = (' + accele.x + ', ' + accele.y + ',' + accele.z + ')');
          };
        };

        // スキャンの開始待ちのコードを加えます
        await obniz.ble.scan.startWait();
      }
      
    </script>
  </body>
```

こちらを実行してみると

![28aa8290c46c8b039be270adc8fb0a12](https://i.gyazo.com/28aa8290c46c8b039be270adc8fb0a12.png)

found と出て MESH が見つかってしばらく待つと接続されます。

![34b1468491c13e7a98112b9544c3a972](https://i.gyazo.com/34b1468491c13e7a98112b9544c3a972.png)

shaked は振られた時、tapped はトンっと叩かれた時、orientation changed は面が変わった時、flipped はひっくり返したときです。

こういった動きは、各 MESH タグでスマホアプリからつないだ設定項目で分かります。また、obniz ドキュメントからたどれる MESH の [技術仕様書](https://developer.meshprj.com/hc/ja/categories/8286129859737-MESH-%E3%83%96%E3%83%AD%E3%83%83%E3%82%AF-%E6%8A%80%E8%A1%93%E4%BB%95%E6%A7%98) もおすすめです。

![569c7be5b3ce86213f43e86c5ba4c2a1](https://i.gyazo.com/569c7be5b3ce86213f43e86c5ba4c2a1.png)

たとえば、動きブロックの仕様書はこのようになります。 → https://developer.meshprj.com/hc/ja/articles/8286418941977-%E5%8B%95%E3%81%8D%E3%83%96%E3%83%AD%E3%83%83%E3%82%AF-MESH-100AC-

## 複数の MESH があるときに特定の MESH につなげるには

![28aa8290c46c8b039be270adc8fb0a12](https://i.gyazo.com/28aa8290c46c8b039be270adc8fb0a12.png)

ハッカソンの現場では複数の MESH が飛び交って、いまのコードだと違う動き MESH につながってしまう可能性があります。そういうときは found 後の connected 接続時の peripheral.localName の値で if 文で区別すると良いです。

```js
          // Connect to the Move block
          await moveBlock.connectWait();
          console.log(`connected: ${moveBlock.peripheral.localName}`);
```

さきほどの、コードだとここです。moveBlock の部分は、各ブロックのサンプルで変わりますので確認してみましょう。

![5616b79af74ab07d45a35a4b834e5784](https://i.gyazo.com/5616b79af74ab07d45a35a4b834e5784.jpg)

動きブロックの場合 MESH-100AC というブロックの名称に MESH 本体に書いてある SN というシリアルナンバーが付与したものになります。他のブロックでも、そのブロックの名称＋シリアルナンバーで区別できます。わざわざ一度つながなくても、事前に推測できます。

この写真のように、そのブロックの型番は 2 行目と SN は 4 行目に本体に書かれています。

## 動きブロックを振ると LINE Notify を通知してみる

![53f8c51c13b4ba0786cb12e296e6ff4b](https://i.gyazo.com/53f8c51c13b4ba0786cb12e296e6ff4b.png)

動きブロックを振ると LINE Notify を通知してみましょう。

以前の内容は、すべて選択して消してから、エディタの内容をこちらで上書きします。

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
    <h1>MESH Move</h1>
    
    <script>

      // 今回の obniz を指示するための設定
      const obniz = new Obniz("OBNIZ_ID_HERE");
      // 今回使う IFTTT Webhook の自分のキー
      const IFTTT_WEBHOOK_YOUR_KEY = 'IFTTT_WEBHOOK_YOUR_KEY';
      // 今回使う IFTTT Webhook の Event Name
      const IFTTT_WEBHOOK_EVENT_NAME = 'line_notify';

      // 接続後、MESH と接続
      obniz.onconnect = async function () {
        obniz.display.clear();
        obniz.display.print("[MESH Move]");

        const MESH_100AC = Obniz.getPartsClass('MESH_100AC');

        // BLE の初期化待ちコードを加えます
        await obniz.ble.initWait();

        obniz.ble.scan.onfind = async (peripheral) => {

          if (!MESH_100AC.isMESHblock(peripheral)) {
              return;
          }
          console.log('found');
          obniz.display.print('found');

          // Create an instance
          const moveBlock = new MESH_100AC(peripheral);

          // Connect to the Move block
          await moveBlock.connectWait();
          console.log(`connected: ${moveBlock.peripheral.localName}`);
          obniz.display.print('connected');

          // 振った時だけ LINE Notify に通知
          moveBlock.onShaked = (accele) => {
              console.log('shaked! (ax, ay, az) = (' + accele.x + ', ' + accele.y + ',' + accele.z + ')');
              // ディスプレイに表示
              obniz.display.clear();
              obniz.display.print('onShaked');
              // 通知
              sendIFTTT('MESH 動きタグが振られました！');
          };
        };

        // スキャンの開始待ちのコードを加えます
        await obniz.ble.scan.startWait();
      }

      async function sendIFTTT(message) {
        // IFTTT Webhook に fetch 関数で送る ////////////////////////////

        // メッセージ内容を URLSearchParams で作る
        // 実際のメッセージは message 値
        const params = new URLSearchParams({
            value1: message
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
```

コピーアンドペーストできたら、

```js
      // 今回使う IFTTT Webhook の自分のキー
      const IFTTT_WEBHOOK_YOUR_KEY = 'IFTTT_WEBHOOK_YOUR_KEY';
```

の 'IFTTT_WEBHOOK_YOUR_KEY' シングルクオーテーションの中を IFTTT Webhook のキーに変更します。

こちらを実行してみて、ディスプレイが found と connected が出たら MESH と接続できています。

![53f8c51c13b4ba0786cb12e296e6ff4b](https://i.gyazo.com/53f8c51c13b4ba0786cb12e296e6ff4b.png)

振ってみると LINE Notify にメッセージが送られます。

## Uncaught ObnizBleHciStateError: Connection Failed to be Established / Synchronization Timeout

これが出たら、一度 obniz 実行を止めてつなぎなおすとうまくいきます。

## Uncaught MESHJsBlockVersionError: Please UPDATE the block software to version 1.2.5 or higher. (Current block software version is 1.1.5 .)

このようなエラーが出てきたら、MESH のバージョンアップが必要です。[こちらの記事](https://www.1ft-seabass.jp/memo/2022/12/06/mesh-version-up-meets-obniz-first-contact/) を参考にアップデートしましょう。


## IFTTT と MESH アプリの連携もいけます

実は IFTTT と MESH アプリの連携もできます。

<img width="1253" alt="2022-12-24 16.18.34.jpg (97.3 kB)" src="https://img.esa.io/uploads/production/attachments/3062/2022/12/24/8131/a140adab-a826-46ad-9359-70371719e3af.jpg">

- IFTTTを使ってWEBサービスと連携しよう
    - https://www.get.meshprj.com/iftttapplet

<img width="740" alt="2022-12-24 16.19.17.jpg (86.1 kB)" src="https://img.esa.io/uploads/production/attachments/3062/2022/12/24/8131/52a9224c-a677-4046-9571-846d4406b80a.jpg">

- IFTTTアプレットの使いかた
    - https://support.meshprj.com/hc/ja/articles/115003497128

おもしろいですよね。ただ、MESH アプリが直感的とはいえアプリの使い方を学ぶ必要があるのと、スマートフォンでアプリを起動し続ける運用をします。ちょっと MESH と アプリの接続で苦労することもあるかもしれず、使いこなすには若干の慣れが必要があります。