# test


```mermaid
left to right direction
hide circle
hide empty members

together {
class 税率マスタ {
    税率
    適用日
    丸めモード: 切り上げ・切り下げ
}
class 振込手数料 {
    700円
    プロ作者だと270？
}
class 掛け率 {
    0.9
}
}

class 価格

rectangle ProductSale {
税込価格 ==> 売上
掛け率 ==> 売上: *
価格 ==> 税額
税率マスタ ==> 税額
価格 ==> 税込価格
税額 => 税込価格

class 販売手数料 #line.dashed

税込価格 ..> 販売手数料
売上 .> 販売手数料
}
rectangle PaymentRequest {
売上 "*" ==o 支払金額: 合計 >
税込価格 "*" ==o 売上金額: 合計 >

税率マスタ ==> 税込み手数料
振込手数料 ==> 税込み手数料
}
rectangle Transfer {
支払金額 ==> 振込金額
税込み手数料 ==> 振込金額: -
}
rectangle RakutasuUploadLogDetail {
振込金額 ==> 振込額2
売上金額 ==> 売上金額2
支払金額 ==> 支払金額2
}
rectangle 売上レポート {
税込価格 ==> 当月販売金額: where 当月 >
売上 ==> お支払い可能金額: where PaymentRequest IS NULL >
支払金額 ===> お支払い予定金額: where status == done >
}
note bottom of お支払い予定金額
Tansferが作られたら
"予定"の方にうつる
end note
```
