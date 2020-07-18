---
uid: config-builder
title: ASP.NET の構成ビルダー
author: rick-anderson
description: 外部ソースからの web.config 値以外のソースから構成データを取得する方法について説明します。
ms.author: riande
ms.date: 7/17/2020
msc.type: content
ms.openlocfilehash: 1f95efcceb2ecf33fece12174cecf65cd8b27675
ms.sourcegitcommit: 000cbcd1de66fe8a766f203ef2d6f009e4435f53
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86424803"
---
# <a name="configuration-builders-for-aspnet"></a>ASP.NET の構成ビルダー

[Stephen Molloy](https://github.com/StephenMolloy)と[Rick Anderson](https://twitter.com/RickAndMSFT)

構成ビルダーは、ASP.NET アプリが外部ソースから構成値を取得するための最新のアジャイルメカニズムを備えています。

構成ビルダー:

* は .NET Framework 4.7.1 以降で使用できます。
* 構成値を読み取るための柔軟なメカニズムを提供します。
* アプリがコンテナーおよびクラウドに重点を置いた環境に移行する際の基本的なニーズに対処します。
* を使用すると、.NET 構成システムで以前に使用できないソース (Azure Key Vault や環境変数など) から描画することによって、構成データの保護を向上させることができます。

## <a name="keyvalue-configuration-builders"></a>キー/値構成ビルダー

構成ビルダーで処理できる一般的なシナリオは、キー/値パターンに従う構成セクションの基本的なキー/値置換機構を提供することです。 ConfigurationBuilders の .NET Framework 概念は、特定の構成セクションまたはパターンに限定されません。 ただし、(github、NuGet) の構成ビルダーの多くは、 `Microsoft.Configuration.ConfigurationBuilders` キー/値パターン内で動作します。[github](https://github.com/aspnet/MicrosoftConfigurationBuilders) [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)

## <a name="keyvalue-configuration-builders-settings"></a>キー/値構成ビルダーの設定

次の設定は、のすべてのキー/値構成ビルダーに適用され `Microsoft.Configuration.ConfigurationBuilders` ます。

### <a name="mode"></a>モード

構成ビルダーは、キー/値情報の外部ソースを使用して、構成システムの選択したキー/値要素を設定します。 具体的には `<appSettings/>` 、 `<connectionStrings/>` セクションとセクションは、構成ビルダーから特別な処理を受けます。 ビルダーは、次の3つのモードで動作します。

* `Strict`-既定のモード。 このモードでは、構成ビルダーは既知のキー/値中心の構成セクションでのみ動作します。 `Strict`モードは、セクション内の各キーを列挙します。 一致するキーが外部ソースで見つかった場合は、次のようになります。

   * 構成ビルダーは、結果として得られる構成セクションの値を外部ソースの値に置き換えます。
* `Greedy`-このモードは、モードに密接に関連してい `Strict` ます。 元の構成に既に存在するキーに限定されるわけではありません。

  * 構成ビルダーは、外部ソースからのすべてのキーと値のペアを、結果の構成セクションに追加します。

* `Expand`-構成セクションオブジェクトに解析される前に、未加工の XML に対して動作します。 文字列内のトークンの拡張と考えることができます。 パターンに一致する未加工の XML 文字列のすべての部分 `${token}` は、トークンの展開の候補です。 対応する値が外部ソースに見つからない場合、トークンは変更されません。 このモードのビルダーは、 `<appSettings/>` セクションとセクションに限定されていません `<connectionStrings/>` 。

*web.config*の次のマークアップにより、モードでの環境[configbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/)が有効になり `Strict` ます。

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

次のコードは、 `<appSettings/>` `<connectionStrings/>` 前の*web.config*ファイルに示されているとを読み取ります。

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

上記のコードでは、プロパティ値を次のように設定します。

* キーが環境変数に設定されていない場合は、 *web.config*ファイルの値。
* 環境変数の値 (設定されている場合)。

たとえば、に `ServiceID` は次のものが含まれます。

* 環境変数が設定されていない場合は、"web.config からの値を ServiceID" `ServiceID` です。
* 環境変数の値 `ServiceID` (設定されている場合)。

次の図は、 `<appSettings/>` 環境エディターで上記の*web.config*ファイルセットに含まれていたキーと値を示しています。

![環境エディター](config-builder/static/env.png)

メモ: 環境変数の変更を確認するには、Visual Studio を終了して再起動することが必要になる場合があります。

### <a name="prefix-handling"></a>プレフィックスの処理

キープレフィックスを使用すると、次の理由でキーの設定を簡略化できます。

* .NET Framework 構成は複雑で、入れ子になっています。
* 外部キー/値ソースは、一般に基本的なものであり、本質的にフラットです。 たとえば、環境変数は入れ子になっていません。

環境変数を使用してとの両方を構成に挿入するには、次のいずれかの方法を使用し `<appSettings/>` `<connectionStrings/>` ます。

* 既定のモードのと、 `EnvironmentConfigBuilder` `Strict` 構成ファイル内の適切なキー名。 上記のコードとマークアップは、この方法を採用しています。 この方法を使用すると、との両方で同じ名前のキーを持つことはでき**ません** `<appSettings/>` `<connectionStrings/>` 。
* `EnvironmentConfigBuilder`異なるプレフィックスとを使用して、モードで2つのを使用し `Greedy` `stripPrefix` ます。 この方法では、アプリは `<appSettings/>` `<connectionStrings/>` 構成ファイルを更新する必要なく、読み取ることができます。 次の[セクションでは、この](#stripprefix)方法について説明します。
* `EnvironmentConfigBuilder`異なるプレフィックスを持つモードで2つのを使用し `Greedy` ます。 この方法では、キー名がプレフィックスによって異なる必要があるため、キー名を重複させることはできません。  次に例を示します。

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

上記のマークアップでは、同じフラットキー/値ソースを使用して、2つの異なるセクションの構成を設定できます。

次の図は、 `<appSettings/>` `<connectionStrings/>` 環境エディターで上記の*web.config*ファイルセットのキーと値を示しています。

![環境エディター](config-builder/static/prefix.png)

次のコードは、 `<appSettings/>` `<connectionStrings/>` 前の*web.config*ファイルに格納されているとのキー/値を読み取ります。

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

上記のコードでは、プロパティ値を次のように設定します。

* キーが環境変数に設定されていない場合は、 *web.config*ファイルの値。
* 環境変数の値 (設定されている場合)。

たとえば、前の*web.config*ファイル、前の環境エディターのイメージのキー/値、前のコードを使用すると、次の値が設定されます。

|  キー              | 値 |
| ----------------- | ------------ |
|     AppSetting_ServiceID           | Env 変数からの AppSetting_ServiceID|
|    AppSetting_default            | Env からの値の AppSetting_default |
|       ConnStr_default         | Env からの ConnStr_default val|

### <a name="stripprefix"></a>ストライプの Pprefix

`stripPrefix`: boolean、既定値は `false` です。 

上記の XML マークアップは、アプリケーション設定を接続文字列から分離しますが、指定されたプレフィックスを使用するには、 *web.config*ファイル内のすべてのキーが必要です。 たとえば、プレフィックスを `AppSetting` `ServiceID` キー ("AppSetting_ServiceID") に追加する必要があります。 では `stripPrefix` 、プレフィックスは*web.config*ファイルでは使用されません。 プレフィックスは、構成ビルダーのソース (環境など) で必要です。ほとんどの開発者がを使用することを想定 `stripPrefix` しています。

アプリケーションは通常、プレフィックスを削除します。 次の*web.config*により、プレフィックスが除去されます。

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

前の*web.config*ファイルでは、 `default` キーはとの両方 `<appSettings/>` に `<connectionStrings/>` あります。

次の図は、 `<appSettings/>` `<connectionStrings/>` 環境エディターで上記の*web.config*ファイルセットのキーと値を示しています。

![環境エディター](config-builder/static/prefix.png)

次のコードは、 `<appSettings/>` `<connectionStrings/>` 前の*web.config*ファイルに格納されているとのキー/値を読み取ります。

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

上記のコードでは、プロパティ値を次のように設定します。

* キーが環境変数に設定されていない場合は、 *web.config*ファイルの値。
* 環境変数の値 (設定されている場合)。

たとえば、前の*web.config*ファイル、前の環境エディターのイメージのキー/値、前のコードを使用すると、次の値が設定されます。

|  キー              | 値 |
| ----------------- | ------------ |
|     ServiceID           | Env 変数からの AppSetting_ServiceID|
|    default            | Env からの値の AppSetting_default |
|    default         | Env からの ConnStr_default val|

### <a name="tokenpattern"></a>tokenPattern

`tokenPattern`: String、既定値は`@"\$\{(\w+)\}"`

`Expand`ビルダーの動作により、未加工の XML で、のようなトークンが検索され `${token}` ます。 検索は、既定の正規表現を使用して行われ `@"\$\{(\w+)\}"` ます。 と一致する文字のセット `\w` は、XML よりも厳密であり、多くの構成ソースで許可されます。 `tokenPattern` `@"\$\{(\w+)\}"` トークン名に必要な文字数よりも多くの文字がある場合は、を使用します。

`tokenPattern`文字列

* 開発者がトークン照合に使用される regex を変更できるようにします。
* 適切な形式の非危険な regex であることを確認するための検証は行われません。
* キャプチャグループが含まれている必要があります。 Regex 全体がトークン全体と一致している必要があります。 最初のキャプチャは、構成ソース内で検索するトークン名にする必要があります。

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a>Microsoft.Configuration.ConfigurationBuilders の構成ビルダー

### <a name="environmentconfigbuilder"></a>環境 Configbuilder

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

環境[Configbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):

* は、最も単純な構成ビルダーです。
* 環境から値を読み取ります。
* には、追加の構成オプションはありません。
* `name`属性値は任意です。

**注:** Windows コンテナー環境では、実行時に設定される変数は EntryPoint プロセス環境にのみ挿入されます。 サービスとして実行されるアプリまたはエントリポイント以外のプロセスは、コンテナー内のメカニズムによって挿入されない限り、これらの変数を取得しません。 [IIS](https://github.com/Microsoft/iis-docker/pull/41) / [ASP.NET](https://github.com/Microsoft/aspnet-docker)ベースのコンテナーの場合、現在のバージョンの[ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41)では、 *DefaultAppPool*でのみこの処理が処理されます。 その他の Windows ベースのコンテナーバリアントでは、エントリポイント以外のプロセス用に独自の挿入機構を開発することが必要になる場合があります。

### <a name="usersecretsconfigbuilder"></a>UserSecretsConfigBuilder

> [!WARNING]
> パスワード、機密性の高い接続文字列、またはその他の機密データをソースコードに格納しないでください。 運用シークレットは、開発またはテストには使用しないでください。

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

この構成ビルダーには、 [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets)と同様の機能が用意されています。

[UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/)は .NET Framework プロジェクトで使用できますが、シークレットファイルを指定する必要があります。 または、 `UserSecretsId` プロジェクトファイルでプロパティを定義し、読み取り用の正しい場所に生のシークレットファイルを作成することもできます。 外部の依存関係をプロジェクトから除外するために、シークレットファイルは XML 形式になっています。 XML の書式設定は実装の詳細であり、形式に依存することはできません。 .NET Core プロジェクトでファイル*のsecrets.js*を共有する必要がある場合は、 [Simplejsonconfigbuilder](#simplejsonconfigbuilder)の使用を検討してください。 `SimpleJsonConfigBuilder`.Net Core の形式も、変更される可能性のある実装の詳細と見なす必要があります。

構成属性 `UserSecretsConfigBuilder` :

* `userSecretsId`-これは、XML シークレットファイルを識別するために推奨される方法です。 これは、プロジェクトのプロパティを使用してこの識別子を格納する .NET Core に似て `UserSecretsId` います。 文字列は一意である必要があります。 GUID である必要はありません。 この属性を使用すると、は、 `UserSecretsConfigBuilder` `%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml` この識別子に属するシークレットファイルの既知のローカルの場所 () を検索します。
* `userSecretsFile`-シークレットを含むファイルを指定する省略可能な属性です。 この `~` 文字は、アプリケーションルートを参照するために開始時に使用できます。 この属性または `userSecretsId` 属性が必要です。 両方が指定されている場合は、が優先され `userSecretsFile` ます。
* `optional`: ブール値、既定値 `true` -シークレットファイルが見つからない場合、例外が発生しないようにします。 
* `name`属性値は任意です。

シークレットファイルの形式は次のとおりです。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a>AzureKeyVaultConfigBuilder

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/)は、 [Azure Key Vault](/azure/key-vault/key-vault-whatis)に格納されている値を読み取ります。

`vaultName`が必要です (資格情報コンテナーの名前または資格情報コンテナーへの URI)。 他の属性では、接続先のコンテナーを制御できますが、で動作する環境でアプリケーションが実行されていない場合にのみ必要です `Microsoft.Azure.Services.AppAuthentication` 。 Azure サービス認証ライブラリは、可能であれば、実行環境から接続情報を自動的に取得するために使用されます。 接続文字列を指定することで、接続情報を自動的に取得することができます。

* `vaultName`-が指定されていない場合は必須です `uri` 。 キーと値のペアの読み取りに使用する Azure サブスクリプション内のコンテナーの名前を指定します。
* `connectionString`- [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)によって使用可能な接続文字列
* `uri`-指定された値を使用して、他の Key Vault プロバイダーに接続し `uri` ます。 指定されていない場合、Azure ( `vaultName` ) はコンテナープロバイダーです。
* `version`-Azure Key Vault には、シークレットのバージョン管理機能が用意されています。 を指定した場合 `version` 、ビルダーはこのバージョンと一致するシークレットのみを取得します。
* `preloadSecretNames`-既定では、このビルダーは初期化時に key vault 内の**すべて**のキー名を querys ます。 すべてのキー値が読み取られないようにするには、この属性をに設定 `false` します。 このオプションを設定すると `false` 、一度に1つのシークレットが読み取られます。 資格情報コンテナーが "Get" アクセスを許可し、"リスト" アクセスを許可しない場合は、一度に1つのシークレットを読み取ると便利です。 **注:** モードを使用する場合 `Greedy` 、は `preloadSecretNames` `true` (既定値) である必要があります。

### <a name="keyperfileconfigbuilder"></a>KeyPerFileConfigBuilder

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

[Keyperfileconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/)は、ディレクトリのファイルを値のソースとして使用する基本的な構成ビルダーです。 ファイル名はキーで、内容はの値です。 この構成ビルダーは、調整されたコンテナー環境で実行する場合に役立ちます。 Docker の群れや Kubernetes など `secrets` のシステムでは、ファイルごとのキーによって、調整された windows コンテナーが提供されます。

属性の詳細:

* `directoryPath` - 必須。 値を検索するパスを指定します。 Docker for Windows シークレットは、既定では*C:\ProgramData\Docker\secrets*ディレクトリに格納されます。
* `ignorePrefix`-このプレフィックスで始まるファイルは除外されます。 既定値は "ignore" です。
* `keyDelimiter`-既定値は `null` です。 指定した場合、構成ビルダーはディレクトリの複数のレベルを走査し、この区切り記号を使用してキー名を構築します。 この値がの場合 `null` 、構成ビルダーはディレクトリの最上位レベルのみを参照します。
* `optional`-既定値は `false` です。 ソースディレクトリが存在しない場合に、構成ビルダーでエラーを発生させるかどうかを指定します。

### <a name="simplejsonconfigbuilder"></a>SimpleJsonConfigBuilder

> [!WARNING]
> パスワード、機密性の高い接続文字列、またはその他の機密データをソースコードに格納しないでください。 運用シークレットは、開発またはテストには使用しないでください。

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

.NET Core プロジェクトでは、構成に JSON ファイルを頻繁に使用します。 [Simplejsonconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/)ビルダーでは、.NET Core JSON ファイルを .NET Framework で使用できます。 この構成ビルダーは、フラットキー/値ソースから .NET Framework 構成の特定のキー/値領域への基本的なマッピングを提供します。 この構成ビルダーでは、階層構造の構成は提供**されません**。 JSON バッキングファイルは、複雑な階層オブジェクトではなく、辞書に似ています。 複数レベルの階層ファイルを使用できます。 このプロバイダーは `flatten` 、区切り記号としてを使用して、各レベルにプロパティ名を追加することで深さを指定し `:` ます。

属性の詳細:

* `jsonFile` - 必須。 読み取る JSON ファイルを指定します。 この `~` 文字は、アプリのルートを参照するために開始時に使用できます。
* `optional`-Boolean、既定値は `true` です。 JSON ファイルが見つからない場合に例外をスローしないようにします。
* `jsonMode` - `[Flat|Sectional]`. `Flat` は既定値です。 がの場合 `jsonMode` `Flat` 、JSON ファイルは1つのフラットキー/値ソースです。 とは、 `EnvironmentConfigBuilder` `AzureKeyVaultConfigBuilder` 単一のフラットキー/値ソースでもあります。 `SimpleJsonConfigBuilder`がモードで構成されている場合 `Sectional` :

  * JSON ファイルは、概念的に最上位から複数の辞書に分割されています。
  * 各ディクショナリは、接続されている最上位レベルのプロパティ名と一致する構成セクションにのみ適用されます。 次に例を示します。

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="configuration-builders-order"></a>構成ビルダーの順序

[Aspnet/Microsoft configurationbuilders](https://github.com/aspnet/MicrosoftConfigurationBuilders) GitHub リポジトリの「 [Configurationbuilders の実行順序](https://github.com/aspnet/MicrosoftConfigurationBuilders/blob/master/README.md#configurationbuilders-order-of-execution)」を参照してください。

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a>カスタムキー/値構成ビルダーの実装

構成ビルダーがニーズを満たしていない場合は、カスタムのものを作成できます。 `KeyValueConfigBuilder`基底クラスは、置換モードとほとんどのプレフィックスの問題を処理します。 実装するプロジェクトに必要なものは次のとおりです。

* 基本クラスから継承し、とを使用してキーと値のペアの基本的なソースを実装し `GetValue` `GetAllValues` ます。
* [Microsoft.Configuration.ConfigurationBuilders](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/)をプロジェクトに追加します。

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

基本クラスを使用する `KeyValueConfigBuilder` と、キー/値構成ビルダー全体での作業と一貫性のある動作が多くなります。

## <a name="additional-resources"></a>その他のリソース

* [構成ビルダー GitHub リポジトリ](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [.NET を使用した Azure Key Vault に対するサービス間認証](/azure/key-vault/service-to-service-authentication#connection-string-support)
