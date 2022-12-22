# LINE Notify とは

![image](https://i.gyazo.com/078142258b3c0026c184d54eda2ccba9.jpg)

これから、LINE Notify を使うので手元のスマホで LINE アプリがあるか確認しましょう。

## LINE Notify の大まかな仕組み

LINE Notify の大まかな仕組みを把握します。

![image](https://i.gyazo.com/5ee7b4482f1b28caaf860e72744cd2f5.png)

LINE Notify https://notify-bot.line.me/ja/

> Webサービスと連携すると、LINEが提供する公式アカウント"LINE Notify"から通知が届きます。
> 複数のサービスと連携でき、グループでも通知を受信することが可能です。

![image](https://i.gyazo.com/8dddc3621b4a77af65be36d7907cd02a.png)

つまり「LINE Notifyと連携を行うことで、LINEユーザーが簡単にサービスの通知を受信できるようになります」

## IoT における通知

LINE Notify のような IoT における通知の重要性を把握します。

![image](https://i.gyazo.com/9e70b598a6e055b9b1a7ddab800f6f8a.png)

自分の LINE に通知としてメッセージを受け取ることができる仕組みです。

- 自分から見に行かなくてもメッセージで知らせてくれる仕組み
- 複数人に一斉にメッセージを受け取る仕組み
- 何かしらの情報をまとめて知らせてくれる仕組み

といったものを作ることができます。

自分たちが設定した情報だけを手軽に LINE ユーザーに配信できるので、WEB アプリの仕組みと相性がよく「こういう通知内容は実際役に立つだろうか？」といった形で、自分たちの考えた発想を試しやすいです。

また、そういったメッセージを受け付ける部分を LINE に任せることで、LINE アプリの使い慣れた洗練されたレイアウトで、すぐにメッセージを表示できることも良い点です。

もし、このレベルに使いやすい仕組みを自分でイチからつくるとなると、WEB サーバーの知識・HTML/CSS/JavaScript といった WEB 表示の知識・セキュリティへの配慮・多くのユーザーがいる状況などなど整えるべきことが数多くあります。「こういう通知内容は実際役に立つだろうか？」というシンプルな試行錯誤をするまでに、たくさんの時間がかかります。

このあたりを、LINE Nofity および LINE アプリで、すぐに試せるというのは、自分たちの構想を試して良くしていくときには強い味方になります。

## LINE Notify 事例

LINE Notify に関する使いどころ（ユースケース）を個人面・IoT事例面で把握します

- 個人面
  - 自分の興味のありそうなカテゴリのニュースを定期的に通知
  - 家族共有の Google カレンダーが更新されると通知して共有
- IoT事例面
  - 温度・湿度センサーを設置しておき熱中症アラートを出す（冷房を促すこともセットで）
  - CO2 センサーを設置しておき一定量の濃度に到達したら換気を促す
  - 新生児の健康指標事例
    - https://www.1ft-seabass.jp/memo/2019/11/06/unko-button-getting-start/
    - https://www.1ft-seabass.jp/memo/2020/07/13/summary-of-oyako-tech-lt/
  - 事例
    - https://speakerdeck.com/1ftseabass/developers-summit-2021