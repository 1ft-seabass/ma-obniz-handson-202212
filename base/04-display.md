# 内蔵ディスプレイを動かす

![b8e41a4a08cd0844890db32ae7370a83](https://i.gyazo.com/b8e41a4a08cd0844890db32ae7370a83.jpg)

内蔵ディスプレイを動かしてみましょう。

ドキュメントは https://obniz.com/ja/doc/reference/common/display です。

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
        // ディスプレイをクリアする
        obniz.display.clear();
        // ディスプレイに文字を表示
        obniz.display.print("Hello obniz!!!");
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

![4cbb381842c8ce9b8621d0c80931b503](https://i.gyazo.com/4cbb381842c8ce9b8621d0c80931b503.png)

このように緑のバーになり接続されます。

<img width="1228" alt="2022-09-15 14.26.05.jpg (217.0 kB)" src="https://img.esa.io/uploads/production/attachments/3062/2022/09/15/8131/60b69425-dbc2-48e8-b58b-e8122be3ff01.jpg">

このようにディスプレイに文字が表示されます。

## 終了する

![4cbb381842c8ce9b8621d0c80931b503](https://i.gyazo.com/4cbb381842c8ce9b8621d0c80931b503.png)

右上の終了ボタンをクリックします。

![0dcad23a2030b258bb62570f6ca23ed1](https://i.gyazo.com/0dcad23a2030b258bb62570f6ca23ed1.jpg)

終了をすると obniz が処理待ちに戻ります。