## 1. API説明

APIリクエストドメイン名：mongodb.tencentcloudapi.com。

このAPI（UpgradeDBInstance）は、年額/月額のTencentDB for MongoDBインスタンスをアップグレードするために使用されます。メモリ、ストレージ、およびOplogを拡張できます。

デフォルトAPIのリクエスト頻度制限：20回/秒

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：mongodb.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータについては、[共通リクエストパラメータ](/document/api/240/31800)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、該当APIの値：UpgradeDBInstance |
| Version | はい | String | 共通パラメータ、該当APIの値：2018-04-08 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/240/31800#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| InstanceId | はい | String | インスタンスID、フォーマット：cmgo-p8vnipr5。クラウドデータベースコンソールページに表示するインスタンスIDと同じです |
| Memory | はい | Integer | アップグレード後のメモリサイズ、単位：GB |
| Volume | はい | Integer | アップグレード後のディスクサイズ、単位：GB |
| OplogSize | いいえ | Integer | アップグレード後のoplogのサイズ、単位：GB、デフォルトはディスク領域の10％、設定可能な最小値はディスクの10％、最大値はディスクの90％ |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| DealId | String | 注文ID|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 年額/月額のクラウドデータベースインスタンスのアップグレード

ユーザーがAPIを通して年額/月額のクラウドデータベースインスタンスをアップグレード必要があります

#### 入力例

```
https://mongodb.tencentcloudapi.com/?Action=UpgradeDBInstance
&Memory=4
&Volume=250
&InstanceId=cmgo-f555zzzz
&OplogSize=26
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "RequestId": "be8f4a30-ea2e-4623-8b6b-0ccce04cd9f7",
        "DealId": "19297475"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIを使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mongodb&Version=2018-04-08&Action=UpgradeDBInstance)

### SDK

クラウドAPI 3.0は、API呼び出しを容易にするために複数のプログラミング言語をサポートする、関連開発ツールセット（SDK）を提供します。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### CLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. エラーコード

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](/document/api/240/31803#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| InvalidParameter | パラメータエラー |

