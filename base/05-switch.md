## 内蔵スイッチを押された状態を取得する

![aecd64d26dfbb7f06f6c1c07ae562f34](https://i.gyazo.com/aecd64d26dfbb7f06f6c1c07ae562f34.jpg)

今度は内蔵スイッチを動かしてみましょう。

ドキュメントは https://obniz.com/ja/doc/reference/common/switch です。

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
      // 接続後、ディスプレイに指示を出す
      obniz.onconnect = async function () {
        console.log("[switch]");
        // ディスプレイ表示
        obniz.display.clear();
        obniz.display.print("[switch]");
        // スイッチの動きを検出
        obniz.switch.onchange = function (state) {
          if (state === "push") {
            // 押されたとき
            console.log("push");
            // ディスプレイ表示
            obniz.display.clear();
            obniz.display.print("push");
          } else if (state === "right") {
            // 右に回したとき
            console.log("right");
            // ディスプレイ表示
            obniz.display.clear();
            obniz.display.print("right");
          } else if (state === "left") {
            // 左に回したとき
            console.log("left");
            // ディスプレイ表示
            obniz.display.clear();
            obniz.display.print("left");
          } else if (state === "none") {
            // 何もしていない時
            console.log("none");
            // ディスプレイ表示
            obniz.display.clear();
            obniz.display.print("none");
          }
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

![f20d84a9eac3401c361feb783b0fc4b4](https://i.gyazo.com/f20d84a9eac3401c361feb783b0fc4b4.jpg)

起動すると [switch] が表示されます。

![70aa123f74c443a34fea69c7e48e3738](https://i.gyazo.com/70aa123f74c443a34fea69c7e48e3738.jpg)

左右に指で動かすと left や right が表示されます。

![643733dfc408f781dc3013ae6839e29e](https://i.gyazo.com/643733dfc408f781dc3013ae6839e29e.jpg)

押すと push が表示されます。

![53161bc03ad8f27ed7ec5a54981ba482](https://i.gyazo.com/53161bc03ad8f27ed7ec5a54981ba482.jpg)

なにもしないと none が表示されます。

## 終了する

![458bed935aa2dbcef07333fb1c676b43](https://i.gyazo.com/458bed935aa2dbcef07333fb1c676b43.png)

右上の終了ボタンをクリックします。

![0dcad23a2030b258bb62570f6ca23ed1](https://i.gyazo.com/0dcad23a2030b258bb62570f6ca23ed1.jpg)

終了をすると obniz が処理待ちに戻ります。