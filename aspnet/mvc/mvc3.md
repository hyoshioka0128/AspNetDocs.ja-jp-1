---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: (2011年4月ツールアップデートを含む)ASP.NET MVC 3 は、確立されたデザイン パターンを使用して、スケーラブルな標準ベースの Web アプリケーションを構築するためのフレームワークです。
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 6fe734dc0d0106bb346df154e1e03f97b307567a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675139"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

> *(2011年4月ツールアップデートを含む)*
> 
> ASP.NET MVC 3 は、確立された設計パターンとASP.NETと .NET Framework の機能を使用して、スケーラブルな標準ベースの Web アプリケーションを構築するためのフレームワークです。
> 
> それはASP.NETMVC 2と並んでインストールするので、今日それを使用して開始してください!
> 
> インストーラを[ダウンロードする](https://microsoft.com/download/details.aspx?id=4211)

## <a name="top-features"></a>トップ機能

- NuGet 経由で拡張可能な統合スキャフォールディング システム
- HTML 5 有効プロジェクト テンプレート
- 新しいカミソリビューエンジンを含む表現力豊かなビュー
- 依存性注入とグローバルアクションフィルタを備えた強力なフック
- 控えめな JavaScript、jQuery 検証、JSON バインディングを使用した豊富な JavaScript サポート
- *[以下](#overview)の機能の全リストを読む*

## <a name="top-links"></a>トップリンク

mvc 3 の新機能ASP.NET

- フィル・ハーク: [ASP.NET MVC 3 リリース済み](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- スコット・ヘンゼルマン: [ASP.NET MVC3、ウェブマトリックス、ヌゲット、IISエクスプレス、オーチャードがリリース - マイクロソフト 1 月の Web リリースをコンテキストでリリース](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- スコット・ガスリー: [ASP.NET MVC 3、IIS エクスプレス、SQL CE 4、Web ファーム フレームワーク、オーチャード、WebMatrix のリリースを発表](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [ASP.NET MVC 3 のリリース ノート](../whitepapers/mvc3-release-notes.md)

インストールとヘルプ

- Web プラットフォーム インストーラーを使用して ASP.NET MVC 3 をインストール[する (推奨)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)
- [インストーラーの実行可能ファイル](https://go.microsoft.com/fwlink/?LinkID=208140)を使用してASP.NET MVC 3 をインストールします。
- [Visual Studio 11 開発者プレビューのASP.NET MVC 3 をインストールします。](https://go.microsoft.com/fwlink/?LinkID=208140)
- MVC 3 チュートリアルASP.NET[イントロを](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)読む
- フォーラムでASP.NETMVC 3に関するヘルプを取得[し、議論する](https://forums.asp.net/1146.aspx)

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>ASP.NET MVC 3 Overview (ASP.NET MVC 3 の概要)

mvc 3 ASP.NET、ASP.NET MVC 1 と 2 に基づいて構築され、コードを簡略化し、より深い拡張性を実現する優れた機能を追加します。 このトピックでは、このリリースに含まれる多くの新機能の概要を、以下のセクションに編成して説明します。

- [MvcScaffold統合による拡張可能な足場](#BM_MvcScaffolding)
- [HTML 5 有効プロジェクト テンプレート](#BM_HTML5)
- [カミソリビューエンジン](#BM_TheRazorViewEngine)
- [複数ビュー エンジンのサポート](#BM_Support_for_Multiple_View_Engines)
- [コントローラの改良点](#BM_Controller_Improvements)
- [ジャワスクリプトとアヤックス](#BM_JavaScript_and_Ajax_Improvements)
- [モデル検証の改善](#BM_Model_Validation_Improvements)
- [依存性注入の改善](#BM_Dependency_Injection_Improvements)
- [その他の新機能](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>MvcScaffold統合による拡張可能な足場

新しいスキャフォールディング システムを使用すると、フレームワークにまったく新しい場合は、生産性を向上させ、経験があり、既に実行している作業を把握している場合は、一般的な開発タスクを自動化することが容易になります。

これは **、MvcScaffolding**と呼ばれる新しい NuGet ス*キャフォール*ディング パッケージでサポートされています。 「スキャフォールディング」という用語は、多くのソフトウェア技術で「編集してカスタマイズできるソフトウェアの基本的な概要を迅速に生成する」ことを意味します。 ASP.NET MVC 用に作成するスキャフォールディング パッケージは、いくつかのシナリオで非常に有益です。

- **MVC ASP.NET を初めて学習する場合は**、便利なコードを入手する迅速な方法を提供し、必要に応じて編集および調整できます。 空白のページを見てどこから始めればよいかわからないというトラウマからあなたを救います!
- ASP.NETMVCを知っていて、オブジェクトリレーショナルマッパー、ビューエンジン、テストライブラリなどの**新しいアドオン技術を探求している場合**は、その技術の作成者もスキャフォールディングパッケージを作成している可能性があります。
- **同じようなクラスやファイルを繰り返し作成**する作業が必要な場合は、テスト用の備品、配置スクリプト、その他必要なものを出力するカスタムスキャフフォルダーを作成できます。 チームの全員がカスタムスキャフフォルダを使用することもできます。

MvcScaffoldingの他の機能は次のとおりです。

- C# および VB プロジェクトのサポート
- Razor と ASPX ビュー エンジンのサポート
- ASP.NET MVC 領域へのスキャフォールディングをサポートし、カスタム ビュー レイアウト/マスターを使用します。
- T4テンプレートを編集することで出力を簡単にカスタマイズできます
- PowerShell のカスタム ロジックとカスタム T4 テンプレートを使用して、まったく新しいスキャフフォルダーを追加できます。 これらのパラメーター (および指定したカスタム パラメーター) は、コンソールタブ補完リストに自動的に表示されます。
- さまざまなテクノロジ用の追加のスキャフフォルダーを含む NuGet パッケージを取得し (たとえば、LINQ to SQL 用の概念実証パッケージがあります)、それらを組み合わせて一致させることができます。

ASP.NET MVC 3 ツールの更新プログラムには、このスキャフォールディング システムの優れた Visual Studio サポートが含まれています。

- [コントローラの追加] ダイアログでは、作成、読み取り、更新、および削除のコントローラ アクションと対応するビューのフル自動スキャフォールディングがサポートされるようになりました。 既定では、EF Code First を使用してデータ アクセス コードをスキャフォールディングします。
- [コントローラーの追加] ダイアログは *、MvcScaffolding*などの NuGet パッケージを介して*拡張可能な*スキャフォールディングをサポートしています。 これにより、カスタムスキャフォールドをダイアログに接続して、NHibernate や ODBCDirect を使用した JET などの他のデータ アクセス テクノロジのスキャフォールディングを作成できます。

ASP.NET MVC 3 でスキャフォールディングの詳細については、次のリソースを参照してください。

- スティーブ・サンダーソンのポストシリーズは次のとおりです。 

    1. [はじめに:mvcScaffoldingパッケージを使用してASP.NETMVC 3プロジェクトをスキャフォールディング](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [標準的な使用法: 一般的なユースケースとオプション](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [一対多の関係](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [スキャフォールディングアクションと単体テスト](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [T4 テンプレートのオーバーライド](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [この投稿: カスタム スキャフフォルダーの作成](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- マイクロソフトとのブログを構築する彼のPDC 2010セッションからのスコット・ヘンゼルマンの投稿["Web愛の無名のパッケージ"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)
- [MVC 3 リリースノート](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>HTML 5 プロジェクト テンプレート

[新しいプロジェクト] ダイアログには、HTML 5 バージョンのプロジェクト テンプレートを有効にするチェックボックスが含まれています。 これらのテンプレートは、下位レベルのブラウザで HTML 5 と CSS 3 の互換性サポートを提供するために Modernizr 1.7 を活用します。

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>カミソリビューエンジン

ASP.NET MVC 3 には、次の利点を提供する Razor という名前の新しいビュー エンジンが付属しています。

- Razor 構文はクリーンで簡潔で、キーストロークの最小数が必要です。
- Razor は、C# や Visual Basic などの既存の言語に基づいているため、簡単に学習できます。
- Visual Studio には、Razor 構文の IntelliSense とコードの色付けが含まれています。
- Razor ビューは、アプリケーションを実行したり、Web サーバーを起動する必要なく単体テストできます。

いくつかの新しい Razor 機能を次に示します。

- `@model`ビューに渡される型を指定するための構文。
- `@* *@`コメント構文。
- サイト全体に対して 1 回`layoutpage`だけ既定値 ( など) を指定する機能。
- HTML`Html.Raw`エンコードを使用せずにテキストを表示するメソッド。
- 複数のビュー (*\_ビュースタート.cshtml または**\_ビュースタート.vbhtml*ファイル) 間でコードを共有するためのサポート。

Razor には、次のような新しい HTML ヘルパーも含まれています。

- `Chart`. ASP.NET 4 のグラフ コントロールと同じ機能を提供するグラフをレンダリングします。
- `WebGrid`. ページング機能と並べ替え機能を備えたデータ グリッドをレンダリングします。
- `Crypto`. ハッシュ アルゴリズムを使用して、適切に塩分およびハッシュされたパスワードを作成します。
- `WebImage`. イメージをレンダリングします。
- `WebMail`. 電子メール メッセージを送信します。

Razor の詳細については、次のリソースを参照してください。

- [レイザーを紹介するスコット・ガスリーのブログ記事](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [キーワードを紹介するスコット・ガスリーの@modelブログ記事](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [Razorレイアウトを紹介するスコット・ガスリーのブログ記事](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [カミソリ API クイック リファレンス](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [MVC 3 リリースノート](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>複数ビュー エンジンのサポート

MVC 3 の [**ビューの追加**] ダイアログ ボックスASP.NET使用して、操作するビュー エンジンを選択でき、[**新しいプロジェクト**] ダイアログ ボックスでは、プロジェクトの既定のビュー エンジンを指定できます。 Web フォーム ビュー エンジン (ASPX)、Razor、または[Spark](http://sparkviewengine.com/) [、NHaml](https://code.google.com/p/nhaml/)、または[NDjango](http://ndjango.org/)などのオープン ソース ビュー エンジンを選択できます。

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>コントローラの改良点

### <a name="global-action-filters"></a>グローバルアクションフィルタ

アクション メソッドの実行前またはアクション メソッドの実行後に、ロジックを実行する必要がある場合があります。 これをサポートするために、mvc 2ASP.NETアクションフィルターを提供しました。 アクション フィルターは、特定のコントローラー アクション メソッドに事前アクションと事後動作を追加する宣言的手段を提供するカスタム属性です。 ただし、すべてのアクション メソッドに適用される、アクション前または後の動作を指定する必要がある場合もあります。 MVC 3 では、コレクションに追加することでグローバル`GlobalFilters`フィルターを指定できます。 グローバル アクション フィルターの詳細については、次のリソースを参照してください。

- [MVC 3 プレビューに関するスコット・ガスリーのブログ](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [ASP.NET MVC でのフィルタリング](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>新しい "ビューバッグ" プロパティ

MVC 2 コント`ViewData`ローラーは、遅延バインディングのディクショナリ API を使用してビュー テンプレートにデータを渡すことを可能にするプロパティをサポートします。 MVC 3 では、プロパティでやや単純な構文を`ViewBag`使用して、同じ目的を達成することもできます。 たとえば、 を書く`ViewData["Message"]="text"`代わりに、`ViewBag.Message="text"`を記述できます。 `ViewBag`プロパティを使用するために、厳密に型指定されたクラスを定義する必要はありません。 動的プロパティであるため、プロパティを取得または設定するだけで、実行時に動的に解決できます。 内部的には、`ViewBag`プロパティはディクショナリ内の名前と値の`ViewData`ペアとして格納されます。 (注: MVC 3 のプレリリースバージョンでは、`ViewBag`プロパティに名前が`ViewModel`付けられました。

### <a name="new-actionresult-types"></a>新しい "アクション結果" 型

MVC `ActionResult` 3 では、次の型と対応するヘルパー メソッドが新しいか強化されています。

- [を見つけた結果を見つけました](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx)。 クライアントに 404 HTTP ステータス コードを返します。
- [リダイレクト結果](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx)。 ブール型のパラメーターに応じて、一時リダイレクト (HTTP 302 ステータス コード) または永続的なリダイレクト (HTTP 301 ステータス コード) を返します。 この変更に伴い[、Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx)クラスには、永続的なリダイレクトを実行するための 3 `RedirectPermanent``RedirectToRoutePermanent`つのメソッド`RedirectToActionPermanent`があります。 これらのメソッドは、 プロパティ`RedirectResult`が`Permanent`に設定された`true`インスタンスを返します。
- [を返します](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx)。 ユーザー指定の HTTP ステータス コードを返します。

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>JavaScript と Ajax の機能強化

既定では、MVC 3 の Ajax と検証ヘルパーは控えめな JavaScript アプローチを使用します。 控えめな JavaScript は、インライン JavaScript を HTML に挿入することを避けます。 これにより、HTML のサイズが小さくなり、混乱が少なくなり、JavaScript ライブラリのスワップやカスタマイズが容易になります。 MVC 3 の検証ヘルパーも、`jQueryValidate`既定でプラグインを使用します。 MVC 2 の動作が必要な場合は *、web.config*ファイルの設定を使用して、控えめな JavaScript を無効にすることができます。 JavaScript および Ajax の機能強化の詳細については、次のリソースを参照してください。

- [ウィキペディアのサイトで目立たない JavaScript の基本紹介](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [ブラッド・ウィルソンの控えめなJavaScriptポスト](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [ブラッド・ウィルソンの控えめなJavaScript検証ポスト](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [Razor と控えめな JavaScript を使用して MVC 3 アプリケーションを作成](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md)する (ASP.NET サイトのチュートリアル)
- [MVC 3 リリースノート](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>既定で有効になっているクライアント側の検証

以前のバージョンの MVC では、クライアント側の検証`Html.EnableClientValidation`を有効にするために、ビューからメソッドを明示的に呼び出す必要があります。 MVC 3 では、クライアント側の検証が既定で有効になっているため、これは不要になりました。 *(web.config*ファイルの設定を使用して無効にできます。

クライアント側の検証を機能させるには、サイト内の適切な jQuery および jQuery 検証ライブラリを参照する必要があります。 これらのライブラリは、独自のサーバーでホストすることも、Microsoft や Google の CDN などのコンテンツ配信ネットワーク (CDN) から参照することもできます。

### <a name="remote-validator"></a>リモート検証コントロール

ASP.NET MVC 3 は、jQuery 検証プラグインのリモート検証ツールのサポートを利用できるようにする新しい[RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx)クラスをサポートします。 これにより、クライアント側の検証ライブラリは、サーバー側でのみ実行できる検証ロジックを実行するために、サーバーで定義したカスタム メソッドを自動的に呼び出すことができます。

次の例`Remote`では、属性は、クライアント検証がフィールドを検証するためにクラス`UserNameAvailable`に名前`UsersController`を付けたアクションを呼`UserName`び出すことを指定します。

[!code-csharp[Main](mvc3/samples/sample1.cs)]

次の例は、対応するコントローラーを示しています。

[!code-csharp[Main](mvc3/samples/sample2.cs)]

属性の使用方法の詳細については、「方法: MSDN ライブラリ[の MVC でリモート検証ASP.NET実装](https://msdn.microsoft.com/library/gg508808(VS.98).aspx)する」を参照してください。 `Remote`

### <a name="json-binding-support"></a>JSON バインディングのサポート

ASP.NET MVC 3 には、JSON エンコードデータを受信し、アクション メソッド パラメーターにモデルバインドするアクション メソッドを有効にする組み込みの JSON バインド サポートが含まれています。 この機能は、クライアント テンプレートとデータ バインディングを含むシナリオで役立ちます。 (クライアント テンプレートを使用すると、クライアント上で実行されるテンプレートを使用して、単一のデータ項目またはデータ項目のセットを書式設定および表示できます)。MVC 3 を使用すると、JSON データを送受信するサーバー上のアクション メソッドを使用して、クライアント テンプレートを簡単に接続できます。 JSON バインディングのサポートの詳細については、スコット ガスリーの MVC 3[プレビューブログ記事](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)の **「JavaScript と AJAX の改善**」セクションを参照してください。

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>モデル検証の改善

### <a name="dataannotations-metadata-attributes"></a>"データ注釈" メタデータ属性

MVC 3 `DataAnnotations` ASP.NET、 などのメタデータ`DisplayAttribute`属性をサポートしています。

### <a name="validationattribute-class"></a>"検証属性" クラス

この`ValidationAttribute`クラスは、.NET Framework 4 で、検証`IsValid`対象のオブジェクトなど、現在の検証コンテキストに関する詳細情報を提供する新しいオーバーロードをサポートするように改良されました。 これにより、モデルの別のプロパティに基づいて現在の値を検証できる、より豊富なシナリオが可能になります。 たとえば、新しい`CompareAttribute`属性を使用すると、モデルの 2 つのプロパティの値を比較できます。 次の例では、プロパティ`ComparePassword`が有効になるためにフィールド`Password`と一致する必要があります。

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>検証インターフェイス

[IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx)インターフェイスを使用すると、モデル レベルの検証を実行でき、モデル全体の状態に固有の検証エラー メッセージを提供したり、モデル内の 2 つのプロパティ間で検証エラー メッセージを提供したりできます。 MVC 3 では、モデル`IValidatableObject`バインド時にインターフェイスからエラーを取得し、組み込みの HTML フォーム ヘルパーを使用してビュー内の影響を受けるフィールドに自動的にフラグを設定または強調表示します。

[IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx)インターフェイスを使用すると、ASP.NET MVC は、検証コントロールがクライアント検証をサポートしているかどうかを実行時に検出できます。 このインターフェイスは、さまざまな検証フレームワークと統合できるように設計されています。

検証インターフェイスの詳細については[、Scott Guthrie の MVC 3 プレビュー ブログのブログ記事の](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)**モデル検証の改善**セクションを参照してください。 (ただし、ブログの "IValidateObject" への参照は "IValidatableObject" にする必要があることに注意してください。

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>依存性注入の改善

ASP.NET MVC 3 では、依存関係の挿入 (DI) を適用し、依存関係の挿入または制御の反転 (IOC) コンテナーとの統合の優れたサポートを提供します。 DI のサポートは、次の領域で追加されました。

- コントローラ(コントローラファクトリの登録と注入、コントローラの注入)
- ビュー (ビュー エンジンの登録と挿入、ビュー ページへの依存関係の挿入)。
- アクション フィルター (フィルターの検索と挿入)。
- モデルバインダー(登録と注入)。
- モデル検証プロバイダー (登録と挿入)。
- モデル メタデータ プロバイダー (登録と挿入)。
- 値プロバイダー (登録と注入)。

MVC 3 は[、共通サービス ロケーター](https://github.com/unitycontainer/commonservicelocator)ライブラリとそのライブラリの`IServiceLocator`インターフェイスをサポートする DI コンテナーをサポートします。 また、DI フレームワーク`IDependencyResolver`の統合を容易にする新しいインターフェイスもサポートしています。

MVC 3 の DI の詳細については、次のリソースを参照してください。

- [ブラッド・ウィルソンのサービス場所に関する一連のブログ記事](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [MVC 3 リリースノート](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>その他の新機能

### <a name="nuget-integration"></a>NuGet 統合

ASP.NET MVC 3 は、セットアップの一部として NuGet を自動的にインストールして有効にします。 NuGet は、プロジェクトで .NET ライブラリやツールを簡単に検索、インストール、使用できる、無料のオープン ソース パッケージ マネージャーです。 すべての Visual Studio プロジェクトの種類 (web フォームとASP.NET MVC ASP.NET含む) で動作します。

NuGet を使用すると、オープンソースプロジェクト (Moq、NHibernate、Ninject、StructureMap、NUnit、ウィンザー、ライノモック、エルマなどのプロジェクトなど) を維持する開発者は、ライブラリをパッケージ化してオンライン ギャラリーに登録できます。 こういったライブラリを使用する .NET 開発者は、パッケージを見つけて、作業しているプロジェクトにインストールするのは簡単です。

ASP.NET 3 ツールの更新では、プロジェクト テンプレートには、あらかじめインストールされた JavaScript ライブラリが含まれています NuGet パッケージ、NuGet を使用して更新可能です。 エンティティ フレームワーク コード First も、NuGet パッケージとして事前インストールされています。

NuGet の詳細については、[NuGet のドキュメント](https://docs.microsoft.com/nuget/)を参照してください。

### <a name="partial-page-output-caching"></a>部分ページ出力キャッシュ

mvc ASP.NETバージョン 1 以降のフル ページ応答の出力キャッシュをサポートしています。 MVC 3 では、部分ページ出力キャッシュもサポートされており、これにより、応答の領域やフラグメントを簡単にキャッシュできます。 キャッシュの詳細については[、MVC 3 リリース候補の Scott Guthrie のブログ記事](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)の**部分ページ出力キャッシュ**セクションと[MVC 3 リリース ノート](../whitepapers/mvc3-release-notes.md)の**子アクション出力キャッシュ**セクションを参照してください。

### <a name="granular-control-over-request-validation"></a>要求検証の詳細な制御

ASP.NET MVC には、XSS および HTML インジェクション攻撃から自動的に保護するのに役立つ要求検証が組み込まれています。 ただし、ユーザーが HTML コンテンツを投稿できるようにする場合 (たとえば、ブログエントリや CMS コンテンツなど) など、要求の検証を明示的に無効にする必要がある場合があります。 モデルまたはビュー モデルに[AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx)属性を追加して、モデル バインド中にプロパティごとに要求の検証を無効にできるようになりました。 要求の検証の詳細については、次のリソースを参照してください。

- MVC 3 リリース候補に関する[スコット・ガスリーのブログ記事の](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)控**えめな JavaScript と検証**セクション .
- [MVC 3 リリースノート](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>拡張可能な [新しいプロジェクト] ダイアログ ボックス

mvc 3 ASP.NETでは、プロジェクト テンプレート、ビュー エンジン、および単体テスト プロジェクト フレームワークを **[新しいプロジェクト**] ダイアログ ボックスに追加できます。

### <a name="template-scaffolding-improvements"></a>テンプレートスキャフォールディングの改善

ASP.NET MVC 3 スキャフォールディング テンプレートは、モデルの主キー プロパティを識別し、MVC の以前のバージョンよりも適切に処理する優れたジョブを実行します。 (たとえば、スキャフォールディング テンプレートでは、主キーが編集可能なフォーム フィールドとしてスキャフォールディングされないようにするようになりました)。

既定では、作成および編集のスキャフォールディングはヘルパーではなく`Html.EditorFor`ヘルパーを使用する`Html.TextBoxFor`ようになりました。 これにより、[**ビューの追加]** ダイアログ ボックスでビューが生成されるときに、データ注釈属性の形式でモデルのメタデータのサポートが向上します。

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>"Html.LabelFor" および "Html.ラベルフォーモデル" の新しいオーバーロード

ヘルパー メソッドに新しいメソッド オーバーロード`LabelFor`が追加されました。 `LabelForModel` 新しいオーバーロードを使用すると、ラベル テキストを指定またはオーバーライドできます。

### <a name="sessionless-controller-support"></a>セッションレスコントローラのサポート

ASP.NET MVC 3 では、コント ローラー クラスでセッション状態を使用するかどうか、および使用する場合は、セッション状態を読み取り/書き込みまたは読み取り専用にするかどうかを指定できます。 セッションレス コントローラーのサポートについて詳しくは[、MVC 3 リリース ノート](../whitepapers/mvc3-release-notes.md)をご覧ください。

### <a name="new-additionalmetadataattribute-class"></a>新しい "追加メタデータ属性" クラス

[追加メタデータ](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx)属性を使用して、モデル プロパティの`ModelMetadata.AdditionalValues`ディクショナリを設定できます。 たとえば、ビュー モデルに管理者にのみ表示するプロパティがある場合、次の例に示すように、そのプロパティにアポイントを付けることができます。

[!code-csharp[Main](mvc3/samples/sample4.cs)]

このメタデータは、製品ビュー モデルがレンダリングされるときに、すべての表示テンプレートまたはエディター テンプレートで使用できるようになります。 メタデータ情報を解釈するのは、ユーザーの手間です。

### <a name="accountcontroller-improvements"></a>アカウントコントローラの改善

インターネット プロジェクト テンプレートのアカウント コントローラが大幅に改善されました。

### <a name="new-intranet-project-template"></a>新しいイントラネット プロジェクト テンプレート

新しいイントラネット プロジェクト テンプレートが含まれており、Windows 認証を有効にしてアカウント コント ローラーを削除します。
