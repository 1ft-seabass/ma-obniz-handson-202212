# IFTTT LINE Notify Applet 準備

LINE integrations と Webhook integrations の設定が事前準備できている前提で進めます。

![882b0de8fc7d40a6fd1ec76c3300dbc4](https://i.gyazo.com/882b0de8fc7d40a6fd1ec76c3300dbc4.png)

上部のメニューから Create ボタンをクリックします。2022/12 現在 https://ifttt.com/create でも行けます。

![5609e5ba0b1b051ba8ecbec6e5a7575c](https://i.gyazo.com/5609e5ba0b1b051ba8ecbec6e5a7575c.png)

このような作成画面に移動します。

![334dc3d051205432089bd706c213a94f](https://i.gyazo.com/334dc3d051205432089bd706c213a94f.png)

if This にある Add ボタンをクリックします。

![30bfe0b1ee6d8cbc594393db3603009f](https://i.gyazo.com/30bfe0b1ee6d8cbc594393db3603009f.png)

Choose a service で Webhook で検索して、Webhooks が出てきたらクリックします。

![aed819c39378911162f70ab1c03c2cd4](https://i.gyazo.com/aed819c39378911162f70ab1c03c2cd4.png)

Webhooks ページです。

![5972aef63fbe8eec27ffdb25b2fed81a](https://i.gyazo.com/5972aef63fbe8eec27ffdb25b2fed81a.png)

Receive a web request をクリックします。

![897ac23c7f1ba4ff7193b9ac567c02c3](https://i.gyazo.com/897ac23c7f1ba4ff7193b9ac567c02c3.png)

Event Name を line_notify を入力して、Create trigger をクリックします。

![c5f6b77e7ef1ed99490ab06f2a9d1b17](https://i.gyazo.com/c5f6b77e7ef1ed99490ab06f2a9d1b17.png)

Trigger （きっかけ）のほうに Webhooks が設定できました。

![6a28c85e96d85af378db7d71e9bfe195](https://i.gyazo.com/6a28c85e96d85af378db7d71e9bfe195.png)

Then That の Add ボタンをクリックします。

![911b900372e1cf5c071bba4a06123845](https://i.gyazo.com/911b900372e1cf5c071bba4a06123845.png)

Choose a service で LINE で検索して、LINE が出てきたらクリックします。

![696743bde8565cfcbd32f7c6767743c3](https://i.gyazo.com/696743bde8565cfcbd32f7c6767743c3.png)

LINE の Choose an action では Send message をクリックします。

![8e768ec3e9a7bf3d875ce6d19da491fb](https://i.gyazo.com/8e768ec3e9a7bf3d875ce6d19da491fb.png)

LINE account が自分んだと確認して、Recipient を 1:1 で LINE Notify から通知を受け取るを選択します。

![117a7400f745a63b0c66fe5007d16346](https://i.gyazo.com/117a7400f745a63b0c66fe5007d16346.png)

Message は、いったんこのままで、Photo URL のこのままで Create action ボタンをクリックします。

![07644da20127606b61c3fd369e98c217](https://i.gyazo.com/07644da20127606b61c3fd369e98c217.png)

きっかけで何が動くかの動作として LINE Notify にメッセージが送られる仕組みが出来上がりました。Continue ボタンをクリックします。

![4d45323d5be0cb1689e9e21596c3e454](https://i.gyazo.com/4d45323d5be0cb1689e9e21596c3e454.png)

Finish ボタンをクリックします。

![43968d6906211f43f825be64289e1050](https://i.gyazo.com/43968d6906211f43f825be64289e1050.png)

LINE Notify Applet 作成完了です。

![a8ad4a2f6f9ca4a40307061226da5ce1](https://i.gyazo.com/a8ad4a2f6f9ca4a40307061226da5ce1.png)

上部メニューの My Applets をクリックします。

![00ec87d4956c4ec2e00455b03aa3c1e4](https://i.gyazo.com/00ec87d4956c4ec2e00455b03aa3c1e4.jpg)

My Applets の一覧が表示されて、今回の Applet が表示されています。