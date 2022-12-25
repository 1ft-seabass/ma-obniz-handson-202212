# シンプルな HTTP アクセスをしてみよう

obniz を起動するだけで、テストで作ったサーバーにメッセージを送ってみます。

![1ed7bfa0bc832f45f079eeca20177ad4](https://i.gyazo.com/1ed7bfa0bc832f45f079eeca20177ad4.png)

このようにテストサーバーでは、送られたメッセージが表示されます。

## 今回のテストサーバーは obniz.com を許可している

obniz クラウドのようなブラウザからの実行は、開発環境を準備することなくブラウザだけで実行できて使いやすいのですが、クロスドメイン制約（CORS）という制約で、外部へのデータのやりとりに苦労することがあります。

![d1ba3993931343c5c81072a2cb131102](https://i.gyazo.com/d1ba3993931343c5c81072a2cb131102.png)

obniz クラウドのようなブラウザからのアクセスの場合、通常、受け手のサーバー側が未設定でロスドメイン制約の対応をしてないとき（obniz.com ドメインからのアクセスを許可していないとき）はアクセスすることができません。

![f8c74d2285eafd721c119a9e40ffcf31](https://i.gyazo.com/f8c74d2285eafd721c119a9e40ffcf31.png)

今回のテストサーバーは、obniz.com の設定が済んでいます。

[オリジン間リソース共有 (CORS) - HTTP | MDN](https://developer.mozilla.org/ja/docs/Web/HTTP/CORS) をあたりを参考に、サーバー側で以下の設定をしています。

- Access-Control-Allow-Origin
    - `*` で全開放するか、あるいは `http://obniz.com` だけで obniz.com だけ開放
- Access-Control-Request-Method
    - GET,PUT,POST,DELETE
- Access-Control-Allow-Headers
    - Content-Type

もし、みなさんが連携時に Lambda のサーバレスの仕組みや、自作サーバーで行う場合は、このあたりの設定が必要ですので、チーム内で連携する場合は意識しておきましょう。

## 今回のプログラム

ということで、心おきなくデータを送ってみましょう。

以前の内容をすべて選択して消してから、こちらをエディタの内容を上書きします。

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
    <h1>fetch</h1>

    <div id="obniz-debug"></div>

    <script>

      // 今回の obniz を指示するための設定
      const obniz = new Obniz("OBNIZ_ID_HERE");

      // 接続後、メッセージを送る
      obniz.onconnect = async function () {
        obniz.display.clear();
        obniz.display.print("[fetch]");
        
        // 設定
        const config = {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body:JSON.stringify({
              message:"やっほー！ noname です！"
            })
        };
        // テストサーバーにメッセージを送る
        const FETCH_URL = `https://app-1ft-iot-test-server.herokuapp.com/api/test/message`;
        console.log("FETCH_URL");
        console.log(FETCH_URL);
        // 送信
        const response = await fetch(FETCH_URL, config);
        // 受信した JSON データ
        const json = await response.json();
        console.log("OK");
        console.log(json);

      }
      
    </script>
  </body>
</html>
```

## 動かしてみる

こちらを実行してみます。スイッチを押すようなアクションは必要なく起動して obniz がつながった瞬間にテストサーバーへメッセージを一度だけとばします。

![c2725c5398b89d865b845c958bb2aad0](https://i.gyazo.com/c2725c5398b89d865b845c958bb2aad0.png)

起動するとコンソールでは、プログラム内に書かれた console.log のメッセージが出て OK となり、メッセージ送信が成功します。

![1ed7bfa0bc832f45f079eeca20177ad4](https://i.gyazo.com/1ed7bfa0bc832f45f079eeca20177ad4.png)

このようにテストサーバーでは、送られたメッセージが表示されます。

## メッセージを変えてみましょう

```js
        const config = {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body:JSON.stringify({
              message:"やっほー！ noname です！"
            })
        };
```

こちらが、送るデータを定義している部分です。特に body の

```
            body:JSON.stringify({
              message:"やっほー！ noname です！"
            })
```

こちらの `やっほー！ noname です！` が送っているメッセージです。こちらを自分の名前に変えてみて、送るデータを変えてみましょう！

## HTTP POST リクエストは fetch 関数

![80df55739b7fd5866e67160c4ca34fbc](https://i.gyazo.com/80df55739b7fd5866e67160c4ca34fbc.png)

obniz 側からテストサーバーへは POST リクエストをブラウザに標準で搭載されている fetch 関数を使っています。

フェッチ API の詳しい使い方は、以下を参照ください。

- フェッチ API の使用 - Web API | MDN
    - https://developer.mozilla.org/ja/docs/Web/API/Fetch_API/Using_Fetch
