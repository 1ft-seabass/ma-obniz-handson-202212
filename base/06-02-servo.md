# サーボを動かしてみよう

スターターキットにあるサーボモータを動かしてみましょう。

ドキュメントは https://obniz.com/ja/sdk/parts/ServoMotor/README.md にあります。

![b52728377b772bd5567d743105564fa1](https://i.gyazo.com/b52728377b772bd5567d743105564fa1.jpg)

サーボモータと部品袋を取り出します。部品袋はまだ開けなくて OK です。

![5a12bec99a3074eebbeebd2cdabba75e](https://i.gyazo.com/5a12bec99a3074eebbeebd2cdabba75e.jpg)

この白い部品とサーボモータをくっつけます。

![4fb0e0694e7f4b39e390d0b9e16efc4b](https://i.gyazo.com/4fb0e0694e7f4b39e390d0b9e16efc4b.jpg)

この白い部品のギザギザの凹み部分とサーボモータの上部の白いギザギザの突起部分をはめ込みます。

![153cc2bac52c5bc1ff5f5dfdf874dce4](https://i.gyazo.com/153cc2bac52c5bc1ff5f5dfdf874dce4.jpg)

指ではめ込みました。

![](https://obniz.com/ja/sdk/parts/ServoMotor/servocable.jpg)

https://obniz.com/ja/sdk/parts/ServoMotor/README.md を参考に、茶色の GND ケーブルに注目します。

![a0a3cd236403c6fa277ae1eabb7dedd9](https://i.gyazo.com/a0a3cd236403c6fa277ae1eabb7dedd9.jpg)

obniz の 0 番ピン穴に茶色のケーブルのピンが合う形でつなげます。

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
      // 接続後、サーボに指示を出す
      obniz.onconnect = async function () {
        obniz.display.clear();
        obniz.display.print("[servo]");
        // サーボの呼び出し
        const servo = obniz.wired("ServoMotor", {gnd:0,vcc:1,signal:2});
        // 90 度
        servo.angle(90);
        // 3秒待つ
        await obniz.wait(3000);
        // 0 度
        servo.angle(0);
        // 3秒待つ
        await obniz.wait(3000);
        // 180 度
        servo.angle(180);
        // 3秒待つ
        await obniz.wait(3000);
        // 0 度
        servo.angle(0);
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

## 終了する

![458bed935aa2dbcef07333fb1c676b43](https://i.gyazo.com/458bed935aa2dbcef07333fb1c676b43.png)

右上の終了ボタンをクリックします。

![0dcad23a2030b258bb62570f6ca23ed1](https://i.gyazo.com/0dcad23a2030b258bb62570f6ca23ed1.jpg)

終了をすると obniz が処理待ちに戻ります。

90 度 → 0 度 → 180 度 → 0 度 とサーボモータが動きます。