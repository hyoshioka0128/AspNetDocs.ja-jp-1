---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
title: ASP.NET AJAX Web サービスについて |Microsoft Docs
author: scottcate
description: Web サービスは .NET framework の不可欠な部分であり、分散システム間でデータを交換するためのクロスプラットフォームソリューションを提供します。 ただし、Web...
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 3332d6e7-e2e1-4144-b805-e71d51e7e415
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
msc.type: authoredcontent
ms.openlocfilehash: eac3d53fd871d0cb5a2870488ce752c057cc5b1a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "86162846"
---
# <a name="understanding-aspnet-ajax-web-services"></a>ASP.NET AJAX Web サービスについて理解する

[Scott Cate](https://github.com/scottcate)

[PDF のダウンロード](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial05_Web_Services_with_MS_Ajax_cs.pdf)

> Web サービスは .NET framework の不可欠な部分であり、分散システム間でデータを交換するためのクロスプラットフォームソリューションを提供します。 通常、Web サービスは、さまざまなオペレーティングシステム、オブジェクトモデル、およびプログラミング言語がデータを送受信できるようにするために使用されますが、ASP.NET AJAX ページにデータを動的に挿入したり、ページからバックエンドシステムにデータを送信したりするために使用することもできます。 これらはすべて、ポストバック操作を行わなくても実行できます。

## <a name="calling-web-services-with-aspnet-ajax"></a>ASP.NET AJAX を使用した Web サービスの呼び出し

Dan Wahlin

Web サービスは .NET framework の不可欠な部分であり、分散システム間でデータを交換するためのクロスプラットフォームソリューションを提供します。 通常、Web サービスは、さまざまなオペレーティングシステム、オブジェクトモデル、およびプログラミング言語がデータを送受信できるようにするために使用されますが、ASP.NET AJAX ページにデータを動的に挿入したり、ページからバックエンドシステムにデータを送信したりするために使用することもできます。 これらはすべて、ポストバック操作を行わなくても実行できます。

ASP.NET AJAX UpdatePanel コントロールでは、任意の ASP.NET ページを簡単に有効にすることができますが、UpdatePanel を使用せずにサーバー上のデータに動的にアクセスすることが必要になる場合があります。 この記事では、ASP.NET AJAX ページ内で Web サービスを作成および使用することによってこれを実現する方法について説明します。

この記事では、ASP.NET AJAX のコア拡張機能と、AutoCompleteExtender と呼ばれる ASP.NET AJAX Toolkit の Web サービスが有効になっているコントロールで使用できる機能に焦点を当てます。 ここでは、AJAX 対応 Web サービスの定義、クライアントプロキシの作成、および JavaScript を使用した Web サービスの呼び出しについて説明します。 また、ASP.NET page メソッドに対して Web サービス呼び出しを直接行う方法についても説明します。

## <a name="web-services-configuration"></a>Web サービスの構成

Visual Studio 2008 を使用して新しい Web サイトプロジェクトを作成すると、web.config ファイルには、以前のバージョンの Visual Studio のユーザーにとって馴染みのない多くの新しい追加機能が追加されます。 これらの変更の一部では、ページで使用できるように、"asp" プレフィックスが ASP.NET AJAX コントロールにマップされ、他のユーザーが必要な HttpHandlers と HttpModules を定義します。 リスト1は、 `<httpHandlers>` Web サービスの呼び出しに影響を与える web.config の要素に対して行われた変更を示します。 .Asmx 呼び出しを処理するために使用される既定の HttpHandler は削除され、System.Web.Extensions.dll アセンブリにある ScriptHandlerFactory クラスに置き換えられます。 System.Web.Extensions.dll には、ASP.NET AJAX によって使用される主要な機能がすべて含まれています。

**リスト 1.ASP.NET AJAX Web サービスハンドラーの構成**

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample1.xml)]

この HttpHandler は、JavaScript Web サービスプロキシを使用して、ASP.NET AJAX ページから .NET Web サービスに JavaScript Object Notation (JSON) 呼び出しを行うことができるようにするために行われています。 ASP.NET AJAX は、通常は Web サービスに関連付けられている標準の簡易オブジェクトアクセスプロトコル (SOAP) 呼び出しとは対照的に、JSON メッセージを Web サービスに送信します。 これにより、要求メッセージと応答メッセージ全体が小さくなります。 また、ASP.NET AJAX JavaScript ライブラリが JSON オブジェクトを使用するように最適化されているため、クライアント側でのデータの処理効率が向上します。 リスト2とリスト3は、JSON 形式にシリアル化された Web サービス要求メッセージと応答メッセージの例を示しています。 リスト2に示されている要求メッセージは、"ベルギー" という値を持つ country パラメーターを渡します。リスト3の応答メッセージは、Customer オブジェクトとその関連プロパティの配列を渡します。

**リスト 2.JSON にシリアル化された Web サービス要求メッセージ**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample2.json)]

> *>[!NOTE]操作名は、web サービスへの URL の一部として定義されます。さらに、要求メッセージは JSON 経由で送信されることはありません。Web サービスは、UseHttpGet パラメーターを true に設定して ScriptMethod 属性を利用できます。これにより、クエリ文字列パラメーターを使用してパラメーターが渡されます。*

**リスト 3.JSON にシリアル化された Web サービス応答メッセージ**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample3.json)]

次のセクションでは、JSON 要求メッセージを処理し、単純型と複合型の両方に対応できる Web サービスを作成する方法について説明します。

## <a name="creating-ajax-enabled-web-services"></a>AJAX 対応 Web サービスの作成

ASP.NET AJAX フレームワークには、Web サービスを呼び出すためのさまざまな方法が用意されています。 AutoCompleteExtender コントロール (ASP.NET AJAX Toolkit で利用可能) または JavaScript を使用できます。 ただし、サービスを呼び出す前に、クライアントスクリプトコードから呼び出すことができるように、サービスを AJAX によって有効にする必要があります。

ASP.NET ウェブサービスを初めて使用する場合でも、サービスの作成と AJAX 有効化を簡単に行うことができます。 .NET framework では、2002の初期リリース以降の ASP.NET Web サービスの作成がサポートされています。また、ASP.NET AJAX 拡張機能には、.NET framework の既定の機能セットを基盤とする追加の AJAX 機能が用意されています。 Visual Studio .NET 2008 Beta 2 には、.asmx Web サービスファイルを作成するためのサポートが組み込まれています。また、関連するコードは、System.web. WebService クラスから自動的に派生します。 クラスにメソッドを追加するときに、Web サービスコンシューマーによって呼び出されるようにするために、WebMethod 属性を適用する必要があります。

リスト4は、GetCustomersByCountry () という名前のメソッドに WebMethod 属性を適用する例を示しています。

**リスト 4.Web サービスでの WebMethod 属性の使用**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample4.cs)]

GetCustomersByCountry () メソッドは、country パラメーターを受け取り、Customer オブジェクト配列を返します。 メソッドに渡される country 値はビジネス層クラスに転送され、さらにデータレイヤークラスを呼び出してデータベースからデータを取得し、顧客オブジェクトのプロパティにデータを入力して、配列を返します。

## <a name="using-the-scriptservice-attribute"></a>ScriptService 属性の使用

WebMethod 属性を追加すると、標準の SOAP メッセージを Web サービスに送信するクライアントによって GetCustomersByCountry () メソッドを呼び出すことができますが、JSON 呼び出しを ASP.NET AJAX アプリケーションからすぐに実行することはできません。 JSON 呼び出しを実行できるようにするには、ASP.NET AJAX 拡張機能の `ScriptService` 属性を Web サービスクラスに適用する必要があります。 これにより、Web サービスは JSON を使用して書式設定された応答メッセージを送信できるようになり、JSON メッセージを送信することによって、クライアント側スクリプトがサービスを呼び出すことができます。

リスト5は、"顧客 Sservice" という名前の Web サービスクラスに ScriptService 属性を適用する例を示しています。

**リスト5。ScriptService 属性を使用して Web サービスを AJAX 対応にする**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample5.cs)]

ScriptService 属性は、AJAX スクリプトコードから呼び出すことができることを示すマーカーとして機能します。 実際には、バックグラウンドで発生する JSON のシリアル化または逆シリアル化のタスクを処理しません。 ScriptHandlerFactory (web.config で構成) およびその他の関連クラスは、JSON の処理の大部分を実行します。

## <a name="using-the-scriptmethod-attribute"></a>ScriptMethod 属性の使用

ScriptService 属性は、ASP.NET AJAX ページで使用されるために .NET Web サービスで定義する必要がある唯一の ASP.NET AJAX 属性です。 ただし、ScriptMethod という別の属性をサービスの Web メソッドに直接適用することもできます。 ScriptMethod `UseHttpGet` は、、、およびを含む3つのプロパティを定義し `ResponseFormat` `XmlSerializeString` ます。 これらのプロパティの値を変更することは、web メソッドで受け入れられる要求の種類を GET に変更する必要がある場合、Web メソッドがオブジェクトまたはオブジェクトの形式で未加工の XML データを返す必要がある場合、 `XmlDocument` `XmlElement` またはサービスから返されるデータを JSON ではなく XML として常にシリアル化する必要がある場合に役立ちます

UseHttpGet プロパティは、Web メソッドが POST 要求ではなく GET 要求を受け入れる必要がある場合に使用できます。 要求は、Web メソッドの入力パラメーターが QueryString パラメーターに変換された URL を使用して送信されます。 UseHttpGet プロパティの既定値は false であり、 `true` 操作が安全であることがわかっている場合と、機密データが Web サービスに渡されない場合にのみ設定する必要があります。 リスト6は、ScriptMethod 属性を UseHttpGet プロパティと共に使用する例を示しています。

**リスト6。ScriptMethod 属性を UseHttpGet プロパティと共に使用します。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample6.cs)]

リスト6に示されている Httpgeare o Web メソッドが呼び出されたときに送信されるヘッダーの例を次に示します。

`GET /CustomerViewer/DemoService.asmx/HttpGetEcho?input=%22Input Value%22 HTTP/1.1`

XML 応答が JSON ではなくサービスから返される必要がある場合は、Web メソッドで HTTP GET 要求を受け入れることができるだけでなく、ScriptMethod 属性を使用することもできます。 たとえば、Web サービスは、リモートサイトから RSS フィードを取得し、それを XmlDocument オブジェクトまたは XmlElement オブジェクトとして返すことができます。 その後、XML データの処理をクライアントで行うことができます。

リスト7は、ResponseFormat プロパティを使用して、Web メソッドから XML データを返すように指定する例を示しています。

**リスト7。ScriptMethod 属性を ResponseFormat プロパティと共に使用します。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample7.cs)]

ResponseFormat プロパティは、XmlSerializeString プロパティと共に使用することもできます。 XmlSerializeString プロパティの既定値は false です。これは、 `ResponseFormat` プロパティがに設定されている場合に、Web メソッドから返される文字列を除くすべての戻り値の型が XML としてシリアル化されることを意味し `ResponseFormat.Xml` ます。 `XmlSerializeString`がに設定されている場合 `true` 、Web メソッドから返されるすべての型は、文字列型を含む XML としてシリアル化されます。 ResponseFormat プロパティに値がある場合、 `ResponseFormat.Json` XmlSerializeString プロパティは無視されます。

リスト8は、XmlSerializeString プロパティを使用して文字列を強制的に XML としてシリアル化する例を示しています。

**リスト8。XmlSerializeString プロパティでの ScriptMethod 属性の使用**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample8.cs)]

リスト8に示されている GetXmlString Web メソッドの呼び出しから返される値を次に示します。

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample9.cs)]

既定の JSON 形式では、要求メッセージと応答メッセージの全体的なサイズを最小限に抑えることができ、クロスブラウザー方式で ASP.NET AJAX クライアントによって使用されるようになっていますが、Internet Explorer 5 などのクライアントアプリケーションが Web メソッドから XML データを返すことを期待する場合は、ResponseFormat と XmlSerializeString プロパティを使用できます。

## <a name="working-with-complex-types"></a>複合型の使用

リスト5は、Web サービスから Customer という名前の複合型を返す例を示しています。 Customer クラスは、FirstName や LastName などのプロパティとして、さまざまな単純型を内部的に定義します。 AJAX 対応の Web メソッドで入力パラメーターまたは戻り値の型として使用される複合型は、クライアント側に送信される前に自動的に JSON にシリアル化されます。 ただし、入れ子になった複合型 (別の型の内部で定義されている型) は、既定では、クライアントに対してスタンドアロンオブジェクトとして使用できません。

Web サービスによって使用される入れ子になった複合型をクライアントページでも使用する必要がある場合は、ASP.NET AJAX の種類の属性を Web サービスに追加できます。 たとえば、リスト9に示されている customer Details クラスには、入れ子に***なった複合型を表す***Address プロパティと性別プロパティが含まれています。

**リスト9。ここに示す顧客詳細クラスには、2つの入れ子になった複合型が含まれています。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample10.cs)]

リスト9に示されている [customer Details] クラスに定義されている Address および性別オブジェクトは、入れ子になった型 (Address はクラス、性別は列挙型) であるため、クライアント側では自動的に使用できません。 Web サービス内で使用される入れ子になった型をクライアント側で使用できるようにする必要がある場合は、前述のように、公開されている型の属性を使用できます (一覧10を参照)。 この属性は、サービスから別の入れ子になった複合型が返される場合に、複数回追加できます。 これは、Web サービスクラスまたは特定の Web メソッドに直接適用できます。

**リスト10。クライアントで使用できるようにする必要がある入れ子にされた型を定義するには、公開されたサービス属性を使用します。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample11.cs)]

`GenerateScriptType`属性を Web サービスに適用することで、Address 型と性別型が自動的にクライアント側の ASP.NET AJAX JavaScript コードで使用できるようになります。 自動的に生成され、Web サービスに公開されている型の属性を追加することによってクライアントに送信される JavaScript の例については、一覧11を参照してください。 入れ子になった複合型の使用方法については、この記事の後半で説明します。

**リスト11。入れ子になった複合型は、ASP.NET AJAX ページで使用できます。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample12.cs)]

ここでは、Web サービスを作成し、ASP.NET AJAX ページからアクセスできるようにする方法を説明しました。次は、データを取得または Web サービスに送信できるように、JavaScript プロキシを作成して使用する方法について説明します。

## <a name="creating-javascript-proxies"></a>JavaScript プロキシの作成

標準 Web サービス (.NET またはその他のプラットフォーム) を呼び出すには、通常、SOAP 要求メッセージと応答メッセージを送信する複雑さからのものであることを示すプロキシオブジェクトを作成する必要があります。 ASP.NET AJAX Web サービス呼び出しを使用すると、JavaScript プロキシを作成して、JSON メッセージのシリアル化と逆シリアル化を気にせずに簡単にサービスを呼び出すことができます。 JavaScript プロキシは、ASP.NET AJAX ScriptManager コントロールを使用して自動的に生成できます。

Web サービスを呼び出すことができる JavaScript プロキシの作成は、ScriptManager サービスプロパティを使用して行います。 このプロパティを使用すると、ASP.NET AJAX ページが非同期に呼び出して、ポストバック操作を必要とせずにデータを送受信できる1つ以上のサービスを定義できます。 サービスを定義するには、ASP.NET AJAX `ServiceReference` コントロールを使用し、Web サービスの URL をコントロールのプロパティに割り当て `Path` ます。 リスト12は、"顧客" という名前のサービスを参照する例を示しています。

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample13.aspx)]

**リスト12。ASP.NET AJAX ページで使用される Web サービスを定義します。**

ScriptManager コントロールを介して顧客 Sservice .asmx に参照を追加すると、JavaScript プロキシが動的に生成され、ページによって参照されます。 プロキシは、スクリプトタグを使用して埋め込まれ、 &lt; &gt; 顧客のサービス .asmx ファイルを呼び出し、その末尾に/js を追加することによって動的に読み込まれます。 次の例は、web.config でデバッグが無効になっている場合に、JavaScript プロキシがページに埋め込まれる方法を示しています。

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample14.html)]

> *>[!NOTE]生成された実際の JavaScript プロキシコードを表示するには、必要な .Net Web サービスの URL を Internet Explorer の [アドレス] ボックスに入力し、その末尾に js を追加します。*

デバッグが有効になっている場合 web.config JavaScript プロキシのデバッグバージョンは、次のようにページに埋め込まれます。

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample15.html)]

ScriptManager によって作成された JavaScript プロキシは、 &lt; スクリプトタグの src 属性を使用して参照するのではなく、ページに直接埋め込むこともでき &gt; ます。 これを行うには、ServiceReference コントロールの InlineScript プロパティを true (既定値は false) に設定します。 これは、プロキシが複数のページで共有されておらず、サーバーに対して行われるネットワーク呼び出しの回数を減らす必要がある場合に便利です。 InlineScript が true に設定されている場合、プロキシスクリプトはブラウザーによってキャッシュされないため、ASP.NET AJAX アプリケーションの複数のページでプロキシが使用されている場合は、既定値の false を使用することをお勧めします。 InlineScript プロパティの使用例を次に示します。

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample16.aspx)]

## <a name="using-javascript-proxies"></a>JavaScript プロキシの使用

ScriptManager コントロールを使用して ASP.NET AJAX ページによって Web サービスが参照されると、Web サービスに対して呼び出しを行うことができ、返されたデータはコールバック関数を使用して処理できます。 Web サービスは、名前空間 (存在する場合)、クラス名、および Web メソッド名を参照することによって呼び出されます。 Web サービスに渡されるすべてのパラメーターは、返されたデータを処理するコールバック関数と共に定義できます。

JavaScript プロキシを使用して GetCustomersByCountry () という名前の Web メソッドを呼び出す例については、一覧13を参照してください。 GetCustomersByCountry () 関数は、エンドユーザーがページのボタンをクリックしたときに呼び出されます。

**リスト13。JavaScript プロキシを使用して Web サービスを呼び出す。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample17.js)]

この呼び出しは、サービスで定義されている InterfaceTraining 名前空間、顧客 Sservice クラス、および GetCustomersByCountry Web メソッドを参照します。 このメソッドは、テキストボックスから取得された国の値に加え、非同期 Web サービス呼び出しが返されたときに呼び出される必要がある OnWSRequestComplete という名前のコールバック関数を渡します。 OnWSRequestComplete は、サービスから返された顧客オブジェクトの配列を処理し、ページに表示されるテーブルに変換します。 呼び出しから生成された出力を図1に示します。

[![Web サービスに対して非同期 AJAX 呼び出しを行うことによって取得されるバインディングデータ。](understanding-asp-net-ajax-web-services/_static/image2.png)](understanding-asp-net-ajax-web-services/_static/image1.png)

**図 1**: Web サービスに対して非同期 AJAX 呼び出しを行うことによって取得されるバインディングデータ。  ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-web-services/_static/image3.png)される)

また、JavaScript プロキシでは、Web メソッドを呼び出す必要があるが、プロキシが応答を待たない場合に、Web サービスに対して一方向の呼び出しを行うこともできます。 たとえば、Web サービスを呼び出して、サービスからの戻り値を待機するのではなく、作業フローなどのプロセスを開始することができます。 一方向の呼び出しをサービスに対して行う必要がある場合、リスト13に示されているコールバック関数は単に省略できます。 コールバック関数が定義されていないため、プロキシオブジェクトは、Web サービスがデータを返すまで待機しません。

## <a name="handling-errors"></a>エラーの処理

Web サービスへの非同期コールバックでは、ネットワークがダウンしている、Web サービスが使用できない、または例外が返されているなど、さまざまな種類のエラーが発生する可能性があります。 しかし、ScriptManager によって生成された JavaScript プロキシオブジェクトでは、前に示した成功コールバックに加えて、エラーやエラーを処理するために複数のコールバックを定義することができます。 エラーコールバック関数は、リスト14に示されているように、Web メソッドの呼び出しで標準のコールバック関数の直後に定義できます。

**リスト14。エラーコールバック関数を定義し、エラーを表示しています。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample18.js)]

Web サービスが呼び出されたときに発生したエラーが発生すると、エラーを表すオブジェクトをパラメーターとして受け取る OnWSRequestFailed () コールバック関数が呼び出されます。 Error オブジェクトは、エラーの原因、および呼び出しがタイムアウトしたかどうかを判断するために、いくつかの異なる関数を公開します。一覧14は、さまざまなエラー関数の使用例を示しています。図2は、関数によって生成される出力の例を示しています。

[![ASP.NET AJAX エラー関数を呼び出すことによって生成される出力。](understanding-asp-net-ajax-web-services/_static/image5.png)](understanding-asp-net-ajax-web-services/_static/image4.png)

**図 2**: ASP.NET AJAX エラー関数を呼び出すことによって生成される出力。  ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-web-services/_static/image6.png)される)

## <a name="handling-xml-data-returned-from-a-web-service"></a>Web サービスから返される XML データの処理

前に、ScriptMethod 属性と ResponseFormat プロパティを使用して、Web メソッドが生の XML データを返す方法について説明しました。 ResponseFormat が ResponseFormat.Xml に設定されている場合、Web サービスから返されたデータは JSON ではなく XML としてシリアル化されます。 これは、JavaScript または XSLT を使用して処理するために、XML データをクライアントに直接渡す必要がある場合に便利です。 現在のところ、Internet Explorer 5 以降では、MSXML の組み込みサポートにより、XML データの解析とフィルター処理に最適なクライアント側オブジェクトモデルが提供されています。

Web サービスから XML データを取得することは、他のデータ型を取得することと同じです。 まず、JavaScript プロキシを呼び出して適切な関数を呼び出し、コールバック関数を定義します。 呼び出しが返されたら、コールバック関数でデータを処理できます。

リスト15は、XmlElement オブジェクトを返す GetRssFeed () という名前の Web メソッドを呼び出す例を示しています。 GetRssFeed () は、取得する RSS フィードの URL を表す1つのパラメーターを受け取ります。

**リスト15。Web サービスから返される XML データを操作する。**

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample19.html)]

この例では、RSS フィードに URL を渡し、OnWSRequestComplete () 関数で返された XML データを処理します。 OnWSRequestComplete () は、最初にブラウザーが Internet Explorer であるかどうかを確認し、MSXML パーサーが使用可能かどうかを確認します。 の場合、XPath ステートメントを使用して &lt; RSS フィード内のすべての項目タグを検索 &gt; します。 各項目は反復処理され、関連付けられている &lt; タイトル &gt; と &lt; リンク &gt; タグが配置され、各項目のデータが表示されます。 図3は、JavaScript プロキシ経由で GetRssFeed () Web メソッドに ASP.NET AJAX 呼び出しを行うことによって生成される出力の例を示しています。

## <a name="handling-complex-types"></a>複合型の処理

Web サービスによって受け入れられるか返される複合型は、JavaScript プロキシを介して自動的に公開されます。 ただし、入れ子になった複合型は、前に説明したように、サービスに対して、型の属性が適用されていない限り、クライアント側で直接アクセスすることはできません。 クライアント側で入れ子になった複合型を使用するのはなぜですか。

この質問に答えるには、ASP.NET AJAX ページに顧客データが表示され、エンドユーザーが顧客の住所を更新できるようにすることを前提としています。 Web サービスで、アドレスの種類 (たとえば、顧客の詳細クラスで定義されている複合型) をクライアントに送信できることが指定されている場合、更新プロセスを別の関数に分割して、コードを再利用しやすくすることができます。

[![RSS データを返す Web サービスを呼び出すことによって作成される出力。](understanding-asp-net-ajax-web-services/_static/image8.png)](understanding-asp-net-ajax-web-services/_static/image7.png)

**図 3**: RSS データを返す Web サービスを呼び出すことによって生成される出力。  ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-web-services/_static/image9.png)される)

一覧16は、モデル名前空間で定義されたアドレスオブジェクトを呼び出すクライアント側コードの例を示しています。この例では、更新されたデータを格納し、それを顧客詳細オブジェクトの Address プロパティに割り当てています。 次に、[顧客の詳細] オブジェクトが Web サービスに渡され、処理されます。

**一覧 16.入れ子になった複合型の使用**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample20.js)]

## <a name="creating-and-using-page-methods"></a>ページメソッドの作成と使用

Web サービスは、ASP.NET AJAX ページを含むさまざまなクライアントに対して、再利用可能なサービスを公開する優れた方法を提供します。 ただし、ページが他のページで使用または共有されないデータを取得する必要がある場合もあります。 この場合、サービスは単一のページのみで使用されるため、.asmx ファイルを作成して、ページがデータにアクセスできるようにすることは過剰に思えるかもしれません。

ASP.NET AJAX には、スタンドアロンの .asmx ファイルを作成せずに、Web サービスのような呼び出しを行うための別のメカニズムが用意されています。 これを行うには、"ページメソッド" と呼ばれる手法を使用します。 ページメソッドは、WebMethod 属性が適用されているページまたはコード側ファイルに直接埋め込まれた静的な (VB.NET で共有される) メソッドです。 WebMethod 属性を適用することで、実行時に動的に作成される PageMethods という名前の特殊な JavaScript オブジェクトを使用して呼び出すことができます。 PageMethods オブジェクトは、JSON のシリアル化/逆シリアル化プロセスからのシールドを持つプロキシとして機能します。 PageMethods オブジェクトを使用するには、ScriptManager の EnablePageMethods プロパティを true に設定する必要があることに注意してください。

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample21.aspx)]

リスト17は、ASP.NET のコード側クラスで2つのページメソッドを定義する例を示しています。 これらのメソッドは、Web サイトのアプリコードフォルダーにあるビジネス層クラスからデータを取得 \_ します。

**リスト17。ページメソッドを定義する。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample22.cs)]

ScriptManager がページ内の Web メソッドの存在を検出すると、前に説明した PageMethods オブジェクトへの動的参照を生成します。 Web メソッドを呼び出すには、PageMethods クラスを参照し、その後にメソッドの名前、および渡す必要がある必要なパラメーターデータを参照します。 一覧18では、前に示した2つのページのメソッドを呼び出す例を示します。

**リスト18。PageMethods JavaScript オブジェクトを使用したページメソッドの呼び出し。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample23.js)]

PageMethods オブジェクトの使用は、JavaScript プロキシオブジェクトを使用する場合とよく似ています。 まず、page メソッドに渡す必要があるすべてのパラメーターデータを指定し、次に非同期呼び出しが返されたときに呼び出されるコールバック関数を定義します。 エラーのコールバックを指定することもできます (エラー処理の例については、一覧14を参照してください)。

## <a name="the-autocompleteextender-and-the-aspnet-ajax-toolkit"></a>AutoCompleteExtender and ASP.NET AJAX Toolkit

ASP.NET AJAX Toolkit (から入手可能) には、 [http://ajax.asp.net](http://ajax.asp.net) Web サービスへのアクセスに使用できるいくつかのコントロールが用意されています。 具体的には、ツールキットにはという名前の便利なコントロールが含まれてい `AutoCompleteExtender` ます。これを使用すると、JavaScript コードを記述することなく、Web サービスを呼び出したり、ページにデータを表示したりできます。

AutoCompleteExtender コントロールを使用すると、テキストボックスの既存の機能を拡張し、ユーザーが探しているデータをより簡単に見つけられるようにすることができます。 テキストボックスに入力すると、コントロールを使用して Web サービスのクエリを実行し、結果をテキストボックスの下に動的に表示できます。 図4は、AutoCompleteExtender コントロールを使用して、サポートアプリケーションの顧客 id を表示する例を示しています。 ユーザーがテキストボックスに別の文字を入力すると、入力に基づいて異なる項目がその下に表示されます。 ユーザーは目的の顧客 id を選択できます。

ASP.NET AJAX ページ内で AutoCompleteExtender を使用するには、AjaxControlToolkit.dll アセンブリを Web サイトの bin フォルダーに追加する必要があります。 Toolkit アセンブリが追加されたら、それを web.config で参照して、アプリケーション内のすべてのページでこのツールキットに含まれるコントロールを使用できるようにします。 これを行うには、web.config の controls タグ内に次のタグを追加し &lt; &gt; ます。

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample24.xml)]

特定のページでのみコントロールを使用する必要がある場合は、web.config を更新するのではなく、次に示すように、ページの上部に参照ディレクティブを追加することで参照できます。

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample25.aspx)]

[![AutoCompleteExtender コントロールを使用します。](understanding-asp-net-ajax-web-services/_static/image11.png)](understanding-asp-net-ajax-web-services/_static/image10.png)

**図 4**: AutoCompleteExtender コントロールの使用  ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-web-services/_static/image12.png)される)

ASP.NET AJAX Toolkit を使用するように Web サイトを構成したら、通常の ASP.NET サーバーコントロールを追加するのと同じように、AutoCompleteExtender コントロールをページに追加できます。 リスト19は、コントロールを使用して Web サービスを呼び出す例を示しています。

**リスト19。ASP.NET AJAX Toolkit AutoCompleteExtender コントロールの使用。**

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample26.aspx)]

AutoCompleteExtender には、サーバーコントロールで検出された標準 ID や runat プロパティなど、いくつかの異なるプロパティがあります。 これらに加えて、Web サービスがデータを照会する前に、エンドユーザーが入力する文字数を定義することもできます。 リスト19に示されている MinimumPrefixLength を使用すると、テキストボックスに文字が入力されるたびにサービスが呼び出されます。 この値の設定は、ユーザーが文字を入力するたびに、テキストボックス内の文字と一致する値を検索するために Web サービスが呼び出されるため、慎重に設定する必要があります。 Web サービスとターゲット Web メソッドを呼び出す Web サービスは、それぞれ ServicePath プロパティと ServiceMethod プロパティを使用して定義されます。 最後に、TargetControlID プロパティは、AutoCompleteExtender コントロールをフックするテキストボックスを識別します。

前に説明したように、呼び出される Web サービスには ScriptService 属性が適用されている必要があります。また、対象の Web メソッドは prefixText と count という名前の2つのパラメーターを受け入れる必要があります。 PrefixText パラメーターは、エンドユーザーによって入力された文字を表し、count パラメーターは返される項目の数を表します (既定値は 10)。 リスト20は、前に示した AutoCompleteExtender コントロールによって呼び出された GetCustomerIDs Web メソッドの例を示しています。 Web メソッドは、ビジネス層のメソッドを呼び出します。このメソッドは、データのフィルター処理を処理し、照合結果を返すデータレイヤーメソッドを呼び出します。 データレイヤーメソッドのコードは、一覧21に示されています。

**リスト20。AutoCompleteExtender コントロールから送信されたデータをフィルター処理します。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample27.cs)]

**リスト21。エンドユーザーの入力に基づいて結果をフィルター処理します。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample28.cs)]

## <a name="conclusion"></a>まとめ

ASP.NET AJAX は、要求メッセージと応答メッセージを処理するための多数のカスタム JavaScript コードを記述することなく、Web サービスを呼び出すための優れたサポートを提供します。 この記事では、.NET Web サービスを使用して JSON メッセージを処理できるようにする方法と、ScriptManager コントロールを使用して JavaScript プロキシを定義する方法について説明しました。 また、JavaScript プロキシを使用して Web サービスを呼び出し、単純型と複合型を処理し、エラーに対処する方法についても説明しました。 最後に、ページメソッドを使用して、Web サービス呼び出しを作成および作成するプロセスを簡略化し、AutoCompleteExtender コントロールが入力時にエンドユーザーにヘルプを提供する方法について見てきました。 ASP.NET AJAX で利用できる UpdatePanel は、その単純さにより、多くの AJAX プログラマにとっては確実に選択できますが、JavaScript プロキシを介して Web サービスを呼び出す方法を理解することは、多くのアプリケーションで役に立ちます。

## <a name="bio"></a>略歴

Dan Wahlin (ASP.NET と XML Web サービスの Microsoft の最も重要なプロフェッショナル) は、.NET 開発のインストラクターとアーキテクチャコンサルタントであり、インターフェイス技術トレーニング () を使用してい [http://www.interfacett.com](http://www.interfacett.com) ます。 XML for ASP.NET 開発者向け Web サイト ([www.XMLforASP.NET](http://www.XMLforASP.NET)) を設立した Dan は、Ineta スピーカーの事務局にあり、いくつかのカンファレンスで講演を行っています。 Dan 共同で作成された Professional Windows DNA (Wrox)、ASP.NET: ヒント、チュートリアルとコード (Sams)、ASP.NET 1.1 Insider ソリューション、Professional ASP.NET 2.0 AJAX (Wrox)、ASP.NET 2.0 MVP ハッキング、および ASP.NET 開発者向け XML の作成 (Sams)。 コード、記事、または書籍を書いていない人は、音楽を書いて録音し、妻や子供と共にゴルフやバスケットボールを楽しんでいます。

Scott Cate は1997以来 Microsoft の Web テクノロジを使用しています。また、myKB.com ([www.myKB.com](http://www.myKB.com)) の大統領で、サポート技術情報のソフトウェアソリューションに重点を置いた ASP.NET ベースのアプリケーションを作成することを専門としています。 Scott は [scott.cate@myKB.com](mailto:scott.cate@myKB.com) 、 [ScottCate.com](http://ScottCate.com)で電子メールまたは彼のブログから連絡を受けることができます。

> [!div class="step-by-step"]
> [前へ](understanding-asp-net-ajax-localization.md)
> [次へ](understanding-asp-net-ajax-debugging-capabilities.md)
