# 超音波距離センサーの距離を表示しよう

![ea6b803818c4c007e54a0fb321bcaf2c](https://i.gyazo.com/ea6b803818c4c007e54a0fb321bcaf2c.jpg)

スターターキットにある超音波距離センサーから対象物とセンサーの距離を取得してみましょう。

ドキュメントは https://obniz.com/ja/sdk/parts/HC-SR04/README.md にあります。

![7c8af2aa5ae307a9a95b6ac559fa0f32](https://i.gyazo.com/7c8af2aa5ae307a9a95b6ac559fa0f32.jpg)

このように、GND を 0 番ピンに合わせて挿しこみます。

![a621fe75d0993420dee8ffb009f5ae66](https://i.gyazo.com/a621fe75d0993420dee8ffb009f5ae66.jpg)

しっかり最後まで差し込みましょう。

## エディタに反映

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
    <h1>Hello obniz!!!</h1>

    <div id="obniz-debug"></div>

    <script>

      // 今回の obniz を指示するための設定
      const obniz = new Obniz("OBNIZ_ID_HERE");
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
          // 1秒ごと待つ
          await obniz.wait(1000);
        }
      }
            
    </script>
  </body>
</html>
```

## 動かしてみる

![4b83ca1d7500f2e8a8fffa1292df9f6a](https://i.gyazo.com/4b83ca1d7500f2e8a8fffa1292df9f6a.png)

右上の実行ボタンをクリックして、実行してみましょう。

![3e178ead36eb2fe65e2e09c6aacbcaf9](https://i.gyazo.com/3e178ead36eb2fe65e2e09c6aacbcaf9.png)

Obniz ID を確認して Connect をクリックします。

![85572de0f71c89b2821390ff4a5c742b](https://i.gyazo.com/85572de0f71c89b2821390ff4a5c742b.jpg)

起動時は、おそらく天井や遠くの壁に跳ね返って長めの距離が表示されています。

![a8dce0285e1cdd3a9a6ba62e8507e020](https://i.gyazo.com/a8dce0285e1cdd3a9a6ba62e8507e020.jpg)

手をかぶせると、センサーと対象物（手）になるので距離が短くなるはずです。

## 終了する

![458bed935aa2dbcef07333fb1c676b43](https://i.gyazo.com/458bed935aa2dbcef07333fb1c676b43.png)

右上の終了ボタンをクリックします。

![0dcad23a2030b258bb62570f6ca23ed1](https://i.gyazo.com/0dcad23a2030b258bb62570f6ca23ed1.jpg)

終了をすると obniz が処理待ちに戻ります。