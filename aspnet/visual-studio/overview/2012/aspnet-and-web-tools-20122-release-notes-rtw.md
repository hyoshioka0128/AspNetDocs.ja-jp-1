---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NETおよび Web ツール 2012.2 リリースノート |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NETおよび Web ツール 2012.2 のリリース ノート。
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675905"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET と Web Tools 2012.2 のリリース ノート

> このドキュメントでは、ASP.NETと Web ツール 2012.2 のリリースについて説明します。 これは、Visual Studio Web ツールとASP.NETの更新プログラムです。

- [インストールに関する注意事項](#_Installation)
- [ドキュメント](#_Documentation)
- [サポート](#_Support)
- [ソフトウェア要件](#_Software_Requirements)
- [ASP.NETおよび Web ツール 2012.2 の新機能](#_New_Features_in)

    - [ツール](#_Tooling)
    - [Web 公開](#_Web_Publishing)
    - [ASP.NET MVC テンプレート](#_Templates)
    - [ASP.NET Web API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET Friendly URL](#_ASP.NET_Friendly_URLs)
- [既知の問題と互換性に関する変更](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>インストールに関する注意事項

ASP.NETと Web ツール 2012.2 の Visual Studio 2012 は[、Web プラットフォーム インストーラー](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)を使用してインストールできます。 これは、必要な Web 用の Visual Studio 2012 または Visual Studio Express 2012 の更新プログラムです。 Visual Studio がインストールされていない場合は、Web 用の Visual Studio エクスプレス 2012 がインストールされます。

また、ASP.NETと Web ツール 2012.2 を手動でインストールすることもできます。 Web 用の Visual Studio 2012 または Visual Studio エクスプレス 2012 がインストールされている必要があります。 次に、次の手順を実行します。 

1. ダウンロード センターから[ASP.NET と Web Framework 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe)インストーラーをダウンロードします。
2. プロンプトが表示されたら、[実行] をクリックします。 ファイルを保存して後で実行することもできます。
3. 更新する Visual Studio のバージョンを確認します。 これを行うには、更新する Visual Studio を起動します。 次に、[ヘルプ] メニュー項目をクリックします。   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. メニュー項目&quot;「Web&quot;用の Visual Studio 2012 について」が表示される場合は[、Web 開発者ツール 2012.2 - Web 用 Visual Studio Express 2012 を](https://go.microsoft.com/fwlink/?LinkID=282228)ダウンロードしてください。 それ以外[の場合は、Web 開発者ツール 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)をダウンロードしてください。
5. プロンプトが表示されたら、[実行] をクリックします。 ファイルを保存して後で実行することもできます。

> [!NOTE]
> ASP.NETと Web ツール 2012.2 リリースには SQL Server データ ツールは含まれていません。 SQL Server と Windows Azure SQL データベースは、オフライン プロジェクトの開発、スキーマ比較、および拡張データベース展開機能など、豊富なデータベース ツールを提供します。 詳細については、または SQL Server データ[https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)ツールをインストールする方法を参照してください。

<a id="_Documentation"></a>
## <a name="documentation"></a>ドキュメント

ASP.NETおよび Web ツール 2012.2 に関するチュートリアルおよびその他の情報はhttps://www.asp.net)、web サイト ( ASP.NET から入手できます。

<a id="_Support"></a>
## <a name="support"></a>サポート

ASP.NETと Web ツール 2012.2 は正式にリリースされ、サポートされています。 通常のサポート チャネルを使用できます。 また、ASP.NETフォーラム ([https://forums.asp.net/](https://forums.asp.net/)) に質問を投稿して、ASP.NET コミュニティのメンバーが非公式なサポートを頻繁に行うことができます。

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>ソフトウェア要件

ASP.NETと Web ツール 2012.2 では、Web 用の Visual Studio 2012 または Visual Studio Express 2012 が必要です。

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>ASP.NETおよび Web ツール 2012.2 の新機能

このセクションでは、ASP.NETと Web Tools 2012.2 リリースで導入された機能について説明します。

<a id="_Tooling"></a>
### <a name="tooling"></a>ツール

- Page Inspector 

    - ページインスペクターが動的にページに追加された項目を対応する JavaScript コードにマップできるように、JavaScript 選択マッピングをサポートします。
    - CSS の更新をリアルタイムで確認する機能。
    - 詳細については、[ページインスペクタの「CSS 自動同期と JavaScript 選択マッピング」を参照してください](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)。
- エディター 

    - コーヒー スクリプト、口ひげ、ハンドル バー、および JsRender の構文の強調表示をサポートします。
    - HTML エディタは、ノックアウト バインディング用の Intellisense を提供します。
    - LESS を使用して動的 CSS の構築を可能にする、少ない編集およびコンパイラのサポート。
    - JSON を .NET クラスとして貼り付けます。 この [貼り付け] コマンドを使用して、Json を C# またはコード ファイルVB.NETに貼り付けると、Visual Studio は JSON から推論される .NET クラスを自動的に生成します。
- モバイル エミュレーターのサポートでは、サードパーティのエミュレーターを VSIX としてインストールできるように、機能拡張フックが追加されます。 インストールされているエミュレーターは F5 ドロップダウンに表示されるため、開発者はさまざまなモバイル デバイスで Web サイトをプレビューできます。 この機能の詳細については、[新しいブラウザースタックと Visual Studio との統合](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)に関する Scott Hanselman のブログエントリを参照してください。

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Web 公開

- Web サイト プロジェクトは、Windows Azure Web サイトへの発行を含め、Web アプリケーション プロジェクトと同じ発行エクスペリエンスを持つようになりました。
- 1 つまたは複数のファイルに対して選択発行&#8211;次の操作を実行できます (Web 配置エンドポイントに発行した後)。 

    - 選択したファイルをパブリッシュします。
    - ローカル ファイルとリモート ファイルの違いを参照してください。
    - リモート ファイルを使用してローカル ファイルを更新するか、ローカル ファイルでリモート ファイルを更新します。

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET MVC テンプレート

- 新しい Facebook Application テンプレートを使用すると、Facebook Canvas アプリケーションを簡単に作成できます。 いくつかの簡単な手順で、ログイン ユーザーのデータを取得してその友達と統合する Facebook アプリケーションを作成できます。 このテンプレートには、認証、アクセス許可、Facebook データへのアクセスなど、Facebook アプリケーションの作成に必要なすべてのパーツを処理する新しいライブラリが含まれています。 Facebookアプリケーションテンプレートの使用の詳細については、を[https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)参照してください。
- 新しい Single Page Application MVC テンプレートを使用すると、ASP.NET Web API を基礎にして、HTML 5、CSS 3、および人気のある Knockout ライブラリや jQuery JavaScript ライブラリを使用して対話型のクライアント側 Web アプリケーションを作成できます。 テンプレートには、RESTful サーバー API を使用する JavaScript HTML5 アプリケーションを構築するための一般的な方法を示す "todo" リスト アプリケーションが含まれています。 詳細については、を参照[https://www.asp.net/single-page-application](../../../single-page-application/index.md)してください。
- これで、MVC の新しいプロジェクト] ダイアログ に新しいテンプレートを追加する VSIX ASP.NET作成できます。 詳細はこちら:[https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- MVC 4 のバグの回避策が含まれている新しい 'FixedDisplayModes' NuGet パッケージを含むように、MVC の表示モード パッケージ&#8211; MVC プロジェクト テンプレートが更新されました。 パッケージに含まれる修正プログラムの詳細については、MVC チームのこのブログ記事[https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)( ) を参照してください。

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET Web API は、次のような新機能によって強化されました。

- ASP.NET Web API OData
- ウェブ API トレースASP.NET
- Web API ヘルプ ページASP.NET

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

Web API OData ASP.NET、あらゆるデータソースに対して豊富なビジネスロジックを使用してODataエンドポイントを構築する必要がある柔軟性を提供します。 Web API OData ASP.NET使用して、公開する OData セマンティクスの量を制御します。 ASP.NET Web API OData は、ASP.NET MVC 4 プロジェクト テンプレートに含[http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)まれており、NuGet ( ) からも使用できます。

ASP.NET Web API OData は現在、次の機能をサポートしています。

- [クエリ可能] 属性を適用して、OData クエリセマンティクスを有効にします。
- OData クエリを簡単に検証し、サポートされているクエリ オプション、演算子、関数のセットを制限します。
- パラメーターを直接 ODataQueryOptions にバインドして、クエリの抽象構文ツリー表現を取得し、その結果、検証して IQueryable または IEnumerable に適用できます。
- [Queryable] 属性に結果制限を指定して、サービス駆動型ページングと次のページリンク生成を有効にします。
- $inlinecountを使用して、一致するリソースの合計数のインラインカウントを要求します。
- NULL 伝播を制御します。
- $filter内の任意/すべての演算子。
- エンティティ データ モデルを規則によって推論するか、または Entity Framework コードファーストと同様の方法でモデルを明示的にカスタマイズします。
- エンティティ セットを公開するには、エンティティ セットから派生します。
- ナビゲーション プロパティの公開、リンクの操作、および OData アクションの実装を行うための、簡単でカスタマイズ可能な規則。
- MapODataRoute 拡張メソッドを使用したルーティングの簡略化。
- 複数の EDM モデルを公開することでバージョン管理をサポートします。
- Web API 用のクライアント (.NET、Windows Phone、Windows ストアなど) を生成できるように、サービス ドキュメントと$metadataを公開します。
- OData アトム、JSON、および JSON の詳細形式のサポート。
- エンティティの作成、更新、一部の更新 (PATCH) および削除
- エンティティ間のリレーションシップを照会および操作します。
- ルートに接続するリレーションシップ リンクを作成します。
- 複合型。
- エンティティ型の継承。
- コレクションのプロパティ。
- 列挙 型。
- OData アクション。
- WCF データ サービスと同じ基盤、すなわち ODataLib[http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)( ) に基づいて構築されます。

Web API OData の詳細については[https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)、ASP.NETのを参照してください。

#### <a name="aspnet-web-api-tracing"></a>ウェブ API トレースASP.NET

web API トレースASP.NET、Web API からのトレース データを .NET トレースと統合します。 Web API プロジェクト テンプレートで既定で有効になりました。 Web API のトレース データは出力ウィンドウに送信され、IntelliTrace を通じて使用できるようになります。 ASP.NET Web API トレースを使用すると[、Windows](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)Azure 診断との統合を通じて、Windows Azure でホストされている Web API に関する情報をトレースできます。 また、ASP.NETの Web API トレースの NuGet パッケージ ( )[http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)を使用して、任意のアプリケーションで Web API トレースASP.NETインストールおよび有効化できます。

Web API トレースの構成と使用の詳細については、ASP.NET Web API トレースの参照を参照してください[https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)。

#### <a name="aspnet-web-api-help-page"></a>Web API ヘルプ ページASP.NET

Web API のASP.NETヘルプ ページが、Web API プロジェクト テンプレートに既定で含まれるようになりました。 web API のASP.NETヘルプ ページでは、HTTP エンドポイント、サポートされている HTTP メソッド、パラメーター、要求と応答メッセージのペイロードの例など、Web API のドキュメントが自動的に生成されます。 ドキュメントは、コード内のコメントから自動的に取得されます。 ASP.NET Web API ヘルプ ページの NuGet パッケージ ( )[http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)を使用して、ASP.NET Web API ヘルプ ページを任意のアプリケーションに追加することもできます。

ASP.NET Web API ヘルプ ページの設定とカスタマイズの詳細については[https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)、 を参照してください。

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

signalR ASP.NET、利用可能な場合はWebSocketsを使用して、ASP.NETアプリケーションにリアルタイムのWeb機能を追加することが簡単になり、そうでないときに自動的に他のテクニックにフォールバックします。

ASP.NET SignalR の使用の詳細[https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)については、 を参照してください。

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET Friendly URL

FriendlyURL をASP.NETすると、Web フォーム開発者が (.aspx 拡張子を除く) よりクリーンな URL を生成することが非常に簡単になります。 構成はほとんど必要ないか、またはまったく必要とされず、既存のASP.NET v4.0 アプリケーションで使用できます。 FriendlyURL 機能を使用すると、デスクトップビューとモバイルビューの切り替えをサポートすることで、開発者がアプリケーションにモバイルサポートを追加しやすくなります。

ASP.NET フレンドリ URL のインストールと使用の[http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)詳細については、「」を参照してください。

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>既知の問題と互換性に関する変更

このセクションでは、ASP.NETおよび Web Tools 2012.2 リリースで行われている既知の問題と、互換性に関する変更点について説明します。

### <a name="installation-issues"></a>インストールに関する問題

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>Visual Studio 2012 のインストールが順次

ASP.NETと Web ツール 2012.2 をインストールした後に Visual Studio 2012 の追加 SKU をインストールするには、修復操作が必要になります。 次の例について考えてみます。

1. Web 用の Visual Studio 2012 エクスプレスのインストール
2. ASP.NETおよび Web ツールのインストール 2012.2
3. Visual Studio 2012 プロフェッショナル、プレミアムまたは究極のインストール

手順 2 は、Web 用の Express の更新プログラムをインストールする場合にのみ発生します。 手順 3 でインストールされた追加の SKU に更新プログラムが含まれていることを確認するには、最後にインストールした SKU の更新プログラムをインストールするには、ASP.NETと Web Tools 2012.2 を修復する必要があります。 これは、ステップ 1 と 3 の SKU が逆の場合にも適用されます。

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Visual Studio が開いているときにマイクロソフト ASP.NETと Web ツール 2012.2 をインストールします。

マイクロソフト ASP.NETと Web ツール 2012.2 のインストール中に VS が開かれている場合、Visual Studio は、悪い状態に終わる可能性があります。 インストールを続行する前に、Visual Studio のすべてのインスタンスを閉じておく方法をお勧めします。

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>インストールの途中でASP.NETと Web ツール 2012.2 のセットアップをキャンセルする

インストールの途中でASP.NETと Web ツール 2012.2 のセットアップをキャンセルすると、Visual Studio の状態が悪いままになります。 この問題に対処するには、次の手順を実行します。 

- [プログラムの追加と削除] に移動します
- 存在する場合は、マイクロソフト ASP.NETと Web ツール 2012.2 をアンインストールします。
- マイクロソフトのASP.NETと Web ツール 2012.2 を再インストールします。

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>ASP.NETと Web ツール 2012.2 をアンインストールした後、mvc 4 テンプレートと Razor v2 Web サイト テンプレートが見つからないASP.NET

ASP.NETと Web ツール 2012.2 をアンインストールすると、Visual Studio 2012 から ASP.NET MVC 4 と Razor v2 Web サイト テンプレートもすべてアンインストールされます。

回避策は、MVC 4 と Razor v2 の Web サイト テンプレートASP.NET再インストールする Visual Studio 2012 のインストールを修復することです。

### <a name="tooling-issues"></a>ツールの問題

#### <a name="nuget-error-reported-during-project-creation"></a>プロジェクトの作成中に報告される NuGet エラー

ASP.NETと Web ツール 2012.2 をインストールした後、MVC 4 プロジェクトを作成するときに次のエラーが表示される場合があります。

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

ASP.NETと Web ツール 2012.2 は NuGet 2.1 を出荷し、Visual Studio 2012 の拡張機能をアップグレードします。 場合によっては、VSIX インストーラーが VSIX を正しく更新できない場合があります。 この問題に対処するには、次の手順を実行します。

1. 管理者として Visual Studio 2012 を起動します。
2. ツール -&gt;拡張機能と更新プログラムに移動し、NuGet をアンインストールします。
3. Visual Studio を閉じます。
4. ASP.NETと Web ツール 2012.2 のインストール フォルダーに移動します。

    1. ビジュアル スタジオ 2012の場合:**プログラム ファイル\マイクロソフト ASP.NET\ASP.NET Web スタック\Visual Studio 2012**
    2. Web 用の Visual Studio 2012 エクスプレスの場合:**プログラム ファイル\マイクロソフト ASP.NET\ASP.NET Web スタック\Visual Studio エクスプレス 2012 for Web**
5. NuGet を再インストールするには、NuGet.Tools.vsix をダブルクリックします。

### <a name="web-api-issues"></a>ウェブ API の問題

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>$filterリテラルおよび DateTime リテラルの構文解析の問題

OData URI パーサーは、部分的な日時リテラルを正しく解析できません。 たとえば、$filter=開始 eq datetime'2012-12-31T12:00' は正しく解析できません。 回避策としては、リテラル全体$filter=開始 eq datetime'2012-12-31T12:00:00'を使用します。

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData では、大文字と小文字を区別しないプロパティ名はサポートされません。

OData は、OData クエリと odata パスで大文字と小文字を区別しないプロパティ名をサポートしていません。 ワークアイテムを参照してください:

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

Javascript クライアント側とサーバー側でユーザーの大文字と小文字が異なる場合、おそらくこの問題が発生します。 この問題は odata プロトコルの仕様です。 ただし、多くのユーザーがこの問題を報告します。 この問題を回避するには、ユーザーが URL でケースを修正する必要があります。

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>既定の OData ルーティング規則では、ナビゲーション プロパティでの POST/PUT はサポートされません。

既定の OData ルーティング規則では、ナビゲーション プロパティでの POST/PUT はサポートされません。 ワークアイテム[http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)を参照してください。 既定の規則では、この一般的に使用される規則が欠けています。

この問題を回避するには、ユーザーは新しいルーティング規則を拡張してサポートする必要があります。

### <a name="facebook-template-issues"></a>フェイスブックテンプレートの問題

#### <a name="facebook-application-template-only-works-using-net-45"></a>Facebookアプリケーションテンプレートは.NET 4.5のみを使用して動作します

[新しいプロジェクト] ダイアログのフレームワーク ドロップダウン リストで [.NET 4.5] を選択して、ASP.NETの MVC 4 で Facebook アプリケーション テンプレートを表示する必要があります。

#### <a name="real-time-update-controller"></a>リアルタイムアップデートコントローラ

Facebookアプリケーションテンプレートを使用すると、ユーザーは簡単にFacebookからのリアルタイムの更新を処理するためのWeb APIコントローラを作成することができます。 開発マシンが NAT の背後にある場合、コントローラはネットワーク設定が必要でないと動作しない可能性があります。 詳細はこちらをご覧ください。[http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>クエリ文字列の値が Facebook OAuth パラメーターと競合しています

次のフィールドは、Facebook OAuth ダイアログのコールバック URL と競合しています。 コード、エラー、エラーの\_説明、エラー\_の理由の名前を持つ独自のクエリ文字列値を追加しないでください。

#### <a name="using-page-inspector-with-facebook-template"></a>Facebookテンプレートでのページインスペクターの使用

Facebook アプリケーションのデバッグ中に、Visual Studio 2012 のページインスペクター機能を使用することはできません。 ページインスペクタは現在 iframe をサポートしていません。

### <a name="single-page-application-template-issues"></a>単一ページアプリケーションテンプレートの問題

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>JQuery 1.9/ノックアウト 2.2.1 更新プログラムでは、既定の MVC SPA プロジェクトを実行すると、新しい todo 項目編集入力フォーカス イベントが正しく処理されません。

JQuery 1.9/Knockout 2.2.1 アップデートでは、デフォルトの MVC SPA プロジェクトを実行すると、新しい todo 項目編集は、新しい todo 項目を todo リストに入力した後、新しい todo 項目編集ボックスにフォーカスし直す必要がなくなりました。

を回避するには[http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)、 を参照し、次のサンプル コードと同様の修正を行います。

ファイル todo.model.js  
 関数 todolist(データ)、次を追加します。  
 **選択された = ko.observable(偽)。**

関数 todoList.prototype.addTodo, 次の黒いテキストを追加します。  
 **選択された(真)。**  
 自己.newTodoタイトル(&quot;&quot;);

ファイル index.cshtml.  
 &lt;フォームデータバインド=&quot;送信: addTodo&quot;&gt;  
 &lt;入力クラス=&quot;addTodo&quot; &quot;タイプ&quot;= テキスト&quot;データバインド= 値: newTodoTitle, プレースホルダ: 'ここに追加するタイプ', blurOnEnter: true, **hasfocus: isfocus: isSelected,** イベント: { ブラー: addTodo }&quot; /&gt;  
 &lt;/フォーム&gt;
