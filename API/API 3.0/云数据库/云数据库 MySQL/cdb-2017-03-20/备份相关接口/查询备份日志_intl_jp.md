## 1. API説明

APIリクエストドメイン名： cdb.tencentcloudapi.com 。

このAPI（DescribeBackups）はデータベースインスタンスのバックアップデータを照合するために使用されます。

デフォルトのAPIリクエスト頻度制限：100回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：cdb.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/236/15833)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：DescribeBackups |
| Version | はい | String | 共通パラメータ、該当APIの値：2017/03/20 |
| Region | はい | String | 共通パラメータ。詳細について製品がサポートする[地域リスト](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| InstanceId | はい | String | インスタンスID。フォーマット：cdb-c1nl9rpv。データベースページコンソールページで表示されるインスタンスIDと同じ |
| Offset | いいえ | Integer | オフセット、最小値は0。 |
| Limit | いいえ | Integer | ページングのサイズ。デフォルト値は20、最小値は1、最大値は100。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| TotalCount | Integer | 照合条件を満たすインスタンス総数|
| Items | Array of [BackupInfo](/document/api/236/15878#BackupInfo) | 照合条件を満たすバックアップ情報詳細|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 バックアップログの照合

#### 入力例

```
https://cdb.tencentcloudapi.com/?Action=DescribeBackups
&InstanceId=cdb-c1nl9rpv
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "TotalCount":2,
        "Items":[
            {
                "Status":"SUCCESS",
                "FinishTime":"2017-07-23 12:03:42",
                "Name":"ivansqwutestdr_backup_20170429000134",
                "IntranetUrl":"http://gz.xxxxxxxxxxxxxxxxx",
                "Creator":"SYSTEM",
                "BackupId":12445233,
                "Date":"2017-04-29 00:01:34",
                "InternetUrl":"http://gz.xxxxxxxxxxxxxxxxx",
                "Type":"logical",
                "Size":653226
            },
            {
                "Status":"SUCCESS",
                "FinishTime":"2017-07-23 12:03:42",
                "Name":"ivansqwutestdr_backup_20170430000129",
                "IntranetUrl":"http://gz.xxxxxxxxxxxxxxxxx",
                "Creator":"SYSTEM",
                "BackupId":436184134,
                "Date":"2017-04-30 00:01:29",
                "InternetUrl":"http://gz.xxxxxxxxxxxxxxxxx",
                "Type":"logical",
                "Size":653226
            }
        ]
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeBackups)

### SDK

クラウドAPI 3.0は、API呼び出しを容易にするために複数のプログラミング言語をサポートする、関連開発ツールセット（SDK）を提供します。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. エラーコード

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](/document/api/236/15835#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| CdbError | バックエンドエラーまたはプロセスエラー。 |
| InternalError.DatabaseAccessError | データベース内部エラー。 |
| InternalError.DesError | システム内部エラー。 |
| InvalidParameter | パラメータエラー。 |
| InvalidParameter.InstanceNotFound | インスタンスが存在しません。 |
| OperationDenied.WrongStatus | バックエンドタスクのステータスが不正です。 |

