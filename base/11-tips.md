## AWS Lambda + obniz 連携

AWS Lambda + obniz 連携は公式ドキュメントがあります。

- AWS Lambda: 1関数で1台のobnizを管理する - obniz Docs
    - https://obniz.com/ja/doc/guides/production/aws-lambda-single
- AWS LambdaとAPI Gatewayを使う - obniz Docs
    - https://obniz.com/ja/doc/guides/nodejs/aws-lambda

注意点としては、ブラウザの JavaScript でなく Node.js で組むことになるので、かなり似ているコードで書けますが、違いはあるのでそのあたりを気をつけながら実装していくことになります。

## obniz とビーコンの連携

私の方が、いろいろ調べてみました。ぜひご参考ください。

- MAMORIO を BLE ビーコンとして obniz の BLE で検知するメモ – 1ft-seabass.jp.MEMO
    - https://www.1ft-seabass.jp/memo/2022/12/20/obniz-check-mamorio-ble-beacon/
- obniz で BLE ビーコンを試すとき MAMORIO RE が使いやすかったメモ – 1ft-seabass.jp.MEMO
    - https://www.1ft-seabass.jp/memo/2022/12/23/obniz-mamorio-re-very-nice-approach/

## ハッカソン前に一通り試そう

![6fab899c0415c0a1bcb2444bd262664e](https://i.gyazo.com/6fab899c0415c0a1bcb2444bd262664e.png)

obniz + MESH 含めて、チーム内の作りたいものに合わせて実装していきますね。

その時に大切なのは「ハッカソン前に一通り試すこと」です。

ハッカソン中に試行錯誤をしながら作り切るのは至難の業です。ですので、事前に Slack でのテクニカルメンターへの質問も駆使しつつ事前に自分たちのやりたい仕組みを試しておきましょう。理想を言えば、一つ一つの検証だけでなくだいたいの仕組みをつなげておくことです。

もちろん obniz + MESH まわりは、私の方が全力でサポートします！がんばりましょー。

## MESH や obniz は自分のモノとわかるようにラベルを貼りましょう

![894de1e36ec3b519d77a3ad986339cc7](https://i.gyazo.com/894de1e36ec3b519d77a3ad986339cc7.jpg)

とくに MESH は、同じ会場でみなさんが同時に使うケースがあって、他チームと混ざっちゃう可能性があります。そうなると、タイムロスにつながりかねないので、このようにチーム名でも担当する人の名前でもラベルを貼るのがおススメです。

私は、よく白いマスキングテープのようなものにボールペンで書いて貼ってます。あとでも剥がしやすいです。

obniz は電源をつければ ID が書いてあるので、結構分かりますが、それでも全く同じ機材なだけに混乱しやすいので、ラベルを付けるのもいいでしょう。

