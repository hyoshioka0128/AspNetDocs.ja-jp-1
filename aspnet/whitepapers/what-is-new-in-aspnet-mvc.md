---
uid: whitepapers/what-is-new-in-aspnet-mvc
title: ASP.NET MVC 2 の新機能 |Microsoft Docs
author: rick-anderson
description: このドキュメントでは、ASP.NET MVC 2 で導入された新機能と機能強化について説明します。 このドキュメントは、ダウンロードすることもできます。
ms.author: riande
ms.date: 04/20/2010
ms.assetid: 69a8d6f8-4b10-4602-8822-2d6c05fc432b
msc.legacyurl: /whitepapers/what-is-new-in-aspnet-mvc
msc.type: content
ms.openlocfilehash: ecc840c33714aa04bebcd9e413cb548eca8cc058
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045040"
---
# <a name="whats-new-in-aspnet-mvc-2"></a>ASP.NET MVC 2 の新機能

> このドキュメントでは、ASP.NET MVC 2 で導入された新機能と機能強化について説明します。 このドキュメントは、[ダウンロード](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf)することもできます。

[基礎](#_TOC1)   
[ASP.NET MVC 1.0 プロジェクトを ASP.NET MVC 2 にアップグレードする](#_TOC2)   
[新機能](#_TOC3)   
[テンプレートヘルパー](#_TOC3_1)   
[場所](#_TOC3_2)   
[非同期コントローラーのサポート](#_TOC3_3)   
[アクションメソッドパラメーターの DefaultValueAttribute のサポート](#_TOC3_4)   
[モデルバインダーを使用したバイナリデータのバインドのサポート](#_TOC3_5)   
[ModelMetadata および ModelMetadataProvider クラス](#_TOC3_6)   
[DataAnnotations 属性のサポート](#_TOC3_7)   
[モデルの検証コントロールプロバイダー](#_TOC3_8)   
[クライアント側の検証](#_TOC3_9)   
[Visual Studio 2010 の新しいコードスニペット](#_TOC3_10)   
[新しい RequireHttpsAttribute アクションフィルター](#_TOC3_11)   
[HTTP メソッド動詞のオーバーライド](#_TOC3_12)   
[テンプレートヘルパーの New HiddenInputAttribute クラス](#_TOC3_13)   
[Html. ValidationSummary ヘルパーメソッドは、モデルレベルのエラーを表示できます](#_TOC3_14)   
[Visual Studio の T4 テンプレートでは、.NET Framework API の機能強化のターゲットバージョンに固有のコードが生成さ](#_TOC3_15)[API Improvements](#_TOC4)れます  
[重大な変更](#_TOC5)  
[免責事項](#_TOC6)  

## <a name="introduction"></a><a id="_TOC1"></a>  基礎

ASP.NET MVC 2 は ASP.NET MVC 1.0 上に構築されており、生産性を高めることに重点を置いた多数の拡張機能と機能が導入されています。 このリリースは ASP.NET MVC 1.0 と互換性があるため、ASP.NET MVC 1.0 のすべての知識、スキル、コード、および拡張機能が引き続き適用されます。

ASP.NET MVC の詳細については、次のリソースを参照してください。

- [MSDN の ASP.NET MVC ドキュメント](https://go.microsoft.com/fwlink/?LinkId=159758)
- [ASP.NET MVC Web サイト](https://asp.net/mvc/)
- [ASP.NET MVC フォーラム](https://forums.asp.net/1146.aspx)

## <a name="upgrading-an-aspnet-mvc-10-project-to-aspnet-mvc-2"></a><a id="_TOC2"></a>  ASP.NET MVC 1.0 プロジェクトを ASP.NET MVC 2 にアップグレードする

ASP.NET MVC 2 は、同じサーバーに ASP.NET MVC 1.0 とサイドバイサイドでインストールできます。これにより、アプリケーション開発者は、ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 にアップグレードするタイミングを柔軟に選択できます。 アップグレード方法の詳細については、「 [ASP.NET mvc 1.0 アプリケーションを ASP.NET mvc 2 にアップグレードする](https://go.microsoft.com/fwlink/?LinkID=185459)」を参照してください。

## <a name="new-features"></a><a id="_TOC3"></a>  新機能

このセクションでは、MVC 2 リリースで導入された機能について説明します。

### <a name="templated-helpers"></a><a id="_TOC3_1"></a>  テンプレートヘルパー

テンプレートヘルパーを使用すると、編集および表示する HTML 要素をデータ型で自動的に関連付けることができます。 たとえば、system.string 型のデータがビューに表示されている場合、日付の選択 UI 要素を自動的に表示できます。 これは、ASP.NET 動的データでのフィールドテンプレートの動作に似ています。 詳細については、MSDN Web サイトの「テンプレート化された [ヘルパーを使用したデータの表示](https://go.microsoft.com/fwlink/?LinkId=159062) 」を参照してください。

### <a name="areas"></a><a id="_TOC3_2"></a>  場所

区分を使用すると、大規模な Web アプリケーションの複雑さを管理するために、大きなプロジェクトを複数の小さなセクションに整理できます。 各セクション ("area") は、通常、大規模な Web サイトの個別のセクションを表し、コントローラーとビューの関連するセットをグループ化するために使用されます。 詳細については、MSDN Web サイトの「 [チュートリアル: 領域ごとの ASP.NET MVC アプリケーションの整理](https://go.microsoft.com/fwlink/?LinkId=158978) 」を参照してください。

新しい領域を作成するには、ソリューションエクスプローラーでプロジェクトを右クリックし、[追加] をクリックして、[区分] をクリックします。 これにより、領域名の入力を求めるダイアログボックスが表示されます。 区分名を入力すると、Visual Studio によってプロジェクトに新しい領域が追加されます。

次の図は、管理者とブログの2つの領域を持つプロジェクトのレイアウト例を示しています。

![](what-is-new-in-aspnet-mvc/_static/image1.png)

区分を作成すると、Visual Studio は、領域登録から派生したクラスを各領域に追加します。 このクラスは、次の例に示すように、領域とそのルートを登録するために必要です。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample1.cs)]

ASP.NET MVC 2 の既定のプロジェクトテンプレートには、global.asax ファイルのコードの RegisterAllAreas メソッドの呼び出しが含まれています。 このメソッドは、領域登録クラスから派生したすべての型を検索し、その型のインスタンスをインスタンス化して、インスタンスで RegisterArea メソッドを呼び出すことによって、プロジェクト内の各領域を登録します。 この方法を次の例に示します。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample2.cs)]

コンテキストを呼び出すことによって、RegisterArea メソッドで名前空間を指定しない場合。Namespace. Add メソッド。既定では、登録クラスの名前空間が使用されます。

### <a name="support-for-asynchronous-controllers"></a><a id="_TOC3_3"></a>  非同期コントローラーのサポート

ASP.NET MVC 2 では、コントローラーが要求を非同期に処理できるようになりました。 これにより、ブロック操作 (ネットワーク要求など) を頻繁に呼び出すサーバーが、代わりに非ブロッキング対応を呼び出すことができるため、パフォーマンスが向上する可能性があります。 詳細については、MSDN の「 [ASP.NET MVC での非同期コントローラーの使用](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx) 」トピックを参照してください。

### <a name="support-for-defaultvalueattribute-in-action-method-parameters"></a><a id="_TOC3_4"></a>  アクションメソッドパラメーターの DefaultValueAttribute のサポート

System.componentmodel クラスを使用すると、アクションメソッドの引数パラメーターに既定値を指定できます。 たとえば、次の既定のルートが定義されているとします。

[!code-json[Main](what-is-new-in-aspnet-mvc/samples/sample3.txt)]

また、次のコントローラーとアクションメソッドが定義されていることを前提としています。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample4.cs)]

次のいずれかの要求 Url は、前の例で定義されているビューアクションメソッドを呼び出します。

- /Article/View/123
- /Article/View/123? page = 1 (実質的には前の要求と同じ)
- /Article/View/123? ページ = 2

DefaultValueAttribute 属性を指定しない場合、ページ引数は null 非許容の値型に値が指定されていないため、上記のリストの最初の URL は機能しません。

コードが Visual Basic 2010 または Visual C# 2010 で記述されている場合は、次の例に示すように、DefaultValueAttribute 属性ではなく、省略可能なパラメーターを使用できます。

[!code-vb[Main](what-is-new-in-aspnet-mvc/samples/sample5.vb)]

### <a name="support-for-binding-binary-data-with-model-binders"></a><a id="_TOC3_5"></a>  モデルバインダーを使用したバイナリデータのバインドのサポート

バイナリ値を base-64 エンコードされた文字列としてエンコードする、次の2つの新しいオーバーロードヘルパーがあります。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample6.cs)]

一般的な用途は、ビューにオブジェクトのタイムスタンプを埋め込むことです。 たとえば、アプリケーションに次のような製品オブジェクトが含まれているとします。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample7.cs)]

編集フォームでは、次の例に示すように、タイムスタンププロパティをフォームに表示できます。

[!code-aspx[Main](what-is-new-in-aspnet-mvc/samples/sample8.aspx)]

このマークアップは、次の例のような base 64 エンコード文字列としてタイムスタンプ値を持つ非表示の input 要素をレンダリングします。

[!code-html[Main](what-is-new-in-aspnet-mvc/samples/sample9.html)]

このフォームは、次の例に示すように、Product 型の引数を持つアクションメソッドにポストされる場合があります。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample10.cs)]

アクションメソッドでは、ポストされた base-64 エンコード文字列がバイト配列に変換されるため、TimeStamp プロパティが正しく設定されます。

### <a name="modelmetadata-and-modelmetadataprovider-classes"></a><a id="_TOC3_6"></a>  ModelMetadata および ModelMetadataProvider クラス

ModelMetadataProvider クラスは、ビュー内のモデルのメタデータを取得するための抽象化を提供します。 MVC 2 には、System.componentmodel 名前空間の属性によって公開されるメタデータを使用できるようにする既定のプロバイダーが含まれています。 データベースや XML ファイルなどの他のデータストアからメタデータを提供するメタデータプロバイダーを作成することができます。

ViewDataDictionary クラスは、ModelMetadataProvider クラスによってモデルから抽出されたメタデータを含む ModelMetadata オブジェクトを公開します。 これにより、テンプレート化されたヘルパーはこのメタデータを使用し、それに応じて出力を調整できます。

詳細については、 [Modelmetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) クラスおよび [modelmetadataprovider](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) クラスのドキュメントを参照してください。

### <a name="support-for-dataannotations-attributes"></a><a id="_TOC3_7"></a>  DataAnnotations 属性のサポート

ASP.NET MVC 2 では、入力の検証を行うためにモデルにバインドするときに、RangeAttribute、RequiredAttribute、Stringlength 属性、および RegexAttribute validation 属性 (System.componentmodel 名前空間で定義されています) の使用をサポートしています。

詳細については、MSDN Web サイトの「 [方法: DataAnnotations 属性を使用してモデルデータを検証する](https://go.microsoft.com/fwlink/?LinkId=159063) 」を参照してください。 これらの属性の使用方法を示すサンプルプロジェクトは、でダウンロードでき [https://go.microsoft.com/fwlink/?LinkId=157753](https://go.microsoft.com/fwlink/?LinkId=157753) ます。

### <a name="model-validator-providers"></a><a id="_TOC3_8"></a>  モデルの検証コントロールプロバイダー

モデル検証プロバイダークラスは、モデルの検証ロジックを提供する抽象化を表します。 ASP.NET MVC には、System.componentmodel 名前空間に含まれる検証属性に基づく既定のプロバイダーが含まれています。 また、カスタム検証規則と、モデルに対する検証規則のカスタムマッピングを定義する独自の検証プロバイダーを作成することもできます。 詳細については、 [Modelvalidatorprovider](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx) クラスのドキュメントを参照してください。

### <a name="client-side-validation"></a><a id="_TOC3_9"></a>  クライアント側の検証

モデル検証コントロールプロバイダークラスは、クライアント側の検証ライブラリで使用できる JSON でシリアル化されたデータの形式でブラウザーに検証メタデータを公開します。 ASP.NET MVC 2 には、前に説明した DataAnnotations 名前空間検証属性をサポートするクライアント検証ライブラリおよびアダプターが含まれています。 また、プロバイダークラスを使用すると、JSON データを処理するアダプターを記述し、別のライブラリを呼び出すことによって、他のクライアント検証ライブラリを使用することもできます。

### <a name="new-code-snippets-for-visual-studio-2010"></a><a id="_TOC3_10"></a>  Visual Studio 2010 の新しいコードスニペット

ASP.NET MVC 2 用の HTML コードスニペットのセットは、Visual Studio 2010 と共にインストールされます。 これらのスニペットの一覧を表示するには、[ツール] メニューの [コードスニペットマネージャー] をクリックします。 言語として [HTML] を選択し、[場所] で [ASP.NET MVC 2] を選択します。 コードスニペットの使用方法の詳細については、Visual Studio のドキュメントを参照してください。

### <a name="new-requirehttpsattribute-action-filter"></a><a id="_TOC3_11"></a>  新しい RequireHttpsAttribute アクションフィルター

ASP.NET MVC 2 には、アクションメソッドとコントローラーに適用できる新しい RequireHttpsAttribute クラスが含まれています。 既定では、フィルターは SSL 以外 (HTTP) 要求を SSL 対応 (HTTPS) にリダイレクトします。

### <a name="overriding-the-http-method-verb"></a><a id="_TOC3_12"></a>  HTTP メソッド動詞のオーバーライド

REST アーキテクチャスタイルを使用して Web サイトを構築する場合、リソースに対して実行するアクションを決定するために HTTP 動詞が使用されます。 REST では、アプリケーションが GET、PUT、POST、DELETE などの一般的な HTTP 動詞の完全な範囲をサポートしている必要があります。

ASP.NET MVC 2 には、アクションメソッドに適用できる新しい属性と、その機能の compact 構文が含まれています。 これらの属性により、ASP.NET MVC は HTTP 動詞に基づいてアクションメソッドを選択できます。 次の例では、POST 要求は最初のアクションメソッドを呼び出し、PUT 要求は2番目のアクションメソッドを呼び出します。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample11.cs)]

以前のバージョンの ASP.NET MVC では、次の例に示すように、これらのアクションメソッドはより詳細な構文を必要としていました。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample12.cs)]

ブラウザーは GET および POST HTTP 動詞のみをサポートしているため、別の動詞を必要とするアクションにポストすることはできません。 そのため、すべての RESTful 要求をネイティブにサポートすることはできません。

ただし、POST 操作中に RESTful 要求をサポートするために、ASP.NET MVC 2 には新しい HttpMethodOverride HTML ヘルパーメソッドが導入されています。 このメソッドは、フォームが任意の HTTP メソッドを効果的にエミュレートする、非表示の input 要素をレンダリングします。 たとえば、HttpMethodOverride HTML ヘルパーメソッドを使用すると、フォーム送信を PUT または DELETE 要求として表示できます。 HttpMethodOverride の動作は、次の属性に影響します。

- HttpPostAttribute
- HttpPutAttribute
- HttpGetAttribute
- HttpDeleteAttribute
- AcceptVerbsAttribute

非表示の input 要素の名前は、"X-HTTP-Method-Override" で、値は "HTTP 動詞" に設定されます。 オーバーライド値は、HTTP ヘッダーまたはクエリ文字列値の名前と値のペアとして指定することもできます。

オーバーライドは、実際の要求が POST 要求の場合にのみ使用できます。 他の HTTP 動詞を使用する要求では、オーバーライド値は無視されます。

### <a name="new-hiddeninputattribute-class-for-templated-helpers"></a><a id="_TOC3_13"></a>  テンプレートヘルパーの New HiddenInputAttribute クラス

新しい HiddenInputAttribute 属性をモデルプロパティに適用すると、エディターテンプレートでモデルを表示するときに、非表示の input 要素を表示するかどうかを指定できます。 (属性は、暗黙的な UIHint 値 HiddenInput) を設定します。 属性の DisplayValue プロパティを使用して、エディターと表示モードのどちらで値を表示するかを指定できます。 DisplayValue が false に設定されている場合は、通常、フィールドを囲む HTML マークアップではなく、何も表示されません。 DisplayValue の既定値は true です。

次のシナリオでは、HiddenInputAttribute 属性を使用できます。

- ビューでオブジェクトの ID を編集できるときに、値を表示するだけでなく、古い ID を含む非表示の入力要素を指定して、コントローラーに渡すことができるようにする場合。
- タイムスタンププロパティなど、表示されないバイナリプロパティをユーザーが編集できるようにする場合。 その場合、値とそれに関連する HTML マークアップ (ラベルや値など) は表示されません。

次の例は、HiddenInputAttribute クラスの使用方法を示しています。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample13.cs)]

属性が true に設定されている場合 (またはパラメーターが指定されていない場合)、次のようになります。

- [表示テンプレート] にラベルが表示され、値がユーザーに表示されます。
- エディターテンプレートでは、ラベルがレンダリングされ、値が非表示の input 要素に表示されます。

属性が false に設定されている場合、次のようになります。

- 表示テンプレートでは、そのフィールドに対して何もレンダリングされません。
- エディターテンプレートでは、ラベルは表示されず、値は非表示の input 要素に表示されます。

### <a name="htmlvalidationsummary-helper-method-can-display-model-level-errors"></a><a id="_TOC3_14"></a>  Html. ValidationSummary ヘルパーメソッドは、モデルレベルのエラーを表示できます

すべての検証エラーを常に表示するのではなく、Html の ValidationSummary ヘルパーメソッドには、モデルレベルのエラーのみを表示する新しいオプションがあります。 これにより、モデルレベルのエラーが、各フィールドの横に表示される検証の概要とフィールド固有のエラーに表示されるようになります。

### <a name="t4-templates-in-visual-studio-generate-code-that-is-specific-to-the-target-version-of-the-net-framework"></a><a id="_TOC3_15"></a>  Visual Studio の T4 テンプレートでは、対象となるバージョンの .NET Framework に固有のコードが生成されます

ASP.NET MVC T4 ホストから、アプリケーションで使用される .NET Framework のバージョンを指定する新しいプロパティを使用できます。 これにより、T4 テンプレートを使用して、.NET Framework のバージョンに固有のコードとマークアップを生成することができます。 Visual Studio 2008 では、値は常に .NET 3.5 です。 Visual Studio 2010 では、値は .NET 3.5 または .NET 4 です。

## <a name="api-improvements"></a><a id="_TOC4"></a>  API の機能強化

このセクションでは、既存の ASP.NET MVC の型とメンバーに対する変更について説明します。

- 保護された仮想 CreateActionInvoker 元メソッドがコントローラークラスに追加されました。 このメソッドは、コントローラーの ActionInvoker 元プロパティによって呼び出され、呼び出し元が既に設定されていない場合に、呼び出し元の遅延インスタンス化を可能にします。
- AuthorizeAttribute クラスに protected virtual HandleUnauthorizedRequest メソッドが追加されました。 これにより、承認が失敗したときの動作を制御するために、AuthorizeAttribute から派生したフィルターが有効になります。
- ValueProviderDictionary クラスに Add (文字列キー、オブジェクト値) メソッドを追加しました。 これにより、次の例に示すように、ValueProviderDictionary の辞書初期化子構文を使用できます。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample14.cs)]

- \_AjaxContext クラスに get object メソッドが追加されました。 これは get data メソッドに似た JavaScript メソッドです \_ が、応答のコンテンツの種類が application/json の場合、get object は \_ json オブジェクトを返します。
- AuthorizationContext クラスに ActionDescriptor プロパティが追加されました。
- UrlParameter が追加されました。省略可能なトークン。プロパティがフォームポストに存在しない場合に、ID プロパティを含むモデルにバインドするときに問題を回避するために使用できます。 詳細については、Phil Haack のブログの記事「 [ASP.NET MVC 2 OPTIONAL URL Parameters](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx) 」を参照してください。

## <a name="breaking-changes"></a><a id="_TOC5"></a>  重大な変更

次の変更によって、既存の ASP.NET MVC 1.0 アプリケーションでエラーが発生する可能性があります。

#### <a name="change-in-property-validation-behavior-for-classes-that-implement-idataerrorinfo"></a>IDataErrorInfo を実装するクラスのプロパティ検証動作の変更

IDataErrorInfo を使用して検証を実行するモデルオブジェクトの場合、新しい値が設定されているかどうかに関係なく、すべてのプロパティが検証されます。 ASP.NET MVC 1.0 では、新しい値が設定されたプロパティのみが検証されました。 ASP.NET MVC 2 では、IDataErrorInfo の Error プロパティは、すべてのプロパティ検証コントロールが成功した場合にのみ呼び出されます。

#### <a name="iis-script-mapping-script-is-no-longer-available-in-the-installer"></a>IIS スクリプトマッピングスクリプトがインストーラーで使用できなくなりました

IIS スクリプトマッピングスクリプトは、IIS 6 および IIS 7 用のスクリプトマップをクラシックモードで構成するために使用されるコマンドラインスクリプトです。 Visual Studio 開発サーバーを使用する場合、または統合モードで IIS 7 を使用する場合は、スクリプトマッピングスクリプトは必要ありません。 スクリプトは、 [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)でサポートされていない個別のダウンロードとして入手できます。

#### <a name="the-htmlsubstitute-helper-method-in-mvc-futures-is-no-longer-available"></a>MVC のフューチャの Html. 代替ヘルパーメソッドは使用できなくなりました

MVC ビューエンジンのレンダリング動作の変更により、Html. 代替ヘルパーメソッドは動作せず、削除されました。

#### <a name="the-ivalueprovider-interface-replaces-all-uses-of-idictionary"></a>IValueProvider インターフェイスは、IDictionary のすべての使用を置き換えます。

MVC 1.0 で IDictionary を受け入れたすべてのプロパティまたはメソッドの引数は、IValueProvider を受け入れるようになりました。 この変更は、カスタム値プロバイダーまたはカスタムモデルバインダーを含むアプリケーションにのみ影響します。 この変更の影響を受けるプロパティとメソッドの例を次に示します。

- コントローラークラスと ModelBindingContext クラスの ValueProvider プロパティ。
- コントローラークラスの TryUpdateModel メソッド。

#### <a name="new-css-classes-were-added-in-the-sitecss-file"></a>新しい CSS クラスが、サイト .css ファイルに追加されました

ASP.NET MVC プロジェクトテンプレートのサイト .css ファイルが更新され、検証機能およびテンプレート化されたヘルパーによって使用される新しいスタイルが追加されました。

#### <a name="helpers-now-return-an-mvchtmlstring-object"></a>ヘルパーが MvcHtmlString オブジェクトを返すようになりました

ASP.NET 4 で HTML エンコード式の新しい構文を利用するために、HTML ヘルパーの戻り値の型は文字列ではなく MvcHtmlString になりました。 ASP.NET MVC 2 と新しいヘルパーを ASP.NET 3.5 で使用する場合、HTML エンコード構文を利用することはできません。新しい構文は、ASP.NET 4 で ASP.NET MVC 2 を実行する場合にのみ使用できます。

#### <a name="jsonresult-now-responds-only-to-http-post-requests"></a>JsonResult は HTTP POST 要求にのみ応答するようになりました

情報漏えいの可能性がある JSON ハイジャック攻撃を軽減するために、既定では、JsonResult クラスは HTTP POST 要求にのみ応答するようになりました。 JsonResult オブジェクトを返すアクションメソッドの Ajax GET 呼び出しは、代わりに POST を使用するように変更する必要があります。 必要に応じて、JsonResult の新しい JsonRequestBehavior プロパティを設定することによって、この動作をオーバーライドできます。 潜在的な悪用の詳細については、ブログ記事「Phil Haack の [JSON ハイジャック](http://haacked.com/archive/2009/06/25/json-hijacking.aspx) 」を参照してください。

#### <a name="model-and-modeltype-property-setters-on-modelbindingcontext-are-obsolete"></a>ModelBindingContext の Model および ModelType プロパティ setter は廃止されています

新しい設定可能な ModelMetadata プロパティが ModelBindingContext クラスに追加されました。 新しいプロパティは、Model プロパティと ModelType プロパティの両方をカプセル化します。 Model および ModelType プロパティは互換性のために残されていますが、旧バージョンとの互換性のために、プロパティ getter は引き続き動作します。これらは、値を取得するために ModelMetadata プロパティにデリゲートします。

#### <a name="changes-to-the-defaultcontrollerfactory-class-break-custom-controller-factories-that-derive-from-it"></a>Defaultcontroller ファクトリクラスに対する変更により、そのクラスから派生したカスタムコントローラーファクトリが中断されます。

Defaultコントローラーファクトリクラスは、RequestContext プロパティを削除することによって修正されました。 このプロパティの代わりに、要求コンテキストインスタンスは、保護された仮想 Getコントローラーインスタンスと Getコントローラー型のメソッドに渡されます。 この変更は、Defaultcontroller ファクトリから派生したカスタムコントローラーファクトリに影響します。

カスタムコントローラーファクトリは、ASP.NET MVC アプリケーションの依存関係の挿入を提供するためによく使用されます。 ASP.NET MVC 2 をサポートするようにカスタムコントローラーファクトリを更新するには、新しいシグネチャに一致するようにメソッドのシグネチャまたはシグネチャを変更し、プロパティの代わりに要求コンテキストパラメーターを使用します。

#### <a name="area-is-a-now-a-reserved-route-value-key"></a>"Area" は現在予約されているルート値のキーです

ルート値の文字列 "area" は、"controller" と "action" の場合と同じように、ASP.NET MVC では特別な意味を持ちます。 1つの意味として、HTML ヘルパーに "area" を含むルート値ディクショナリが指定されている場合、ヘルパーはクエリ文字列に "area" を追加しなくなります。

区分機能を使用している場合は、ルート URL の一部として {area} を使用しないようにしてください。

## <a name="disclaimer"></a><a id="_TOC6"></a>  免責事項

このドキュメントは暫定版であり、ここで説明するソフトウェアの最終的な商業リリースより前に大幅に変更される可能性があります。

このドキュメントに含まれる情報は、取り上げている問題についての、公開時点における Microsoft Corporation の見解を表します。 Microsoft は変化する市場状況に対応する必要があるため、これを Microsoft による確約と解釈しないでください。Microsoft は、記載されている情報の公開後の正確さを保証できません。

このホワイト ペーパーは、情報提供のみを目的としています。 マイクロソフトは、このドキュメント内の情報に関して、明示的、暗黙的、または法的ないかなる保証も行いません。

お客様ご自身の責任において、適用されるすべての著作権関連法規に従ったご使用を願います。 このソフトウェアおよびマニュアルのいかなる部分も、米国 Microsoft Corporation の書面による許諾を受けることなく、その目的を問わず、どのような形態であっても、複製または譲渡することは禁じられています。ここでいう形態とは、複写や記録など、電子的な、または物理的なすべての手段を含みます。

Microsoft は、このマニュアルに記載されている内容に関し、特許、特許申請、商標、著作権、またはその他の無体財産権を有する場合があります。 別途マイクロソフトのライセンス契約上に明示の規定がない限り、このドキュメントはこれらの特許、商標、著作権、またはその他の無体財産権に関する権利をお客様に許諾するものではありません。

特に明記されていない限り、ここに記載されている会社、組織、製品、ドメイン名、電子メールアドレス、ロゴ、人物、場所、およびイベントの例は架空のものであり、実在する企業、組織、製品、ドメイン名、電子メールアドレス、ロゴ、人物、場所、イベントとは一切関係ありません。

© 2010 Microsoft Corporation.  All rights reserved.

Microsoft および Windows は、米国および他の国における Microsoft Corporation の登録商標または商標です。

本ドキュメントで説明する実際の製造元および製品名は、それぞれの所有者の商標である場合があります。
