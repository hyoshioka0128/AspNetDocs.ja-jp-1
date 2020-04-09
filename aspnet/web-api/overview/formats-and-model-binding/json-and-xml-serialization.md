---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: Web API での json および XML シリアル化ASP.NET - ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x の Web API での JSON および XML フォーマッタASP.NET説明します。
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: e6e02fa1c48e9c5fb8499379508619ddb317ccc9
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675833"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>web API での JSON および XML シリアル化ASP.NET

[マイク・ワッソン](https://github.com/MikeWasson)著

この記事では、Web API の JSON および XML フォーマッタASP.NET説明します。

ASP.NET Web API では、*メディアタイプのフォーマッタ*は次のオブジェクトです。

- HTTP メッセージ本文から CLR オブジェクトを読み取る
- CLR オブジェクトを HTTP メッセージ本文に書き込む

Web API は、JSON と XML の両方にメディアタイプのフォーマッタを提供します。 フレームワークは、既定でこれらのフォーマッタをパイプラインに挿入します。 クライアントは、HTTP 要求の Accept ヘッダーで JSON または XML のいずれかを要求できます。

## <a name="contents"></a>内容

- [JSON メディアタイプフォーマッタ](#json_media_type_formatter)

    - [読み取り専用プロパティ](#json_readonly)
    - [Dates](#json_dates)
    - [インデント](#json_indenting)
    - [キャメルケーシング](#json_camelcasing)
    - [匿名オブジェクトと弱い型指定オブジェクト](#json_anon)
- [XML メディアタイプフォーマッタ](#xml_media_type_formatter)

    - [読み取り専用プロパティ](#xml_readonly)
    - [Dates](#xml_dates)
    - [インデント](#xml_indenting)
    - [型ごとの XML シリアライザーの設定](#xml_pertype)
- [JSON または XML フォーマッタの削除](#removing_the_json_or_xml_formatter)
- [循環オブジェクト参照の処理](#handling_circular_object_references)
- [オブジェクトのシリアル化のテスト](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON メディアタイプフォーマッタ

JSON 形式は **、クラスによって**提供されます。 既定では **、jsonMediaTypeFormatter**は[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)ライブラリを使用してシリアル化を実行します。 Json.NETは、サードパーティのオープンソースプロジェクトです。

必要に応じて、Json.NET**の代**わりに**データコントラクトJsonSerializer**を使用するようにクラスを構成できます。 これを行うには **、プロパティを** **true**に設定します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>JSON シリアル化

このセクションでは、デフォルトの[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)シリアライザーを使用して、JSON フォーマッタの特定の動作について説明します。 これは、Json.NETライブラリの包括的なドキュメントではありません。詳細については、「 Json.NET ドキュメント 」を[参照してください](http://james.newtonking.com/projects/json/help/)。

#### <a name="what-gets-serialized"></a>シリアル化されるもの

既定では、すべてのパブリック プロパティとパブリック フィールドがシリアル化された JSON に含まれます。 プロパティまたはフィールドを省略するには **、JsonIgnore**属性を使用して修飾します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

オプトイン&quot;&quot;アプローチを希望する場合は **、DataContract**属性を使用してクラスを修飾します。 この属性が存在する場合、メンバーが**DataMember**を持っていない限り、メンバーは無視されます。 **また、DataMember**を使用してプライベート メンバーをシリアル化することもできます。

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>読み取り専用プロパティ

読み取り専用プロパティは、既定でシリアル化されます。

<a id="json_dates"></a>
### <a name="dates"></a>日付

デフォルトでは、Json.NETは日付を[ISO 8601](http://www.w3.org/TR/NOTE-datetime)形式で書き込みます。 UTC (協定世界時) の日付は、"Z" 接尾辞を付けて書かれます。 ローカル時間の日付には、タイム ゾーン オフセットが含まれます。 次に例を示します。

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

デフォルトでは、Json.NETはタイムゾーンを保持します。 これをオーバーライドするには、次のプロパティを設定します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

ISO 8601 の代わりに`"\/Date(ticks)\/"`Microsoft JSON[の日付形式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb)( ) を使用する場合は、シリアライザーの設定で**DateFormatHandling**プロパティを設定します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>インデント

インデントされた JSON を書き込むには、[**書式設定**] 設定を **[書式設定]** に設定します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>キャメルケーシング

データ モデルを変更せずにキャメル 大文字と小文字を使用して JSON プロパティ名を書き込むには、シリアライザーで**CamelCasePropertyNamesContractResolver**を設定します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>匿名オブジェクトと弱い型指定オブジェクト

アクション メソッドは、匿名オブジェクトを返して JSON にシリアル化できます。 次に例を示します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

応答メッセージ本文には、次の JSON が含まれます。

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

Web API がクライアントから緩やかに構造化された JSON オブジェクトを受け取る場合は、要求本文を**Newtonsoft.Json.Linq.JObject**型に逆シリアル化できます。

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

ただし、通常は厳密に型指定されたデータ オブジェクトを使用する方が適しています。 その後、データを自分で解析する必要がなくて、モデル検証のメリットを得ることができます。

XML シリアライザーは、匿名型または**JObject**インスタンスをサポートしていません。 JSON データにこれらの機能を使用する場合は、この記事で後述するように、パイプラインから XML フォーマッタを削除する必要があります。

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>XML メディアタイプフォーマッタ

XML 書式設定は **、クラスによって**提供されます。 既定では、**シリアル**化を実行するために**クラスを**使用します。

必要に応じて、データコントラクトシリアライザーの代わりに**XmlSerializer**を使用するように**XmlMediaTypeFormatter** **を**構成できます。 これを行うには、**プロパティ**を**true**に設定します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

**クラス**は **、データ コントラクトシリアライザー**よりも幅の狭い型のセットをサポートしますが、結果の XML をより詳細に制御できます。 既存の XML スキーマと一致させる必要がある場合は **、XmlSerializer**の使用を検討してください。

### <a name="xml-serialization"></a>XML シリアル化

ここでは、既定の**DataContractSerializer**を使用して、XML フォーマッタの特定の動作について説明します。

既定では、次のように動作します。

- すべてのパブリック読み取り/書き込みプロパティおよびフィールドはシリアル化されます。 プロパティまたはフィールドを省略するには、**それを IgnoreDataMember**属性で修飾します。
- プライベート メンバーとプロテクト メンバーはシリアル化されません。
- 読み取り専用プロパティはシリアル化されません。 (ただし、読み取り専用のコレクション プロパティの内容はシリアル化されます。
- クラス名とメンバー名は、クラス宣言に記述されているとおりに XML に書き込まれます。
- 既定の XML 名前空間が使用されます。

シリアル化をより詳細に制御する必要がある場合は **、DataContract**属性を使用してクラスを修飾できます。 この属性が存在する場合、クラスは次のようにシリアル化されます。

- &quot;オプト&quot;インアプローチ: プロパティとフィールドは、既定ではシリアル化されません。 プロパティまたはフィールドをシリアル化するには **、DataMember**属性を使用して修飾します。
- プライベート メンバーまたはプロテクト メンバーをシリアル化するには **、DataMember**属性を使用して修飾します。
- 読み取り専用プロパティはシリアル化されません。
- XML でのクラス名の表示方法を変更するには **、DataContract**属性で*Name*パラメーターを設定します。
- XML でのメンバー名の表示方法を変更するには **、DataMember**属性で*Name*パラメーターを設定します。
- XML 名前空間を変更するには **、DataContract**クラスで*名前空間*パラメーターを設定します。

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>読み取り専用プロパティ

読み取り専用プロパティはシリアル化されません。 読み取り専用プロパティにバッキングプライベート フィールドがある場合は、プライベート フィールドに**DataMember**属性をマークできます。 この方法では、クラスの**DataContract**属性が必要です。

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>日付

日付は、ISO 8601 形式で記述されます。 たとえば、2012-05-23T20:21:37.9116538Z &quot;&quot;。

<a id="xml_indenting"></a>
### <a name="indenting"></a>インデント

インデントされた XML を書き込むには、**インデント**プロパティを**true**に設定します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>型ごとの XML シリアライザーの設定

さまざまな CLR 型に対して異なる XML シリアライザーを設定できます。 たとえば、下位互換性のために**XmlSerializer**を必要とする特定のデータ オブジェクトがあるとします。 このオブジェクトに**対して XmlSerializer**を使用し、他の型に**対して引**き続き使用できます。

特定の型に対して XML シリアライザーを設定するには **、SetSerializer**を呼び出します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

**XmlSerializer または XmlObjectSerializer**から派生する任意のオブジェクト**を**指定できます。

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>JSON または XML フォーマッタの削除

使用しない場合は、フォーマッタのリストから JSON フォーマッタまたは XML フォーマッタを削除できます。 これを行う主な理由は次のとおりです。

- Web API の応答を特定のメディアタイプに制限する。 たとえば、JSON 応答のみをサポートし、XML フォーマッタを削除するとします。
- 既定のフォーマッタをカスタム フォーマッタに置き換えます。 たとえば、JSON フォーマッタを、JSON フォーマッタの独自のカスタム実装に置き換えることができます。

次のコードは、既定のフォーマッタを削除する方法を示しています。 Global.asax で定義されている**\_アプリケーションの開始**メソッドからこれを呼び出します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>循環オブジェクト参照の処理

デフォルトでは、JSON および XML フォーマッタはすべてのオブジェクトを値として書き込みます。 2 つのプロパティが同じオブジェクトを参照している場合、または同じオブジェクトがコレクション内に 2 回出現した場合、フォーマッタはオブジェクトを 2 回シリアル化します。 シリアライザーは、グラフ内のループを検出すると例外をスローするため、オブジェクト グラフにサイクルが含まれている場合、これは特定の問題です。

次のオブジェクト モデルとコントローラを検討してください。

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

このアクションを呼び出すと、フォーマッタは例外をスローし、クライアントに対するステータス コード 500 (内部サーバー エラー) 応答に変換されます。

JSON でオブジェクト参照を保持するには、Global.asax ファイルの**\_アプリケーションの開始**メソッドに次のコードを追加します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

これで、コントローラーアクションは次のような JSON を返します。

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

シリアライザーは、両方のオブジェクト&quot;に&quot;$idプロパティを追加することに注意してください。 また、Employee.Department プロパティがループを作成することを検出し、値をオブジェクト参照&quot;{ $ref&quot;:&quot;1&quot;} に置き換えます。

> [!NOTE]
> オブジェクト参照は、JSON では標準ではありません。 この機能を使用する前に、クライアントが結果を解析できるかどうかを検討してください。 単にグラフからサイクルを削除する方が良いかもしれません。 たとえば、この例では、従業員から部門へのリンクは実際には必要ありません。

XML でオブジェクト参照を保持するには、2 つのオプションがあります。 より簡単なオプションは、モデル`[DataContract(IsReference=true)]`クラスに追加することです。 *IsReference*パラメーターは、オブジェクト参照を有効にします。 **DataContract**はシリアル化のオプトインを行うので、プロパティに**DataMember**属性を追加する必要があることに注意してください。

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

これで、フォーマッタは次のような XML を生成します。

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

モデル クラスの属性を回避する場合は、別のオプションがあります: 新しい型固有**の DataContractSerializer**インスタンスを作成し、コンストラクターで*preserveObjectReferences*を**true**に設定します。 次に、このインスタンスを XML メディア型フォーマッタの型ごとのシリアライザーとして設定します。 次のコードは、これを行う方法を示しています。

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>オブジェクトのシリアル化のテスト

Web API を設計する際に、データ オブジェクトのシリアル化方法をテストすると便利です。 これは、コントローラを作成したり、コントローラアクションを呼び出したりしなくても実行できます。

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
