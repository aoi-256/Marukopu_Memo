# I2C通信をやってみよう（開発バージョン)

I2Cの通信方法について説明するよ！

## I2C通信とは

> [!NOTE] 
>
> I2C通信は、データのやり取りに使う線と、タイミングを合わせるために使う線の2本を使って通信する
> 
> 安定性が高く、センサーと400kbps（そこそこはやい）で通信できるため、めちゃくちゃ便利
>
> 慣れてしまえば、かなり簡単に通信ができて便利なので頑張って覚えてみてね

## I2C通信をするためには

> [!TIP]
>　
> I2C通信では次の4つの情報を送っているよ
>
> - データを送る相手（I2Cアドレス)
> - データの送信場所 (レジスタアドレス）
> - 送るデータ　　　 (データ)
> - データの長さ
