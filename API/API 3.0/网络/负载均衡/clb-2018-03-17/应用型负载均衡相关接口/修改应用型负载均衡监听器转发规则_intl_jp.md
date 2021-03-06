## 1. API説明

APIリクエストドメイン名：clb.tencentcloudapi.com。

ModifyRule APIはアプリケーション型CLBの7層リスナーの転送規則の各属性を変更するために使用され、転送パス、正常性検査属性、転送ポリシーなどを含みます。
このAPIは非同期APIであり、APIの返し動作が完了した後、返されたRequestIDを入力パラメータとする必要があり、DescribeTaskStatus APIを呼び出して今回のタスクが成功したか照合します。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互通信できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例：clb.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/214/30670)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：ModifyRule |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-03-17 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/214/30670#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| LoadBalancerId | はい | String | ロードバランサーインスタンスID |
| ListenerId | はい | String | アプリケーション型CLBリスナーID |
| LocationId | はい | String | 変更する転送規則のID。 |
| Url | いいえ | String | 転送規則の新しい転送パスであり、URLを変更する必要がない場合、このパラメータを修正する必要はありません |
| HealthCheck | いいえ | [HealthCheck](/document/api/214/30694#HealthCheck) | 正常性検査情報 |
| Scheduler | いいえ | String | 規則のリクエスト転送方式 |
| SessionExpireTime | いいえ | Integer | セッション保留時間 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 転送規則の正常性検査パラメータおよび転送ポリシーの変更

#### 入力例

```
https://clb.tencentcloudapi.com/?Action=ModifyRule
&LoadBalancerId=lb-cuxw2rm0
&ListenerId=lbl-4fbxq45k
&LocationId=loc-9dr7bsl3
&Url=/bar&Scheduler=LEAST_CONN
&SessionExpireTime=75
&HealthCheck.HealthSwitch=1
&HealthCheck.IntervalTime=50
&HealthCheck.HealthNum=3
&HealthCheck.UnHealthNum=3
&HealthCheck.HttpCode=7
&HealthCheck.HttpCheckPath=/check
&HealthCheck.HttpCheckDomain=foo.net
&HealthCheck.HttpCheckMethod=GET
&<共通リクエストパラメータ>
```

#####　出力例

```
{
    "Response": {
        "RequestId": "6d846dfd-27f3-4d74-bc00-ec9ae0570cb0"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールはオンライン呼び出し、署名の検証、SDKコード生成と高速検索APIなどの機能を提供し、クラウドAPI使用の難易度を大幅に低減することができるため、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=clb&Version=2018-03-17&Action=ModifyRule)

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

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](/document/api/214/30673#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| FailedOperation | 操作失敗 |
| InternalError | 内部エラー |
| InvalidParameter | パラメータエラー。 |
| InvalidParameterValue | パラメータ値エラー |
| UnauthorizedOperation | 操作が承認されていません |

