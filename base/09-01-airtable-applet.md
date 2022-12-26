# IFTTT Airtable Applet 準備

## Sample Base の確認

![3dfcd97111ba5a5ba892371663299bde](https://i.gyazo.com/3dfcd97111ba5a5ba892371663299bde.png)

事前準備で作成した Sample Base を確認しておきましょう。まだの方は、いまつくりましょう。

## IFTTT の準備

Airtable integrations と Webhook integrations の設定が事前準備できている前提で進めます。

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

![86e10685001f96afa5ed353f2cb1f9c6](https://i.gyazo.com/86e10685001f96afa5ed353f2cb1f9c6.png)

Event Name を airtable_record を入力して、Create trigger をクリックします。

![c5f6b77e7ef1ed99490ab06f2a9d1b17](https://i.gyazo.com/c5f6b77e7ef1ed99490ab06f2a9d1b17.png)

Trigger （きっかけ）のほうに Webhooks が設定できました。

![6a28c85e96d85af378db7d71e9bfe195](https://i.gyazo.com/6a28c85e96d85af378db7d71e9bfe195.png)

Then That の Add ボタンをクリックします。

![ce9340dd02fb0a47b01b9ac851477bde](https://i.gyazo.com/ce9340dd02fb0a47b01b9ac851477bde.png)

Choose a service で Airtable で検索して、Airtable が出てきたらクリックします。

![bcc46f4c19d3130df4e2ca36166b0077](https://i.gyazo.com/bcc46f4c19d3130df4e2ca36166b0077.png)

Create a new record をクリックします。

![d6b975be01acc06d613da90a8b9eea4b](https://i.gyazo.com/d6b975be01acc06d613da90a8b9eea4b.png)

Create a new record のページに移動します。Airtable account が自分の Airtable アカウントか確認します。

![9d23d185fac79bd6bfdb74b898cc0617](https://i.gyazo.com/9d23d185fac79bd6bfdb74b898cc0617.png)

- Which Base ?
    - `Sample`
- Table
    - `Table 1`
- Record content
    - > ::airtable::Name::{{Value1}}

と設定して、設定できたら Create action をクリックします。

Record content の細かな設定方法は、英語ですが <a href="https://support.airtable.com/docs/using-ifttt-to-integrate-airtable-with-other-services#making-an-ifttt-applet-with-airtable-as-the-action" target="_blank">Using IFTTT to Integrate Airtable with Other Services | Airtable Support</a> の Making an IFTTT applet with Airtable as the action が参考になります。

![e8ee56a84f0e4d60378804df889d71fa](https://i.gyazo.com/e8ee56a84f0e4d60378804df889d71fa.png)

Continue ボタンをクリックします。

![9df56b95f086bb355ce8130c3a37c481](https://i.gyazo.com/9df56b95f086bb355ce8130c3a37c481.png)

Finish ボタンをクリックします。

![9853a12f671cf91361c872cf1978214e](https://i.gyazo.com/9853a12f671cf91361c872cf1978214e.png)

Applet が作成できました。