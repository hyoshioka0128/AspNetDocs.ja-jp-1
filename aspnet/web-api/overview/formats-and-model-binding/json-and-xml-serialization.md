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
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="cd41f-103">web API での JSON および XML シリアル化ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cd41f-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="cd41f-104">[マイク・ワッソン](https://github.com/MikeWasson)著</span><span class="sxs-lookup"><span data-stu-id="cd41f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="cd41f-105">この記事では、Web API の JSON および XML フォーマッタASP.NET説明します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="cd41f-106">ASP.NET Web API では、*メディアタイプのフォーマッタ*は次のオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="cd41f-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="cd41f-107">HTTP メッセージ本文から CLR オブジェクトを読み取る</span><span class="sxs-lookup"><span data-stu-id="cd41f-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="cd41f-108">CLR オブジェクトを HTTP メッセージ本文に書き込む</span><span class="sxs-lookup"><span data-stu-id="cd41f-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="cd41f-109">Web API は、JSON と XML の両方にメディアタイプのフォーマッタを提供します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="cd41f-110">フレームワークは、既定でこれらのフォーマッタをパイプラインに挿入します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="cd41f-111">クライアントは、HTTP 要求の Accept ヘッダーで JSON または XML のいずれかを要求できます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="cd41f-112">内容</span><span class="sxs-lookup"><span data-stu-id="cd41f-112">Contents</span></span>

- [<span data-ttu-id="cd41f-113">JSON メディアタイプフォーマッタ</span><span class="sxs-lookup"><span data-stu-id="cd41f-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="cd41f-114">読み取り専用プロパティ</span><span class="sxs-lookup"><span data-stu-id="cd41f-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="cd41f-115">Dates</span><span class="sxs-lookup"><span data-stu-id="cd41f-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="cd41f-116">インデント</span><span class="sxs-lookup"><span data-stu-id="cd41f-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="cd41f-117">キャメルケーシング</span><span class="sxs-lookup"><span data-stu-id="cd41f-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="cd41f-118">匿名オブジェクトと弱い型指定オブジェクト</span><span class="sxs-lookup"><span data-stu-id="cd41f-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="cd41f-119">XML メディアタイプフォーマッタ</span><span class="sxs-lookup"><span data-stu-id="cd41f-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="cd41f-120">読み取り専用プロパティ</span><span class="sxs-lookup"><span data-stu-id="cd41f-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="cd41f-121">Dates</span><span class="sxs-lookup"><span data-stu-id="cd41f-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="cd41f-122">インデント</span><span class="sxs-lookup"><span data-stu-id="cd41f-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="cd41f-123">型ごとの XML シリアライザーの設定</span><span class="sxs-lookup"><span data-stu-id="cd41f-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="cd41f-124">JSON または XML フォーマッタの削除</span><span class="sxs-lookup"><span data-stu-id="cd41f-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="cd41f-125">循環オブジェクト参照の処理</span><span class="sxs-lookup"><span data-stu-id="cd41f-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="cd41f-126">オブジェクトのシリアル化のテスト</span><span class="sxs-lookup"><span data-stu-id="cd41f-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="cd41f-127">JSON メディアタイプフォーマッタ</span><span class="sxs-lookup"><span data-stu-id="cd41f-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="cd41f-128">JSON 形式は **、クラスによって**提供されます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="cd41f-129">既定では **、jsonMediaTypeFormatter**は[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)ライブラリを使用してシリアル化を実行します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="cd41f-130">Json.NETは、サードパーティのオープンソースプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="cd41f-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="cd41f-131">必要に応じて、Json.NET**の代**わりに**データコントラクトJsonSerializer**を使用するようにクラスを構成できます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="cd41f-132">これを行うには **、プロパティを** **true**に設定します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="cd41f-133">JSON シリアル化</span><span class="sxs-lookup"><span data-stu-id="cd41f-133">JSON Serialization</span></span>

<span data-ttu-id="cd41f-134">このセクションでは、デフォルトの[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)シリアライザーを使用して、JSON フォーマッタの特定の動作について説明します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="cd41f-135">これは、Json.NETライブラリの包括的なドキュメントではありません。詳細については、「 Json.NET ドキュメント 」を[参照してください](http://james.newtonking.com/projects/json/help/)。</span><span class="sxs-lookup"><span data-stu-id="cd41f-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="cd41f-136">シリアル化されるもの</span><span class="sxs-lookup"><span data-stu-id="cd41f-136">What Gets Serialized?</span></span>

<span data-ttu-id="cd41f-137">既定では、すべてのパブリック プロパティとパブリック フィールドがシリアル化された JSON に含まれます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="cd41f-138">プロパティまたはフィールドを省略するには **、JsonIgnore**属性を使用して修飾します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="cd41f-139">オプトイン&quot;&quot;アプローチを希望する場合は **、DataContract**属性を使用してクラスを修飾します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="cd41f-140">この属性が存在する場合、メンバーが**DataMember**を持っていない限り、メンバーは無視されます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="cd41f-141">**また、DataMember**を使用してプライベート メンバーをシリアル化することもできます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="cd41f-142">読み取り専用プロパティ</span><span class="sxs-lookup"><span data-stu-id="cd41f-142">Read-Only Properties</span></span>

<span data-ttu-id="cd41f-143">読み取り専用プロパティは、既定でシリアル化されます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="cd41f-144">日付</span><span class="sxs-lookup"><span data-stu-id="cd41f-144">Dates</span></span>

<span data-ttu-id="cd41f-145">デフォルトでは、Json.NETは日付を[ISO 8601](http://www.w3.org/TR/NOTE-datetime)形式で書き込みます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="cd41f-146">UTC (協定世界時) の日付は、"Z" 接尾辞を付けて書かれます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="cd41f-147">ローカル時間の日付には、タイム ゾーン オフセットが含まれます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="cd41f-148">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="cd41f-149">デフォルトでは、Json.NETはタイムゾーンを保持します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="cd41f-150">これをオーバーライドするには、次のプロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="cd41f-151">ISO 8601 の代わりに`"\/Date(ticks)\/"`Microsoft JSON[の日付形式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb)( ) を使用する場合は、シリアライザーの設定で**DateFormatHandling**プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="cd41f-152">インデント</span><span class="sxs-lookup"><span data-stu-id="cd41f-152">Indenting</span></span>

<span data-ttu-id="cd41f-153">インデントされた JSON を書き込むには、[**書式設定**] 設定を **[書式設定]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="cd41f-154">キャメルケーシング</span><span class="sxs-lookup"><span data-stu-id="cd41f-154">Camel Casing</span></span>

<span data-ttu-id="cd41f-155">データ モデルを変更せずにキャメル 大文字と小文字を使用して JSON プロパティ名を書き込むには、シリアライザーで**CamelCasePropertyNamesContractResolver**を設定します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="cd41f-156">匿名オブジェクトと弱い型指定オブジェクト</span><span class="sxs-lookup"><span data-stu-id="cd41f-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="cd41f-157">アクション メソッドは、匿名オブジェクトを返して JSON にシリアル化できます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="cd41f-158">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="cd41f-159">応答メッセージ本文には、次の JSON が含まれます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="cd41f-160">Web API がクライアントから緩やかに構造化された JSON オブジェクトを受け取る場合は、要求本文を**Newtonsoft.Json.Linq.JObject**型に逆シリアル化できます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="cd41f-161">ただし、通常は厳密に型指定されたデータ オブジェクトを使用する方が適しています。</span><span class="sxs-lookup"><span data-stu-id="cd41f-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="cd41f-162">その後、データを自分で解析する必要がなくて、モデル検証のメリットを得ることができます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="cd41f-163">XML シリアライザーは、匿名型または**JObject**インスタンスをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="cd41f-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="cd41f-164">JSON データにこれらの機能を使用する場合は、この記事で後述するように、パイプラインから XML フォーマッタを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd41f-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="cd41f-165">XML メディアタイプフォーマッタ</span><span class="sxs-lookup"><span data-stu-id="cd41f-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="cd41f-166">XML 書式設定は **、クラスによって**提供されます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="cd41f-167">既定では、**シリアル**化を実行するために**クラスを**使用します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="cd41f-168">必要に応じて、データコントラクトシリアライザーの代わりに**XmlSerializer**を使用するように**XmlMediaTypeFormatter** **を**構成できます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="cd41f-169">これを行うには、**プロパティ**を**true**に設定します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="cd41f-170">**クラス**は **、データ コントラクトシリアライザー**よりも幅の狭い型のセットをサポートしますが、結果の XML をより詳細に制御できます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="cd41f-171">既存の XML スキーマと一致させる必要がある場合は **、XmlSerializer**の使用を検討してください。</span><span class="sxs-lookup"><span data-stu-id="cd41f-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="cd41f-172">XML シリアル化</span><span class="sxs-lookup"><span data-stu-id="cd41f-172">XML Serialization</span></span>

<span data-ttu-id="cd41f-173">ここでは、既定の**DataContractSerializer**を使用して、XML フォーマッタの特定の動作について説明します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="cd41f-174">既定では、次のように動作します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="cd41f-175">すべてのパブリック読み取り/書き込みプロパティおよびフィールドはシリアル化されます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="cd41f-176">プロパティまたはフィールドを省略するには、**それを IgnoreDataMember**属性で修飾します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="cd41f-177">プライベート メンバーとプロテクト メンバーはシリアル化されません。</span><span class="sxs-lookup"><span data-stu-id="cd41f-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="cd41f-178">読み取り専用プロパティはシリアル化されません。</span><span class="sxs-lookup"><span data-stu-id="cd41f-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="cd41f-179">(ただし、読み取り専用のコレクション プロパティの内容はシリアル化されます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="cd41f-180">クラス名とメンバー名は、クラス宣言に記述されているとおりに XML に書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="cd41f-181">既定の XML 名前空間が使用されます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-181">A default XML namespace is used.</span></span>

<span data-ttu-id="cd41f-182">シリアル化をより詳細に制御する必要がある場合は **、DataContract**属性を使用してクラスを修飾できます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="cd41f-183">この属性が存在する場合、クラスは次のようにシリアル化されます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="cd41f-184">&quot;オプト&quot;インアプローチ: プロパティとフィールドは、既定ではシリアル化されません。</span><span class="sxs-lookup"><span data-stu-id="cd41f-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="cd41f-185">プロパティまたはフィールドをシリアル化するには **、DataMember**属性を使用して修飾します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="cd41f-186">プライベート メンバーまたはプロテクト メンバーをシリアル化するには **、DataMember**属性を使用して修飾します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="cd41f-187">読み取り専用プロパティはシリアル化されません。</span><span class="sxs-lookup"><span data-stu-id="cd41f-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="cd41f-188">XML でのクラス名の表示方法を変更するには **、DataContract**属性で*Name*パラメーターを設定します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="cd41f-189">XML でのメンバー名の表示方法を変更するには **、DataMember**属性で*Name*パラメーターを設定します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="cd41f-190">XML 名前空間を変更するには **、DataContract**クラスで*名前空間*パラメーターを設定します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="cd41f-191">読み取り専用プロパティ</span><span class="sxs-lookup"><span data-stu-id="cd41f-191">Read-Only Properties</span></span>

<span data-ttu-id="cd41f-192">読み取り専用プロパティはシリアル化されません。</span><span class="sxs-lookup"><span data-stu-id="cd41f-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="cd41f-193">読み取り専用プロパティにバッキングプライベート フィールドがある場合は、プライベート フィールドに**DataMember**属性をマークできます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="cd41f-194">この方法では、クラスの**DataContract**属性が必要です。</span><span class="sxs-lookup"><span data-stu-id="cd41f-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="cd41f-195">日付</span><span class="sxs-lookup"><span data-stu-id="cd41f-195">Dates</span></span>

<span data-ttu-id="cd41f-196">日付は、ISO 8601 形式で記述されます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="cd41f-197">たとえば、2012-05-23T20:21:37.9116538Z &quot;&quot;。</span><span class="sxs-lookup"><span data-stu-id="cd41f-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="cd41f-198">インデント</span><span class="sxs-lookup"><span data-stu-id="cd41f-198">Indenting</span></span>

<span data-ttu-id="cd41f-199">インデントされた XML を書き込むには、**インデント**プロパティを**true**に設定します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="cd41f-200">型ごとの XML シリアライザーの設定</span><span class="sxs-lookup"><span data-stu-id="cd41f-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="cd41f-201">さまざまな CLR 型に対して異なる XML シリアライザーを設定できます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="cd41f-202">たとえば、下位互換性のために**XmlSerializer**を必要とする特定のデータ オブジェクトがあるとします。</span><span class="sxs-lookup"><span data-stu-id="cd41f-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="cd41f-203">このオブジェクトに**対して XmlSerializer**を使用し、他の型に**対して引**き続き使用できます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="cd41f-204">特定の型に対して XML シリアライザーを設定するには **、SetSerializer**を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="cd41f-205">**XmlSerializer または XmlObjectSerializer**から派生する任意のオブジェクト**を**指定できます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="cd41f-206">JSON または XML フォーマッタの削除</span><span class="sxs-lookup"><span data-stu-id="cd41f-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="cd41f-207">使用しない場合は、フォーマッタのリストから JSON フォーマッタまたは XML フォーマッタを削除できます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="cd41f-208">これを行う主な理由は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="cd41f-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="cd41f-209">Web API の応答を特定のメディアタイプに制限する。</span><span class="sxs-lookup"><span data-stu-id="cd41f-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="cd41f-210">たとえば、JSON 応答のみをサポートし、XML フォーマッタを削除するとします。</span><span class="sxs-lookup"><span data-stu-id="cd41f-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="cd41f-211">既定のフォーマッタをカスタム フォーマッタに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="cd41f-212">たとえば、JSON フォーマッタを、JSON フォーマッタの独自のカスタム実装に置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="cd41f-213">次のコードは、既定のフォーマッタを削除する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="cd41f-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="cd41f-214">Global.asax で定義されている**\_アプリケーションの開始**メソッドからこれを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="cd41f-215">循環オブジェクト参照の処理</span><span class="sxs-lookup"><span data-stu-id="cd41f-215">Handling Circular Object References</span></span>

<span data-ttu-id="cd41f-216">デフォルトでは、JSON および XML フォーマッタはすべてのオブジェクトを値として書き込みます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="cd41f-217">2 つのプロパティが同じオブジェクトを参照している場合、または同じオブジェクトがコレクション内に 2 回出現した場合、フォーマッタはオブジェクトを 2 回シリアル化します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="cd41f-218">シリアライザーは、グラフ内のループを検出すると例外をスローするため、オブジェクト グラフにサイクルが含まれている場合、これは特定の問題です。</span><span class="sxs-lookup"><span data-stu-id="cd41f-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="cd41f-219">次のオブジェクト モデルとコントローラを検討してください。</span><span class="sxs-lookup"><span data-stu-id="cd41f-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="cd41f-220">このアクションを呼び出すと、フォーマッタは例外をスローし、クライアントに対するステータス コード 500 (内部サーバー エラー) 応答に変換されます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-220">Invoking this action will cause the formatter to throw an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="cd41f-221">JSON でオブジェクト参照を保持するには、Global.asax ファイルの**\_アプリケーションの開始**メソッドに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="cd41f-222">これで、コントローラーアクションは次のような JSON を返します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="cd41f-223">シリアライザーは、両方のオブジェクト&quot;に&quot;$idプロパティを追加することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="cd41f-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="cd41f-224">また、Employee.Department プロパティがループを作成することを検出し、値をオブジェクト参照&quot;{ $ref&quot;:&quot;1&quot;} に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="cd41f-225">オブジェクト参照は、JSON では標準ではありません。</span><span class="sxs-lookup"><span data-stu-id="cd41f-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="cd41f-226">この機能を使用する前に、クライアントが結果を解析できるかどうかを検討してください。</span><span class="sxs-lookup"><span data-stu-id="cd41f-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="cd41f-227">単にグラフからサイクルを削除する方が良いかもしれません。</span><span class="sxs-lookup"><span data-stu-id="cd41f-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="cd41f-228">たとえば、この例では、従業員から部門へのリンクは実際には必要ありません。</span><span class="sxs-lookup"><span data-stu-id="cd41f-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="cd41f-229">XML でオブジェクト参照を保持するには、2 つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="cd41f-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="cd41f-230">より簡単なオプションは、モデル`[DataContract(IsReference=true)]`クラスに追加することです。</span><span class="sxs-lookup"><span data-stu-id="cd41f-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="cd41f-231">*IsReference*パラメーターは、オブジェクト参照を有効にします。</span><span class="sxs-lookup"><span data-stu-id="cd41f-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="cd41f-232">**DataContract**はシリアル化のオプトインを行うので、プロパティに**DataMember**属性を追加する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="cd41f-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="cd41f-233">これで、フォーマッタは次のような XML を生成します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="cd41f-234">モデル クラスの属性を回避する場合は、別のオプションがあります: 新しい型固有**の DataContractSerializer**インスタンスを作成し、コンストラクターで*preserveObjectReferences*を**true**に設定します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="cd41f-235">次に、このインスタンスを XML メディア型フォーマッタの型ごとのシリアライザーとして設定します。</span><span class="sxs-lookup"><span data-stu-id="cd41f-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="cd41f-236">次のコードは、これを行う方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="cd41f-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="cd41f-237">オブジェクトのシリアル化のテスト</span><span class="sxs-lookup"><span data-stu-id="cd41f-237">Testing Object Serialization</span></span>

<span data-ttu-id="cd41f-238">Web API を設計する際に、データ オブジェクトのシリアル化方法をテストすると便利です。</span><span class="sxs-lookup"><span data-stu-id="cd41f-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="cd41f-239">これは、コントローラを作成したり、コントローラアクションを呼び出したりしなくても実行できます。</span><span class="sxs-lookup"><span data-stu-id="cd41f-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
