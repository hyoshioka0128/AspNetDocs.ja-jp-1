---
uid: visual-studio/overview/2013/release-notes
title: Visual Studio 2013 のリリース ノートのASP.NETと Web ツール |マイクロソフトドキュメント
author: rick-anderson
description: このドキュメントでは、Visual Studio 2013 のASP.NETと Web ツールのリリースについて説明します。
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 4494b4acdd30384e1def89b7fff9bad30933e38e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543497"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>Visual Studio 2013 の ASP.NET と Web ツールのリリース ノート

[マイクロソフト](https://github.com/microsoft)

> このドキュメントでは、Visual Studio 2013 のASP.NETと Web ツールのリリースについて説明します。

## <a name="contents"></a>内容

- [インストールに関する注意事項](#TOC1)
- [ドキュメント](#TOC2)
- [ソフトウェア要件](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>visual Studio 2013 のASP.NETおよび Web ツールの新機能

- [1ASP.NET](#TOC6)
- [新しい Web プロジェクト エクスペリエンス](#newproj)
- [ASP.NET足場](#scaffold)
- [ブラウザー リンク](#browser-link)
- [ビジュアル スタジオ Web エディターの機能強化](#web-editor)
- [Azure アプリ サービス Web アプリのサポート](#waws)
- [Web 発行の機能強化](#publish)
- [NuGet 2.7](#nuget)
- [ASP.NET Web Forms](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [ASP.NET Web API 2](#TOC11)
- [ASP.NET SignalR](#TOC13)
- [ASP.NET Identity](#TOC8)
- [Microsoft OWIN コンポーネント](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NETカミソリ3](#TOC14)
- [ASP.NETアプリの中断](#TOC15)
- [既知の問題と互換性に関する変更](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>インストールに関する注意事項

Visual Studio 2013 のASP.NETと Web ツールはメイン インストーラーにバンドルされており、[ここで](https://www.asp.net/downloads)ダウンロードできます。

<a id="TOC2"></a>
## <a name="documentation"></a>ドキュメント

チュートリアルとその他の Visual Studio 2013 のASP.NETと Web ツールに関する情報は[、ASP.NET Web サイト](https://www.asp.net/)から入手できます。

<a id="TOC4"></a>
## <a name="software-requirements"></a>ソフトウェア要件

ASP.NETと Web ツールには、Visual Studio 2013 が必要です。

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>visual Studio 2013 のASP.NETおよび Web ツールの新機能

以下のセクションでは、リリースで導入された機能について説明します。

<a id="TOC6"></a>
## <a name="one-aspnet"></a>1ASP.NET

Visual Studio 2013 のリリースでは、ASP.NET テクノロジを使用するエクスペリエンスを統一する一歩を踏み出しました。 たとえば、MVC を使用してプロジェクトを開始し、後で Web フォーム ページをプロジェクトに簡単に追加したり、Web フォーム プロジェクトの Web API をスキャフォールディングしたりできます。 ASP.NETの一つは、開発者がASP.NETで好きなことをしやすくすることです。 どのテクノロジーを選択しても、信頼できる基盤となる One ASP.NETのフレームワークを構築しているという自信を持つことができます。

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>新しい Web プロジェクト エクスペリエンス

Visual Studio 2013 で新しい Web プロジェクトを作成するエクスペリエンスが強化されました。 [**新しいASP.NET Web プロジェクト**] ダイアログで、必要なプロジェクトの種類を選択し、任意のテクノロジ (Web フォーム、MVC、Web API) の組み合わせを構成し、認証オプションを構成し、単体テスト プロジェクトを追加できます。

![新しいASP.NET プロジェクト](release-notes/_static/image1.png)

新しいダイアログでは、多くのテンプレートのデフォルトの認証オプションを変更できます。 たとえば、Web フォーム プロジェクトASP.NET作成する場合は、次のオプションのいずれかを選択できます。

- [認証なし]
- 個人ユーザー アカウント (ASP.NET メンバーシップまたはソーシャル プロバイダーのログイン)
- 組織アカウント (インターネット アプリケーションの Active Directory)
- Windows 認証 (イントラネット アプリケーションのアクティブ ディレクトリ)

![認証オプション](release-notes/_static/image2.png)

Web プロジェクトを作成するための新しいプロセスの詳細については[、「Visual Studio 2013 でASP.NET Web プロジェクトを作成](creating-web-projects-in-visual-studio.md)する」を参照してください。 新しい認証オプションの詳細については、このドキュメントの[「ASP.NET ID」](#TOC8)を参照してください。

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET足場

ASP.NETスキャフォールディングは、ASP.NET Web アプリケーション用のコード生成フレームワークです。 これにより、データ モデルとやり取りする定型コードをプロジェクトに簡単に追加できます。

以前のバージョンの Visual Studio では、スキャフォールディングは MVC プロジェクトASP.NETに限定されていました。 Visual Studio 2013 では、Web フォームを含む任意のASP.NET プロジェクトにスキャフォールディングを使用できるようになりました。 Visual Studio 2013 は、Web フォーム プロジェクトのページの生成をサポートしていませんが、プロジェクトに MVC 依存関係を追加することで Web フォームでスキャフォールディングを使用できます。 Web フォームのページ生成のサポートは、今後の更新プログラムで追加される予定です。

スキャフォールディングを使用する場合、必要なすべての依存関係がプロジェクトにインストールされていることを確認します。 たとえば、ASP.NET Web フォーム プロジェクトを使用して Web API コント ローラーを追加するのにはスキャフォールディングを使用する場合は、必要な NuGet パッケージと参照が自動的にプロジェクトに追加されます。

Mvc スキャフォールディングを Web フォーム プロジェクトに追加するには、**新しいスキャフォールディング項目**を追加し、ダイアログ ウィンドウで**MVC 5 の依存関係**を選択します。 スキャフォールディング MVC には 2 つのオプションがあります。最小限とフル。 [最小] を選択した場合は、ASP.NET MVC の NuGet パッケージと参照のみがプロジェクトに追加されます。 [完全] オプションを選択すると、MVC プロジェクトに必要なコンテンツ ファイルと同様に、最小限の依存関係が追加されます。

スキャフォールディング非同期コントローラーのサポートでは、Entity Framework 6 の新しい非同期機能が使用されます。

詳細およびチュートリアルについては、「ASP.NET[スキャフォールディングの概要](aspnet-scaffolding-overview.md)」を参照してください。

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>ブラウザー リンク – ブラウザーと Visual Studio の間の SignalR チャネル

新しい[ブラウザー リンク](using-browser-link.md)機能を使用すると、複数のブラウザーを Visual Studio に接続し、ツール バーのボタンをクリックしてすべてのブラウザーを更新できます。 モバイル エミュレーターを含む複数のブラウザーを開発サイトに接続し、[更新] をクリックすると、すべてのブラウザーを同時に更新できます。 また、開発者がブラウザリンク拡張機能を記述できるように API も公開します。

![](release-notes/_static/image3.png)

開発者がブラウザー リンク API を利用できるようにすることで、Visual Studio と接続されているブラウザーの境界を越える非常に高度なシナリオを作成できます。 Web Essentials は、この API を利用して、Visual Studio とブラウザーの開発者ツール、リモート制御モバイル エミュレーターなどの間に統合されたエクスペリエンスを作成します。

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>ビジュアル スタジオ Web エディターの機能強化

Visual Studio 2013 には、Web アプリケーションの Razor ファイルと HTML ファイル用の新しい HTML エディターが含まれています。 新しい HTML エディターは、HTML5 に基づく単一の統一されたスキーマを提供します。 自動ブレース補完、jQuery UIとAngularJS属性IntelliSense、属性IntelliSenseグループ、IDとクラス名Intellisense、および優れたパフォーマンス、フォーマット、スマートタグなどのその他の改善があります。

次のスクリーンショットは、HTML エディターでブートストラップ属性 IntelliSense を使用する方法を示しています。

![HTML エディタでのインテリセンス](release-notes/_static/image4.png)

また、2013 年には、コーヒー スクリプトと LESS の両方のエディターが組み込まれています。 LESSエディタには、CSSエディタからのすべてのクールな機能が付属しており、チェーン内のすべてのLESSドキュメント全体の変数とミキシンのための特定のIntellisenseがあります@import。

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Azure アプリ サービス Web アプリのサポート

.NET 2.2 用 Azure SDK を使用した Visual Studio 2013 では、**サーバー エクスプローラー**を使用してリモート Web アプリと直接対話できます。 Azure アカウントへのサインイン、新しい Web アプリの作成、アプリの構成、リアルタイム ログの表示などを行うことができます。 SDK 2.2 がリリースされた直後に、Azure でリモートでデバッグ モードで実行できるようになります。 Azure アプリ サービス Web アプリの新機能のほとんどは、.NET 用 Azure SDK の最新リリースをインストールするときに Visual Studio 2012 でも動作します。

詳細については、次のリソースを参照してください。

- [Azure アプリ サービスでASP.NET Web アプリを作成する](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [Visual Studio を使用した Azure App Service のトラブルシューティング](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>Web 発行の機能強化

Visual Studio 2013 には、新しい Web 発行機能と強化された Web 発行機能が含まれています。 いくつかを次に示します。

- [Web.config ファイルの暗号化](https://go.microsoft.com/fwlink/?LinkId=325529)を簡単に自動化する 。 (このリンクと、MSDN のドキュメントへのリンクを次の 2 つ示しますが、10/17 日の遅い時間まで利用できない場合があります)。
- [展開時にアプリケーションをオフラインにする作業を簡単に自動化](https://go.microsoft.com/fwlink/?LinkId=325530)する :
- サーバーにコピーするファイルを決定するために[、最後に変更された日付ではなくファイル チェックサムを使用](https://go.microsoft.com/fwlink/?LinkId=325531)するように Web 配置を構成します。
- FTP またはファイル システムの発行方法を使用している場合や、Web 配置を使用している場合は、選択した個々のファイル (Web.config を含む) をすばやく発行します。

web 展開ASP.NET詳細については、 [ASP.NET サイトを](https://go.microsoft.com/fwlink/?LinkId=322027)参照してください。

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 には[、NuGet 2.7 リリース ノート](http://docs.nuget.org/docs/release-notes/nuget-2.7)で詳細に説明されている新機能の豊富なセットが含まれています。

このバージョンの NuGet では、パッケージをダウンロードするために NuGet のパッケージ復元機能に明示的な同意を提供する必要もなくなります。 同意 (および NuGet の基本設定ダイアログの関連するチェック ボックス) は、NuGet をインストールすることで付与されます。 今すぐパッケージの復元は、デフォルトで動作します。

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

### <a name="one-aspnet"></a>1ASP.NET

Web フォーム プロジェクト テンプレートは、新しい One ASP.NET エクスペリエンスとシームレスに統合されます。 Web フォーム プロジェクトに MVC および Web API サポートを追加したり、1 ASP.NET プロジェクト作成ウィザードを使用して認証を構成したりできます。 詳細については、「 [Visual Studio 2013 での ASP.NET Web プロジェクトの作成](creating-web-projects-in-visual-studio.md)」を参照してください。

### <a name="aspnet-identity"></a>ASP.NET Identity

Web フォーム プロジェクト テンプレートは、新しい ASP.NET ID フレームワークをサポートします。 さらに、テンプレートは Web フォーム イントラネット プロジェクトの作成をサポートするようになりました。 詳細については **、「Visual Studio 2013 での ASP.NET Web プロジェクトの作成」の**[認証方法](creating-web-projects-in-visual-studio.md#auth)を参照してください。

### <a name="bootstrap"></a>ブートストラップ

Web フォーム テンプレートでは[、Bootstrap](http://twitter.github.io/bootstrap/)を使用して、簡単にカスタマイズできる、洗練された応答性の高い外観を提供します。 詳細については、「 [Visual Studio 2013 Web プロジェクト テンプレートのブートストラップ](creating-web-projects-in-visual-studio.md#bootstrap)」を参照してください。

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>1ASP.NET

Web MVC プロジェクト テンプレートは、新しい One ASP.NET エクスペリエンスとシームレスに統合されます。 MVC プロジェクトをカスタマイズし、One ASP.NET プロジェクト作成ウィザードを使用して認証を構成できます。 ASP.NET MVC 5 の入門チュートリアルは[、MVC 5 の概要](../../../mvc/overview/getting-started/introduction/getting-started.md)ASP.NET で見つけることができます。

MVC 4 プロジェクトを MVC 5 にアップグレードする[方法については、「MVC 4 と Web API プロジェクトASP.NETを MVC 5 と Web API 2 ASP.NETにアップグレードする方法](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)」を参照してください。

### <a name="aspnet-identity"></a>ASP.NET Identity

認証と ID 管理に ASP.NET ID を使用するように、MVC プロジェクト テンプレートが更新されました。 FacebookとGoogleの認証と新しいメンバーシップAPIをフィーチャーしたチュートリアルは[、FacebookとGoogle OAuth2とOpenIDサインオンでASP.NETMVC 5アプリを作成し](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)、[認証とSQL DBを使用してASP.NETMVCアプリを作成し、Azureアプリサービスに展開するにあります](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)。

### <a name="bootstrap"></a>ブートストラップ

MVC プロジェクト テンプレートは[、ブートストラップ](http://getbootstrap.com/)を使用して、簡単にカスタマイズできる、洗練された応答性の高い外観と操作性を提供するように更新されました。 詳細については、「 [Visual Studio 2013 Web プロジェクト テンプレートのブートストラップ](creating-web-projects-in-visual-studio.md#bootstrap)」を参照してください。

### <a name="authentication-filters"></a>認証フィルタ

認証フィルターは、ASP.NET ASP.NET MVC パイプラインで承認フィルターの前に実行され、すべてのコント ローラーのアクションごとの、コント ローラーごと、またはグローバルに認証ロジックを指定できるようにする MVC の新しい種類のフィルターです。 認証フィルターは、要求内の資格情報を処理し、対応するプリンシパルを提供します。 認証フィルタは、承認されていない要求に応じて認証チャレンジを追加することもできます。

### <a name="filter-overrides"></a>フィルタの上書き

オーバーライド フィルターを指定して、特定のアクション メソッドまたはコントローラーに適用するフィルターをオーバーライドできるようになりました。 オーバーライド フィルターは、特定のスコープ (アクションまたはコントローラー) に対して実行してはならないフィルターの種類のセットを指定します。 これにより、グローバルに適用されるが、特定のアクションまたはコントローラに適用から特定のグローバル フィルタを除外するフィルタを設定できます。

### <a name="attribute-routing"></a>属性ルーティング

ASP.NET MVC は、 の著者である Tim McCall の投稿により[http://attributerouting.net](http://attributerouting.net)、属性ルーティングをサポートするようになりました。 属性ルーティングを使用すると、アクションとコントローラにアコードを付けてルートを指定できます。

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>ASP.NET Web API 2

### <a name="attribute-routing"></a>属性ルーティング

ASP.NET Web API は、 の著者である Tim McCall の投稿[http://attributerouting.net](http://attributerouting.net)により、属性ルーティングをサポートするようになりました。 属性ルーティングを使用すると、次のようにアクションとコントローラにアコードを付けて Web API ルートを指定できます。

[!code-csharp[Main](release-notes/samples/sample1.cs)]

属性ルーティングを使用すると、Web API の URI をより詳細に制御できます。 たとえば、単一の API コントローラを使用して、リソース階層を簡単に定義できます。

[!code-csharp[Main](release-notes/samples/sample2.cs)]

属性ルーティングでは、オプションのパラメータ、デフォルト値、およびルート制約を指定するための便利な構文も提供します。

[!code-csharp[Main](release-notes/samples/sample3.cs)]

属性ルーティングの詳細については[、「Web API 2 での属性ルーティング](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)」を参照してください。

### <a name="oauth-20"></a>OAuth 2.0

Web API および単一ページアプリケーションのプロジェクトテンプレートで、OAuth 2.0 を使用した承認がサポートされるようになりました。 OAuth 2.0 は、保護されたリソースへのクライアント アクセスを承認するためのフレームワークです。 これは、ブラウザやモバイルデバイスを含むクライアントの様々なのために動作します。

OAuth 2.0 のサポートは、ベアラー認証と承認サーバーの役割の実装のために Microsoft OWIN コンポーネントによって提供される新しいセキュリティ ミドルウェアに基づいています。 または、Windows Server 2012 R2 の Azure アクティブ ディレクトリや ADFS などの組織の承認サーバーを使用して、クライアントを承認することもできます。

### <a name="odata-improvements"></a>OData の機能強化

**$select、$expand、$batch、$valueのサポート**

ASP.NET Web API OData は、$select、$expand、および$valueを完全にサポートできるようになりました。 また、要求のバッチ処理や変更セットの処理に$batchを使用することもできます。

$selectおよび$expandオプションを使用すると、OData エンドポイントから返されるデータの形状を変更できます。 詳細については、「 [Web API OData での$selectと$expandサポートの概要](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)」を参照してください。

**拡張性の向上**

OData フォーマッタは拡張可能になりました。 Atom エントリ メタデータの追加、名前付きストリームおよびメディア リンク エントリのサポート、インスタンスの注釈の追加、およびリンクの生成方法のカスタマイズを行うことができます。

**タイプレスサポート**

エンティティ型に対して CLR 型を定義しなくても、OData サービスを構築できるようになりました。 代わりに、OData コントローラは、シリアル化/逆シリアル化する OData フォーマッタである**IEdmObject**のインスタンスを取得または返すことができます。

**既存のモデルを再利用する**

既存のエンティティ データ モデル (EDM) を既に使用している場合は、新しいモデルを構築する代わりに、直接再利用できるようになりました。 たとえば、エンティティ フレームワークを使用している場合は、EF が作成する EDM を使用できます。

### <a name="request-batching"></a>要求バッチ処理

要求バッチ処理は、複数の操作を 1 つの HTTP POST 要求に結合して、ネットワーク トラフィックを削減し、よりスムーズで、より少ないユーザー インターフェイスを提供します。 ASP.NET Web API では、要求バッチ処理のいくつかの戦略がサポートされるようになりました。

- OData サービスの$batch エンドポイントを使用します。
- 複数の要求を 1 つの MIME マルチパート要求にパッケージ化します。
- カスタム バッチ形式を使用します。

要求バッチ処理を有効にするには、バッチ処理ハンドラーを含むルートを Web API 構成に追加するだけです。

[!code-csharp[Main](release-notes/samples/sample4.cs)]

また、要求または実行を順次に実行するか、または任意の順序で実行するかを制御することもできます。

### <a name="portable-aspnet-web-api-client"></a>ポータブル ASP.NET Web API クライアント

ASP.NET Web API クライアントを使用して、Windows ストア アプリケーションと Windows Phone 8 アプリケーションで動作するポータブル クラス ライブラリを作成できるようになりました。 クライアントとサーバー間で共有できるポータブル フォーマッタを作成することもできます。

### <a name="improved-testability"></a>テストの容易性の向上

Web API 2 を使用すると、API コントローラーの単体テストが大幅に容易になります。 要求メッセージと構成を使用して API コントローラーをインスタンス化し、テストするアクション メソッドを呼び出すだけです。 リンク生成を実行するアクション メソッドの**UrlHelper**クラスを簡単にモックできます。

### <a name="ihttpactionresult"></a>を返す

これで、Web API アクション メソッドの結果をカプセル化するために IHttpActionResult を実装できます。 Web API アクション メソッドから返された IHttpActionResult は、結果として生成される応答メッセージを生成するために、ASP.NET Web API ランタイムによって実行されます。 Web API の実装の単体テストを簡略化するために、任意の Web API アクションから IHttpActionResult を返すことができます。 便宜上、特定のステータス コード、書式設定されたコンテンツ、またはコンテンツネゴシエーションされた応答を返す結果を含む、多数の IHttpActionResult 実装が提供されています。

### <a name="httprequestcontext"></a>HttpRequestContext

新しい**HttpRequestContext**は、要求に関連付けられているが、要求からすぐには使用できない状態を追跡します。 たとえば **、HttpRequestContext**を使用して、ルート データ、要求に関連付けられているプリンシパル、クライアント証明書 **、UrlHelper、** および仮想パス ルートを取得できます。 単体テスト用に**HttpRequestContext**を簡単に作成できます。

要求のプリンシパルは **、Thread.CurrentPrincipal**に依存するのではなく、要求と共にフローされるため、要求の有効期間中、Web API パイプライン内でプリンシパルを使用できるようになりました。

### <a name="cors"></a>CORS

ブロックアレンからのもう一つの大きな貢献のおかげで、ASP.NET完全にクロスオリジンリクエスト共有(CORS)をサポートしています。

ブラウザーのセキュリティ機能により、Web ページでは AJAX 要求を別のドメインに送信することはできません。 [CORS](http://www.w3.org/TR/cors/)は、サーバーが同じ発信元ポリシーを緩和できるようにする W3C 標準です。 CORS を使用することで、サーバーが一部のクロス オリジン要求を、その他の要求を拒否しながら、明示的に許可することができます。

Web API 2 では、プリフライト要求の自動処理を含む CORS がサポートされるようになりました。 詳細については、 [ASP.NET Web API でのクロスオリジン要求の有効化](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)に関する文書を参照してください。

### <a name="authentication-filters"></a>認証フィルタ

認証フィルターは、ASP.NET Web API パイプラインで承認フィルターの前に実行される web API ASP.NET新しい種類のフィルターであり、すべてのコントローラーに対してアクションごと、コントローラーごと、またはグローバルに認証ロジックを指定できます。 認証フィルターは、要求内の資格情報を処理し、対応するプリンシパルを提供します。 認証フィルタは、承認されていない要求に応じて認証チャレンジを追加することもできます。

### <a name="filter-overrides"></a>フィルタの上書き

オーバーライド フィルターを指定して、指定したアクション メソッドまたはコントローラーに適用するフィルターをオーバーライドできるようになりました。 オーバーライド フィルターは、特定のスコープ (アクションまたはコントローラー) に対して実行してはならないフィルターの種類のセットを指定します。 これにより、グローバルフィルタを追加できますが、特定のアクションやコントローラから除外することができます。

### <a name="owin-integration"></a>OWIN 統合

ASP.NET Web API は OWIN を完全にサポートし、OWIN 対応のホストで実行できるようになりました。 OWIN 認証システムとの統合を提供する**ホスト認証フィルター**も含まれています。

OWIN 統合を使用すると、SignalR などの他の OWIN ミドルウェアと共に、独自のプロセスで Web API を自己ホストできます。 詳細については、「 [OWIN を使用して Web API を自己ホストする 」ASP.NET](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)参照してください。

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET信号機 2.0

次のセクションでは、SignalR 2.0 の機能について説明します。

- [OWIN に構築](#builtonowin)
- [マップハブとマップコネクションがマップシグナルです](#MapSignalR)
- [クロスドメインサポート](#crossdomain)
- [モノタッチとモノドロイドによるiOSとアンドロイドのサポート](#mobile)
- [ポータブル .NET クライアント](#portable)
- [新しいセルフホストパッケージ](#selfhost)
- [下位互換性のあるサーバーのサポート](#backwardcompat)
- [.NET 4.0 のサーバー サポートを削除しました](#remove40)
- [クライアントとグループのリストにメッセージを送信する](#messagelist)
- [特定のユーザーへのメッセージの送信](#sendtouser)
- [より良いエラー処理のサポート](#errorhandling)
- [ハブの単体テストが容易](#unittesting)
- [エラー処理](#javascripterror)

既存の 1.x プロジェクトを SignalR 2.0 にアップグレードする方法の例については[、「SignalR 1.x プロジェクトのアップグレード](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)」を参照してください。

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>OWIN に構築

SignalR 2.0 は[OWIN (.NET 用のオープン Web インターフェイス)](http://owin.org/)上で完全に構築されています。 この変更により、Web ホスト型と自己ホスト型の SignalR アプリケーション間で SignalR のセットアップ プロセスの一貫性が大幅に高くなりますが、API の変更も数多く必要になりました。

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>マップハブとマップコネクションがマップシグナルです

OWIN 標準との互換性を保つために、これらのメソッド`MapSignalR`の名前は に変更されました。 `MapSignalR`パラメーターなしで呼び出されると、すべてのハブが`MapHubs`マップされます (バージョン 1.x の場合と同様)。個々の**PersistentConnection**オブジェクトをマップするには、型パラメーターとして接続の種類を指定し、最初の引数として接続の URL 拡張子を指定します。

この`MapSignalR`メソッドは、Owin スタートアップ クラスで呼び出されます。 Visual Studio 2013 には、Owin スタートアップ クラスの新しいテンプレートが含まれています。このテンプレートを使用するには、次の操作を行います。

1. プロジェクトを右クリックします。
2. **[追加**]、[**新しいアイテム] の順に選択します。**
3. **[Owin スタートアップ クラス**] を選択します。 新しいクラスに名前**を付けるStartup.cs。**

Web**アプリケーションでは、** 以下に示すように、`MapSignalR`メソッドを含む Owin スタートアップ クラスが、Web.Config ファイルのアプリケーション設定ノードのエントリを使用して Owin のスタートアップ プロセスに追加されます。

**自己ホスト型アプリケーション**では、Startup クラスが`WebApp.Start`メソッドの型パラメーターとして渡されます。

**SignalR 1.x のハブと接続のマッピング (Web アプリケーションのグローバル アプリケーション ファイルから):** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**SignalR 2.0 内のハブと接続のマッピング (Owin スタートアップ クラス ファイルから):** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

**自己ホスト型アプリケーション**では、次に示すように、Startup クラスがメソッドの`WebApp.Start`型パラメーターとして渡されます。

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>クロスドメインサポート

SignalR 1.x では、クロス ドメイン要求は単一の EnableCrossDomain フラグによって制御されました。 このフラグは、JSONP 要求と CORS 要求の両方を制御しました。 柔軟性を高めるために、SignalR のサーバー コンポーネントからすべての CORS サポートが削除され (JavaScript クライアントは、ブラウザが CORS をサポートすることが検出された場合は引き続き CORS を使用します)、これらのシナリオをサポートする新しい OWIN ミドルウェアが利用可能になりました。

SignalR 2.0 では、JSONP がクライアントで必要な場合 (古いブラウザーでクロスドメイン要求をサポートするため)、次に示すように`EnableJSONP``HubConfiguration`、オブジェクトに対`true`して設定して明示的に有効にする必要があります。 JSONP は、CORS よりも安全性が低いため、デフォルトでは無効になっています。

SignalR 2.0 で新しい CORS ミドルウェアを`Microsoft.Owin.Cors`追加するには、次のセクションに`UseCors`示すように、プロジェクトにライブラリを追加し、SignalR ミドルウェアの前に呼び出します。

**プロジェクトへの Microsoft.Owin.Cors の追加**: このライブラリをインストールするには、パッケージ マネージャ コンソールで次のコマンドを実行します。

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

このコマンドを実行すると、パッケージの 2.0.0 バージョンがプロジェクトに追加されます。

**使用する呼び出し**

次のコード スニペットは、SignalR 1.x と 2.0 でクロスドメイン接続を実装する方法を示しています。

**SignalR 1.x でのクロスドメイン要求の実装 (グローバル アプリケーション ファイルからの)**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**SignalR 2.0 でのクロスドメイン要求の実装 (C# コード ファイルからの)**

次のコードは、SignalR 2.0 プロジェクトで CORS または JSONP を有効にする方法を示しています。 このコード サンプル`Map`では`RunSignalR``MapSignalR`、 の代わりに を使用し、CORS ミドルウェアは、(で指定されたパスのすべてのトラフィックではなく) CORS サポートを必要`MapSignalR`とする SignalR 要求に対してのみ実行されるようにします。`Map`また、アプリケーション全体ではなく、特定の URL プレフィックスに対して実行する必要がある他のミドルウェアにも使用できます。

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>モノタッチとモノドロイドによるiOSとアンドロイドのサポート

[Xamarin ライブラリ](https://xamarin.com/)からモノタッチと MonoDroid コンポーネントを使用して iOS と Android クライアントのサポートが追加されました。 これらの使用方法の詳細については、「 [Xamarin コンポーネントの使用](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)」を参照してください。 SignalR RTW リリースが利用可能な場合、これらのコンポーネントは[Xamarin ストア](https://store.xamarin.com/)で使用できるようになります。

<a id="portable"></a>### ポータブル .NET クライアント

クロスプラットフォーム開発を容易にするために、Silverlight、WinRT、および Windows Phone クライアントは、次のプラットフォームをサポートする単一のポータブル .NET クライアントに置き換えられました。

- ネット 4.5
- Silverlight 5
- Windows ストア アプリ用の .NET
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>新しいセルフホストパッケージ

SignalR セルフ ホスト (Web サーバーでホストされるのではなく、プロセスまたは他のアプリケーションでホストされている SignalR アプリケーション) を簡単に使い始めるための NuGet パッケージが用意されました。 SignalR 1.x でビルドされたセルフホスト プロジェクトをアップグレードするには、Microsoft.AspNet.SignalR.Owin パッケージを削除し、パッケージを追加します。 セルフホストパッケージの概要については、「[チュートリアル: SignalR セルフホスト](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)」を参照してください。

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>下位互換性のあるサーバーのサポート

SignalR の以前のバージョンでは、クライアントとサーバーで使用される SignalR パッケージのバージョンは同じである必要があります。 更新が困難なシック クライアント アプリケーションをサポートするために、SignalR 2.0 では、古いクライアントで新しいサーバー バージョンを使用できるようになりました。 **注: SignalR 2.0 は、新しいクライアントを使用して古いバージョンで構築されたサーバーをサポートしていません。**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>.NET 4.0 のサーバー サポートを削除しました

SignalR 2.0 は.NET 4.0 とのサーバーの相互運用性のサポートを低下しました。 NET 4.5 は SignalR 2.0 サーバーと共に使用する必要があります。 SignalR 2.0 には.NET 4.0 クライアントがまだあります。

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>クライアントとグループのリストにメッセージを送信する

SignalR 2.0 では、クライアント ID とグループ ID のリストを使用してメッセージを送信できます。 次のコード スニペットは、この方法を示しています。

**永続的な接続を使用して、クライアントとグループの一覧にメッセージを送信します。**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**ハブを使用してクライアントとグループの一覧にメッセージを送信する**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>特定のユーザーへのメッセージの送信

この機能により、ユーザーは新しいインターフェイス IUserIdProvider を介して IRequest に基づいてユーザー ID が何であるかを指定できます。

**インターフェイス**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

既定では、ユーザー名としてユーザーのIPrincipal.Identity.Nameを使用する実装があります。

ハブでは、新しい API を使用してこれらのユーザーにメッセージを送信できます。

**クライアントの使用.ユーザー API**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>より良いエラー処理のサポート

ユーザーは、任意のハブ呼び出しから**HubException**をスローできるようになりました。 **HubException**のコンストラクターは、文字列メッセージとオブジェクトの追加のエラー データを受け取ることができます。 SignalR は、例外を自動シリアル化し、ハブ メソッドの呼び出しを拒否または失敗するために使用されるクライアントに送信します。

**詳細なハブ例外の**設定は、クライアントに送り返される**HubException**に関係ありません。常に送信されます。

**クライアントに HubException を送信する方法を示すサーバー側コード**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**サーバーから送信されたハブ例外への応答を示す JavaScript クライアント コード**

[!code-html[Main](release-notes/samples/sample16.html)]

**サーバーから送信された HubException への応答を示す .NET クライアント コード**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>ハブの単体テストが容易

SignalR 2.0 には、`IHubCallerConnectionContext`モック クライアント側呼び出しを簡単に作成できる、Hubs で呼び出されるインターフェイスが含まれています。 次のコード スニペットは、このインターフェイスを一般的なテスト ハーネス[xUnit.net](https://github.com/xunit/xunit)と[moq](https://code.google.com/p/moq/)で使用する方法を示しています。

**xUnit.netを使用したユニットテスト信号機**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**moq を使用したユニットテストシグナルR**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>エラー処理

SignalR 2.0 では、すべての JavaScript エラー処理コールバックは、生の文字列ではなく JavaScript エラー オブジェクトを返します。 これにより、SignalR は、より豊富な情報をエラー ハンドラーに流すことができます。 エラーのプロパティから内部例外を`source`取得できます。

**開始エラー例外を処理する JavaScript クライアント コード**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET Identity

### <a name="new-aspnet-membership-system"></a>新しいASP.NET会員制度

ASP.NET識別は、ASP.NETアプリケーションの新しいメンバーシップ システムです。 ASP.NET Identity を使用すると、ユーザー固有のプロファイル データをアプリケーション データに簡単に統合できます。 ASP.NET Identity では、アプリケーションのユーザー プロファイルの永続性モデルを選択することもできます。 データは、SQL Server データベースまたは別のデータ ストア (Azure ストレージ テーブルなどの NoSQL データ ストアを含む) に格納できます。 詳細については、「 **Visual Studio 2013 での ASP.NET Web プロジェクトの作成**」の[「個々のユーザー アカウント](creating-web-projects-in-visual-studio.md#indauth)」を参照してください。

### <a name="claims-based-authentication"></a>クレーム ベースの認証

ASP.NETは、ユーザーの ID が信頼された発行者からのクレームのセットとして表されるクレーム ベース認証をサポートするようになりました。 ユーザーは、アプリケーション データベースで管理されているユーザー名とパスワード、またはソーシャル ID プロバイダー (たとえば、Microsoft アカウント、Facebook、Google、Twitter) を使用するか、Azure Active Directory または Active Directory フェデレーション サービス (ADFS) を通じて組織アカウントを使用して認証できます。

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>Azure アクティブ ディレクトリおよび Windows サーバーのアクティブ ディレクトリとの統合

認証に Azure アクティブ ディレクトリまたは Windows サーバーのアクティブ ディレクトリ (AD) を使用するASP.NET プロジェクトを作成できるようになりました。 詳細については、「 Visual Studio **2013 での ASP.NET Web プロジェクトの作成**」の[「組織アカウント](creating-web-projects-in-visual-studio.md#orgauth)」を参照してください。

### <a name="owin-integration"></a>OWIN 統合

ASP.NET認証は、OWIN ベースのホストで使用できる OWIN ミドルウェアに基づくようになりました。 OWIN の詳細については、次の[マイクロソフトの OWIN コンポーネントセクションを](#TOC7)参照してください。

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Microsoft OWIN コンポーネント

[オープン Web インターフェイスの .NET](http://owin.org/) (OWIN) は、.NET Web サーバーと Web アプリケーション間の抽象化を定義します。 OWIN は Web アプリケーションをサーバーから切り離し、Web アプリケーションをホストに依存しません。 たとえば、IIS で OWIN ベースの Web アプリケーションをホストしたり、カスタム プロセスで自己ホストしたりできます。

Microsoft OWIN コンポーネント (Katana プロジェクトとも呼ばれます) で導入された変更点には、新しいサーバーコンポーネントとホスト コンポーネント、新しいヘルパー ライブラリとミドルウェア、新しい認証ミドルウェアなどがあります。

OWIN とカタナの詳細については、「 [OWIN およびカタナの新機能](../../../aspnet/overview/owin-and-katana/index.md)」を参照してください。

**注: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)アプリケーションは IIS クラシック モードでは実行できません。統合モードで実行する必要があります。**

**注: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)アプリケーションは、完全信頼で実行する必要があります。**

### <a name="new-servers-and-hosts"></a>新しいサーバーとホスト

このリリースでは、セルフホストシナリオを可能にする新しいコンポーネントが追加されました。 これらのコンポーネントには、次の NuGet パッケージが含まれます。

- **マイクロソフト.Owin.ホスト.Httpリスナー**. HTTPListener を使用して**HTTP 要求**をリッスンし、OWIN パイプラインに送信する OWIN サーバーを提供します。
- **コンソール**アプリケーションや Windows サービスなどのカスタム プロセスで OWIN パイプラインを自己ホストする開発者向けのライブラリを提供します。
- **オビンホスト**. カスタム ホスト アプリケーションを作成しなくても`Microsoft.Owin.Hosting`OWIN パイプラインをラップして自己ホストできるスタンドアロンの実行可能ファイルを提供します。

さらに、このパッケージ`Microsoft.Owin.Host.SystemWeb`では、ミドルウェアが**SystemWeb**サーバーにヒントを提供できるようになったので、特定のASP.NET パイプラインステージでミドルウェアを呼び出す必要があることを示します。 この機能は、ASP.NET パイプラインの初期段階で実行する必要がある認証ミドルウェアに特に便利です。

### <a name="helper-libraries-and-middleware"></a>ヘルパー ライブラリとミドルウェア

OWIN 仕様の関数と型の定義のみを使用して OWIN コンポーネントを作成できますが、`Microsoft.Owin`新しいパッケージでは、よりユーザーフレンドリな抽象化セットが提供されます。 このパッケージは、いくつかの以前のパッケージ (たとえば、 `Owin.Extensions`)`Owin.Types`を組み合わせて、他の OWIN コンポーネントで簡単に使用できる、適切に構造化された単一のオブジェクト モデルにします。 実際、現在、大部分の OWIN コンポーネントがこのパッケージを使用しています。

> [!NOTE]
> [OWIN](http://www.owin.org)アプリケーションは IIS クラシック モードでは実行できません。統合モードで実行する必要があります。

> [!NOTE]
> [OWIN](http://www.owin.org)アプリケーションは、完全な信頼で実行する必要があります。

このリリースには、実行中の OWIN アプリケーションを検証するためのミドルウェアと、エラーの調査に役立つエラー ページミドルウェアが含まれる Microsoft.Owin.Diagnostics パッケージも含まれています。

### <a name="authentication-components"></a>認証コンポーネント

次の認証コンポーネントを使用できます。

- **マイクロソフト.Owin.セキュリティ.アクティブディレクトリ**. オンプレミスまたはクラウドベースのディレクトリ サービスを使用した認証を有効にします。
- **クッキーを**使用した認証を有効にします。 このパッケージは以前に`Microsoft.Owin.Security.Forms`という名前でした。
- **Facebookの**OAuthベースのサービスを使用した認証を有効にします。
- **Google の**OpenID ベースのサービスを使用した認証を有効にします。
- JWT トークンを使用した**認証を有効**にします。
- **マイクロソフト アカウントを**使用した認証を有効にします。
- **マイクロソフト.Owin.セキュリティ.OAuth**. ベアラー トークンを認証するためのミドルウェアと同様に、OAuth 承認サーバーを提供します。
- **Twitter の**OAuth ベースのサービスを使用した認証を有効にします。

このリリースには、クロス`Microsoft.Owin.Cors`オリジン HTTP 要求を処理するためのミドルウェアが含まれているパッケージも含まれています。

> [!NOTE]
> JwT 署名のサポートは、Visual Studio 2013 の最終バージョンでは削除されました。

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

Entity Framework 6 の新機能およびその他の変更の一覧については、「[エンティティ フレームワークのバージョン履歴](https://msdn.com/data/jj574253)」を参照してください。

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NETカミソリ3

ASP.NETのRazor 3には、次の新機能が含まれています。

- タブ編集のサポート。 以前は、[**タブを保持**] オプションを使用する場合、Visual Studio での **[ドキュメントの書式設定**] コマンド、自動インデント、および自動書式設定が正しく機能しませんでした。 この変更により、タブの書式設定に関する Razor コードの Visual Studio の書式設定が修正されます。
- リンク生成時の URL 書き換えルールのサポート。
- 透過的セキュリティ属性の削除
  > [!NOTE]
  > これは画期的な変更であり、Razor 3 は MVC4 以前と互換性がありませんが、Razor 2 は MVC5 または MVC5 に対してコンパイルされたアセンブリと互換性がありません。

プレリリース版から Visual Studio 2013 で修正された Razor 3 の問題は[、こちら](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)を見つけることができます。

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NETアプリの中断

ASP.NETアプリケーションの中断は、1 台のコンピューターで多数のASP.NET サイトをホストするためのユーザー エクスペリエンスと経済モデルを根本的に変更する .NET Framework 4.5.1 のゲームを変更する機能です。 詳細については、「[アプリの中断 - 応答性の高い共有 .NET web ホスティング](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)」をASP.NETするを参照してください。

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>既知の問題と互換性に関する変更

このセクションでは、Visual Studio 2013 のASP.NETと Web ツールでの既知の問題と互換性に関する変更点について説明します。

### <a name="nuget"></a>NuGet

- [新しいパッケージの復元は、SLN ファイルを使用する場合は Mono で動作しません](https://nuget.codeplex.com/workitem/3596)- nuget.exe のダウンロードと[NuGet.CommandLine パッケージ](http://www.nuget.org/packages/NuGet.CommandLine/)の更新プログラムで修正されます。
- [新しいパッケージの復元は Wix プロジェクトでは動作しません](https://nuget.codeplex.com/workitem/3598)- 今後の nuget.exe ダウンロードと[NuGet.CommandLine パッケージ](http://www.nuget.org/packages/NuGet.CommandLine/)の更新プログラムで修正されます。
- [自動パッケージの復元は、ソリューション フォルダーの下のプロジェクトでは機能しません](https://nuget.codeplex.com/workitem/3625)- NuGet 2.8 で修正されます。

### <a name="aspnet-web-api"></a>ASP.NET Web API

1. `ODataQueryOptions<T>.ApplyTo(IQueryable)`と のサポート`IQueryable<T>`を追加したので、常に`$select`戻る`$expand`わけではありません。

    以前のサンプルでは`ODataQueryOptions<T>`、戻り値が常に`ApplyTo``IQueryable<T>`から にキャストされます。 以前にサポートしていたクエリ`$filter`オプション ( , , `$orderby` `$skip`)`$top`ではクエリの形状が変更されないため、これは以前に機能していました。 今、私たちは`$select`サポート`$expand`し、戻`ApplyTo`り値は常`IQueryable<T>`にではありません。

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    以前のサンプル コードを使用している場合、クライアントが 送信しない場合は引き続`$select`き`$expand`動作します。 ただし、サポート`$select`を希望し、`$expand`そのコードをこれに変更する必要がある場合は、

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **バッチ要求中に、要求 URL または要求コンテキスト URL が null です。**

    バッチ処理シナリオでは、要求 URL または**要求コンテキスト** **URL**からアクセスすると**UrlHelper**は null です。

    この問題は現在ここで追跡されています:[バッチ処理要求の場合、Url は null です](http://aspnetwebstack.codeplex.com/workitem/1301)。

    この問題の回避策は、次の例のように**UrlHelper**の新しいインスタンスを作成することです。

    **Url ヘルパーの新しいインスタンスの作成**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. MVC5 と OrgAuth を使用する場合、AntiForgerToken 検証を行うビューがある場合、ビューにデータを送信するときに次のエラーが発生する可能性があります。

    **エラー**:

    *'/' アプリケーションのサーバー エラーです。*

    <em>指定された ClaimsId<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>に<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>'' または ' ' の型のクレームが存在しませんでした。クレームベース認証で偽造防止トークンのサポートを有効にするには、構成されたクレーム プロバイダーが、生成する ClaimsIdentity インスタンスでこれらの両方のクレームを提供していることを確認してください。構成済みのクレーム プロバイダーが一意の識別子として異なるクレームの種類を使用する場合は、静的プロパティ AntiForgeryConfig.UniqueClaimTypeIdentifier を設定することで構成できます。</em>

    **対応策**:

    これを修正するには、Global.asax に次の行を追加します。

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    これは、次のリリースで修正されます。
2. MVC4 アプリを MVC5 にアップグレードした後、ソリューションをビルドして起動します。 次のエラーが表示されます。

    [A][B] システムにキャストできません。 タイプ\_A は 'System.Web.WebPages.Razor から発信されます。 バージョン=2.0.0.0,カルチャー=ニュートラル,公開鍵トークン=31bf3856ad364e35''コンテキスト'の場所'C:\windows\Net\アセンブリ\GAC MSIL\システム.Web.Webページ.Razor\v4.0\_2.0.0.31bf3856ad364e33\Web.Dll.Web.Web.Dll.Web.Web.Dll.Web.Web\_\_ページ タイプ B は 'System.Web.WebPages.Razor, バージョン = 3.0.0.0, カルチャ =ニュートラル、 場所 'C:\Windows\NET\Framework\v4.0.30319\一時ASP.NET ファイル\ルート\6 のコンテキスト '既定' で公開キートークン=31bf3856ad364e35' d05bbd0\e8b5908e\アセンブリ\dl3\c9cbca63\f8910382\_6273ce01\システム.Web.WebPages.Razor.dll'。

    上記のエラーを修正するには、プロジェクト*内のすべての*Web.config ファイル (Views フォルダー内のファイルを含む) を開き、次の操作を行います。

   1. "System.Web.Mvc" のバージョン "4.0.0.0" のすべてのオカレンスを "5.0.0.0" に更新します。
   2. 「システム.Web.ヘルパー」、システム&quot;.Web.Webページ、&quot;&quot;システム.Web.WebPages.Razor&quot;のバージョン"2.0.0.0"のすべてのオカレンスを「3.0.0.0」に更新します。

      たとえば、上記の変更を行った後、アセンブリ バインディングは次のようになります。

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      MVC 4 プロジェクトを MVC 5 にアップグレードする[方法については、「MVC 4 と Web API プロジェクトASP.NETを MVC 5 と Web API 2 ASP.NETにアップグレードする方法](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)」を参照してください。
3. jQuery の控えめな検証でクライアント側の検証を使用する場合、検証メッセージは、型が'number' の HTML 入力要素に対して正しくない場合があります。 有効な数値が必要であることを示す正しいメッセージではなく、無効な数値が入力されると、必要な値の検証エラー (「年齢フィールドが必要です」) が表示されます。

    この問題は、一般に、作成ビューと編集ビューで整数プロパティを持つモデルのスキャフォールディングされたコードで発生します。

    この問題を回避するには、エディター ヘルパーを次の手順で変更します。

    `@Html.EditorFor(person => person.Age)`

    変更後:

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5 では、部分信頼がサポートされなくなりました。 MVC または WebAPI バイナリにリンクしているプロジェクトは、[セキュリティトランスペアレント](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx)属性と[AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)属性を削除する必要があります。 これらの属性を削除すると、次のようなコンパイラ エラーが解消されます。

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > この副次的な効果として、同じアプリケーションで 4.0 および 5.0 のアセンブリを使用することはできません。 すべてのファイルを 5.0 に更新する必要があります。

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>Facebookの承認を持つSPAテンプレートは、Webサイトがイントラネットゾーンでホストされている間、IEで不安定になる可能性があります

SPA テンプレートは、Facebook で外部ログインを提供します。 テンプレートで作成されたプロジェクトがローカルで実行されている場合、サインインすると IE がクラッシュする可能性があります。

解決方法:

1. インターネット ゾーンで Web サイトをホストします。または

2. IE 以外のブラウザーでシナリオをテストします。

### <a name="web-forms-scaffolding"></a>Web フォームのスキャフォールディング

Web フォームスキャフォールディングは VS2013 から削除され、Visual Studio の今後の更新プログラムで使用できるようになります。 ただし、MVC 依存関係を追加し、MVC のスキャフォールディングを生成することで、Web フォーム プロジェクト内でスキャフォールディングを使用できます。 プロジェクトには、Web フォームと MVC の組み合わせが含まれます。

Mvc を Web フォーム プロジェクトに追加するには、新しいスキャフォールディングされた項目を追加し **、[MVC 5 依存関係**] を選択します。 スクリプトなど、すべてのコンテンツ ファイルが必要かどうかに応じて、[最小] または [完全] を選択します。 次に、プロジェクト内にビューとコント ローラーを作成する MVC のスキャフォールディング項目を追加します。

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC および Web API スキャフォールディング - HTTP 404、見つかりませんエラー

スキャフォールディングされた項目をプロジェクトに追加するときにエラーが発生した場合、プロジェクトが不整合な状態のままになる可能性があります。 スキャフォールディングに加えられた変更の一部はロールバックされますが、インストールされている NuGet パッケージなどの他の変更はロールバックされません。 ルーティング構成の変更がロールバックされると、スキャフォールディングされたアイテムに移動するときに、ユーザーに HTTP 404 エラーが表示されます。

対処法:

- MVC のこのエラーを修正するには、新しいスキャフォールディングされた項目を追加し、MVC 5 の依存関係 (最小または完全) を選択します。 このプロセスにより、必要な変更がすべてプロジェクトに追加されます。
- Web API でこのエラーを修正するには、次の手順を実行します。

  1. プロジェクトにクラスを追加します。

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. 次のようにして、Global.asax\_のアプリケーション開始メソッドで WebApiConfig.Register を構成します。

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
