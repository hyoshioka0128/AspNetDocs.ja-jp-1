---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: Visual Studio 2013 リリース ノートのASP.NETと Web ツール 2013.2 |マイクロソフトドキュメント
author: rick-anderson
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 41b0f3ad43846bc5799ecd398188b0f6ffcc0d66
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543627"
---
# <a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>Visual Studio 2013 の ASP.NET と Web 2013.2 ツールのリリース ノート

[マイクロソフト](https://github.com/microsoft)

## <a name="installation-notes"></a>インストールに関する注意事項

visual Studio 2013.2 のASP.NETと Web ツールは、メイン インストーラーにバンドルされており[、Visual Studio 2013 更新プログラム 2](https://go.microsoft.com/fwlink/?LinkId=390521)の一部としてダウンロードできます。

## <a name="documentation"></a>ドキュメント

チュートリアルおよびその他の情報 ASP.NETと Visual Studio 2013.2 の Web ツールは[、ASP.NET Web サイト](https://www.asp.net/)から入手できます。

## <a name="software-requirements"></a>ソフトウェア要件

visual Studio 2013.2 のASP.NETと Web ツールには、Visual Studio 2013 が必要です。

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>ASP.NETおよび Web ツールの新機能 2013.2

以下のセクションでは、リリースで導入された機能について説明します。

- [プロジェクト テンプレートASP.NET 1 つ](#oneaspnet)
- [IIS Express で Web アプリケーションを起動する際の SSL のサポート](#ssl)
- [ビジュアル スタジオ Web エディターの機能強化](#vswebeditor)
- [ブラウザー リンク](#browserlink)
- [Visual Studio での Azure アプリ サービス Web アプリのサポート](#waws)
- [新しい Web プロジェクトを作成するときにリモート Azure リソースを作成する](#AzureResources)
- [Web 発行の機能強化](#webpublish)
- [ASP.NET足場](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET Web Forms](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NETウェブ API 2.1.2](#webapi)
- [ASP.NETウェブページ 3.1.2](#webpages)
- [エンティティ フレームワーク 6.1](#ef)
- [ASP.NETアイデンティティ 2.0.0](#identity)
- [マイクロソフト OWIN コンポーネント](#owin)
- [ASP.NET信号機 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>プロジェクト テンプレートASP.NET 1 つ

- アカウントの確認とパスワードのリセットをサポートするプロジェクト テンプレートをASP.NETする更新。
- オンプレミスASP.NET組織アカウントを使用した認証をサポートするように Web API テンプレートを更新します。
- ASP.NET SPA テンプレートには、MVC とサーバー側のビューに基づく認証が含まれるようになりました。 テンプレートには、認証されたユーザーのみがアクセスできる WebAPI コントローラーがあります。

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>IIS Express で Web アプリケーションを起動する際の SSL のサポート

ローカルホストで HTTPS を参照およびデバッグする際のセキュリティ警告を排除するために、Internet Explorer と Chrome が自己署名 IIS express SSL 証明書を信頼できるようにするダイアログを追加しました。

たとえば、Web プロジェクトのプロパティを SSL を使用するように設定できます。 F4 をクリックしてプロパティ ダイアログを表示します。 **[SSL の有効化] を**true に変更します。 SSL URL をコピーします。

![SSL 対応プロパティ](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

HTTPS ベースの URL を使用するように Web プロジェクトのプロパティ ページの`https://localhost:44300/`Web タブを設定します (SSL Web サイトを以前に作成していない限り、SSL URL は使用されます)。

![プロジェクト URL の設定 (HTTPS)](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。 IIS Express が生成した自己署名証明書を信頼する手順に従います。

![SSL 警告](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

localhost を表す証明書をインストールする場合は、**セキュリティの警告**ダイアログを読み、[**はい**] をクリックします。

![Security Warning](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

サイトは、ブラウザで証明書の警告なしでIEまたはChromeに表示されます。

![警告なしの HTTPS ページ](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox は独自の証明書ストアを使用するため、警告が表示されます。

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>ビジュアル スタジオ Web エディターの機能強化

- **新しい JSON プロジェクト項目とエディター**: JSON プロジェクト項目とエディターが Visual Studio に追加されました。 現在の JSON エディターの機能には、色付け、構文の検証、中かっこの補完、アウトライン、ツール オプションの設定などがあります。

    ![JSON エディタ](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    IntelliSense は[JSON スキーマ](http://json-schema.org/)v3 と v4 をサポートするようになりました。 既存のスキーマを選択したり、ローカルスキーマパスを編集したり、プロジェクトJSONファイルをドラッグして相対パスを取得するスキーマコンボボックスがあります。

    ![JSONインテリセンス](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON スキーマ エディター](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **新しい Sass (SCSS) エディター**: VS2013 RTM で LESS を追加し、Sass プロジェクトアイテムとエディターを追加しました。 Sass エディタの機能は、LESS エディターに匹敵し、色付け、変数と Mixins IntelliSense、コメント/コメント解除、クイック ヒント、書式設定、構文検証、アウトライン、移動の定義、カラー ピッカー、ツール オプションの設定などを含みます。

    ![新しい項目の追加: SCSS スタイル シート](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![スタイルシートエディタ](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **HTML、カミソリ、CSS、LESS、およびサス文書の新しい URL ピッカー:** VS 2013 は、Web フォーム ページの外部に URL ピッカーを使用しないものとして出荷されました。 HTML、Razor、CSS、LESS、およびSassエディタの新しいURLピッカーは、ダイアログフリーで流暢なタイピングピッカーで、'.' を理解しています。 img タグとリンクに対して適切にファイルリストをフィルターします。

    ![イメージ タグの URL ピッカー](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![ビューの URL ピッカー](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![CSS の URL ピッカー](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **機能を追加して LESS エディタを更新**
- **ノックアウト インテリセンス アップグレード**: VS intelliSense の "コ対エディタの viewModel:" 構文に対して、標準以外のノックアウト構文を追加しました。 このメソッドを使用すると、次の形式のコメントを使用して、ページ上の複数のビュー モデルにバインドできます。

    ![ノックアウトインテッリセンス](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    また、入れ子になったビューモデル IntelliSense のサポートも追加されているので、ビューモデルで深くネストされたオブジェクトにドリルインできます。

    `<div data-bind="text: foo.bar.baz.etc" />`

    表示されるインテリセンスは、JavaScript オブジェクトの完全な IntelliSense です。

    ![完全な JavaScript オブジェクトを示すインテリセンス](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **HTML、カミソリ、CSS、LESS、および Sass ドキュメントの新しい URL ピッカー**: VS 2013 は Web フォーム ページの外部で URL ピッカーなしで出荷されました。 HTML、Razor、CSS、LESS、およびSassエディタの新しいURLピッカーは、ダイアログフリーで流暢なタイピングピッカーで、'.' を理解しています。 img タグとリンクに対して適切にファイルリストをフィルターします。

    ![イメージ タグの URL ピッカー](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![ビューの URL ピッカー](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![CSS の URL ピッカー](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>ブラウザー リンク

- ブラウザリンクはHTTPS接続をサポートするようになりましたが、証明書がブラウザによって信頼されている限り、他の接続とダッシュボードにそれを一覧表示します。
- 静的 HTML ソース マッピング
- データのマッピングに対する SPA のサポート
- マッピング データの自動更新

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>Visual Studio での Azure アプリ サービス Web アプリのサポート

- **Azure サインインをサポートします。**
- **リモート デバッグと Web アプリのリモート ビュー**: [Azure App Service の Web アプリのリモート デバッグ](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)と、サーバー エクスプローラーでの Web アプリ コンテンツ ファイルのリモート ビューがサポートされるようになりました。

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>新しい Web プロジェクトを作成するときにリモート Azure リソースを作成する

新しい Web アプリケーション ダイアログで、Azure[の [リモート リソースの作成]](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)チェック ボックスが追加されました。 これを選択することで、新しい Web アプリケーションの作成、テスト用の Azure 発行サイトのセットアップ、および発行プロファイルの作成をいくつかの簡単な手順で統合できます。

![Azure リソースを使用した新しいプロジェクト](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![Azure への発行](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>Web 発行の機能強化

- 公開のユーザー エクスペリエンスを向上します。

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET足場

- **列挙のサポート:** モデルが Enums を使用している場合、MVC スキャフフォルダーは列挙のドロップダウンを生成します。 これは、MVC で列挙ヘルパーを使用します。
- **ブートストラップのサポート**: 彼らはブートストラップクラスを使用するように、MVCスキャフォールディングでEditorForテンプレートを更新しました。
- **パッケージのサポート**: MVC と Web API のスキャフフォルダーは、MVC と Web API の 5.1 パッケージを追加します。

次のスクリーンショットは、スキャフォールディング モデルを示しています。

- モデル コード:

     ![モデル コード](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- モデル コードをコンパイルして右クリックし、[**追加**]、[**新しいスキャフォールディングされた項目**] の順に選択します。

     ![新しいスキャフォールディングアイテムの追加](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- **エンティティ フレームワークを使用して、ビューを持つ MVC5 コント ローラーを**選択します。

     ![ビューを含む新しい MVC5 コント ローラーを追加します。](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- モデルを使用して**コントローラを追加**します。

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- 生成されたコードを確認してください(例: 列挙を含むビューを含む`@Html.EnumDropDownListFor`ビュー ![/平日モデル/Edit.cshtmlが含まれています)](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- 生成された列挙型コンボ ボックスを表示するには、ページを実行します。 たとえば、[**作成**] ページには次の情報が表示されます。

    ![空の文字列を許可するコンボ ボックス](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM は 2014 年 4 月にリリースされる予定です。 リリース ノートの顕著なポイントはここにありますが、これらの変更の詳細については[、リリース ノートの全文](http://docs.nuget.org/docs/release-notes/nuget-2.8)を参照してください。

- **ターゲット Windows Phone 8.1 アプリケーション**: NuGet 2.8.1 は、ターゲット フレームワーク モニカー 'WindowsPhoneApp'、'WPA'、'WindowsPhoneApp81'、および 'WPA81' を使用して Windows Phone 8.1 アプリケーションをターゲットにできるようになりました。

- **依存関係の修正プログラムの解決**: パッケージの依存関係を解決する際、NuGet は、パッケージの依存関係を満たす最小メジャーおよびマイナー パッケージ バージョンを選択する戦略を従来実装してきました。 ただし、メジャーバージョンやマイナーバージョンとは異なり、パッチバージョンは常に最高バージョンに解決されました。 この動作は善意でしたが、依存関係のあるパッケージをインストールするための決定論が不足していました。
- **依存関係バージョン切り替え**: NuGet 2.8 は依存関係を解決するための*既定*の動作を変更しますが、パッケージ マネージャー コンソールの -DependencyVersion スイッチを使用して依存関係解決プロセスをより正確に制御することもできます。 このスイッチを使用すると、可能な限り低いバージョン (既定の動作)、可能な限り最高のバージョン、または最も高いマイナーバージョンまたはパッチ バージョンへの依存関係の解決が可能になります。 このスイッチは、powershell コマンドのインストールパッケージに対してのみ機能します。
- **依存関係バージョン属性**: 上記で説明した -DependencyVersion スイッチに加えて、NuGet では、-DependencyVersion スイッチがインストール パッケージの呼び出しで指定されていない場合に、nuget.config ファイルに新しい属性を設定して既定値を定義する機能も許可されています。 この値は、インストール パッケージ操作の NuGet パッケージ マネージャー ダイアログでも尊重されます。 この値を設定するには、以下の属性を nuget.config ファイルに追加します。

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **NuGet 操作のプレビュー :WhatIf**: 一部の NuGet パッケージには、深い依存関係グラフが含まれる場合があり、インストール、アンインストール、または更新操作の間に、最初に何が起こるかを確認するのに役立ちます。 NuGet 2.8 では、標準の PowerShell -インストール パッケージ、アンインストール パッケージ、および更新プログラム パッケージ コマンドに切り替える場合は、コマンドが適用されるパッケージのクロージャ全体を視覚化できるようにします。
- **ダウングレードパッケージ**:新機能を調査し、最後の安定版にロールバックすることを決定するために、パッケージのプレリリースバージョンをインストールすることは珍しいことではありません。 NuGet 2.8 より前のバージョンでは、プレリリース パッケージとその依存関係をアンインストールし、以前のバージョンをインストールする複数の手順で行っていました。 ただし、NuGet 2.8 では、パッケージのクロージャ全体 (パッケージの依存関係ツリーなど) が以前のバージョンにロールバックされます。
- **開発の依存関係**: 開発プロセスの最適化に使用されるツールを含め、さまざまな種類の機能を NuGet パッケージとして提供できます。 これらのコンポーネントは、新しいパッケージの開発に役立ちますが、後で発行されるときには、新しいパッケージの依存関係と見なされません。 NuGet 2.8 では、パッケージが開発依存として .nuspec ファイル内で自分自身を識別できます。 このメタデータは、インストールされると、パッケージがインストールされたプロジェクトの packages.config ファイルにも追加されます。 その packages.config ファイルが後で nuget.exe パック中に NuGet 依存関係を分析する場合、開発依存関係としてマークされた依存関係は除外されます。
- **異なるプラットフォーム用の個別の packages.config ファイル**: 複数のターゲット プラットフォーム用のアプリケーションを開発する場合、各ビルド環境ごとに異なるプロジェクト ファイルを持つことは一般的です。 また、パッケージのサポートレベルはプラットフォームによって異なるため、さまざまなプロジェクト ファイルで異なる NuGet パッケージを使用することも一般的です。 NuGet 2.8 では、プラットフォーム固有のプロジェクト ファイルごとに異なる packages.config ファイルを作成することで、このシナリオのサポートが強化されています。
- **ローカル キャッシュへのフォールバック**: 通常、ネットワーク接続を使用する[NuGet ギャラリー](http://www.nuget.org)などのリモート ギャラリーから NuGet パッケージが使用されていますが、クライアントが接続されていないシナリオは多数あります。 ネットワーク接続がないと、NuGet クライアントは、パッケージが既にローカルの NuGet キャッシュ内のクライアントのコンピューターに存在する場合でも、パッケージを正常にインストールできませんでした。 NuGet 2.8 では、パッケージ マネージャー コンソールに自動キャッシュ フォールバックが追加されます。

    キャッシュ フォールバック機能では、特定のコマンド引数は必要ありません。 さらに、キャッシュ フォールバックは現在、パッケージ マネージャー コンソールでのみ機能します。
- **バグ修正**: 主なバグ修正の 1 つは、update-package -reinstall コマンドのパフォーマンス向上です。

    これらの機能と前述のパフォーマンス修正に加えて、NuGet のこのリリースには、他の多くのバグ修正も含まれています。 リリースでは、合計 181 件の問題が解決されました。 NuGet 2.8 で修正された作業項目の完全な一覧については、このリリースの[NuGet の問題トラッカー](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)を参照してください。

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET Web Forms

- Web フォーム テンプレートに、ASP.NET ID のアカウント確認とパスワードのリセットを行う方法が示されました。
- エンティティ データ ソース コントロールとエンティティ フレームワーク 6 の動的データ プロバイダー。 詳細については、次の MSDN ブログを参照してください:[エンティティ フレームワーク 6 の動的データ プロバイダーと EntityDataSource コントロール](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)。

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [属性ルーティングの改善](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [エディタテンプレートのブートストラップサポート](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [ビューでの列挙のサポート](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [MinLength/MaxLength 属性の控えめなサポート](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [控えめなAjaxで「この」コンテキストをサポート](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- さまざまな[バグ修正](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NETウェブ API 2.1.2

- [グローバル エラー処理](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [属性ルーティングの強化](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [ヘルプ ページの機能強化](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [ルートのサポートを無視する](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON メディアタイプフォーマッタ](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [非同期フィルターのサポートの向上](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [クライアント・フォーマット・ライブラリーの照会解析](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- さまざまな[バグ修正](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NETウェブページ 3.1.2

- さまざまな[バグ修正](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>エンティティ フレームワーク 6.1

エンティティ フレームワークは、ランタイムとツールの両方のバージョン 6.1 に更新されました。 エンティティ フレームワーク (EF) 6.1 は、エンティティ フレームワーク 6 のマイナーな更新プログラムで、バグ修正と新機能の数が含まれています。 EF6.1 の詳細については、新機能のドキュメントへのリンクを含む Entity [Framework のバージョン履歴](https://msdn.microsoft.com/data/jj574253)を参照してください。 このリリースの新機能は次のとおりです。

- **ツールの統合**により、新しい EF モデルを作成する一貫した方法が提供されます。 この機能は、既存のデータベースからのリバース エンジニアリングを含む、コード ファースト モデルの作成をサポートするADO.NET エンティティ データ モデル ウィザードを拡張します。 これらの機能は、以前は EF パワー ツールのベータ品質で使用できました。
- **トランザクション コミットエラーの処理は、** トランザクション操作をインターセプトする新しく導入された機能を利用する新しい[System.Data.Entity.Infrastructure.CommitFailureHandler](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx)を提供します。 **CommitFailureHandler**は、トランザクションをコミットしている間、接続障害からの自動リカバリを可能にします。
- **IndexAttribute**を使用すると、コードファースト モデルのプロパティ (またはプロパティ) に属性を配置することで、インデックスを指定できます。 次に、Code First は、対応するインデックスをデータベースに作成します。
- **パブリック マッピング API**は、プロパティと型がデータベース内の列とテーブルにどのようにマップされるかについて、EF が持つ情報へのアクセスを提供します。 過去のリリースでは、この API は内部です。
- **App/Web.config ファイルを介してインターセプターを構成する機能**(アプリケーションを再コンパイルせずにインターセプターを追加できるようにする)
- **DatabaseLogger**は、すべてのデータベース操作をファイルに簡単に記録できる新しいインターセプターです。 前の機能と組み合わせて、再コンパイルする必要なく、配置済みのアプリケーションのデータベース操作のログ記録を簡単に切り替えることができます。
- **移行モデルの変更検出**が改善され、スキャフォールディングされた移行がより正確になります。変更検出プロセスのパフォーマンスも大幅に向上しました。
- 初期化中のデータベース操作の削減、LINQ クエリでの NULL 等価比較の最適化、より多くのシナリオでのビュー生成 (モデルの作成) の高速化、複数の関連付けを持つ追跡対象エンティティのより効率的な具体化など、**パフォーマンスの向上**。

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NETアイデンティティ 2.0.0

- **2 要素認証**: ASP.NET ID は、2 要素認証をサポートするようになりました。 2 要素認証は、パスワードが侵害された場合に、ユーザー アカウントにセキュリティの追加レイヤーを提供します。 また、2 つの因子コードに対するブルート フォース攻撃の保護もあります。
- **アカウントロックアウト:** ユーザーがパスワードまたは 2 要素コードを誤って入力した場合に、ユーザーをロックアウトする方法を提供します。 無効な試行回数と、ロックアウトされたユーザの期間を設定できます。 開発者は、必要に応じて特定のユーザー アカウントのアカウント ロックアウトをオフにすることもできます。
- **アカウントの確認:** ASP.NET ID システムでアカウントの確認がサポートされるようになりました。 これは、ウェブサイト上で新しいアカウントに登録すると、ウェブサイトで何かを行う前に電子メールを確認する必要がある、今日のほとんどのウェブサイトではかなり一般的なシナリオです。 電子メールの確認は偽のアカウントが作成されるのを防ぐため便利です。 これは、フォーラムサイト、銀行、eコマース、ソーシャルWebサイトなど、ウェブサイトのユーザーと通信する方法として電子メールを使用している場合に非常に便利です。
- **パスワードのリセット:** パスワードリセットは、パスワードを忘れた場合にユーザーがパスワードをリセットできる機能です。
- **セキュリティスタンプ(どこでもサインアウト):** ユーザーがパスワードを変更した場合、または関連付けられているログイン(Facebook、Google、Microsoft アカウントなど)の削除などのセキュリティ関連情報を変更した場合に、ユーザーのセキュリティ トークンを再生成する方法をサポートします。 これは、古いパスワードで生成されたトークンを確実に無効にするために必要です。 サンプル プロジェクトでは、ユーザーのパスワードを変更すると、ユーザーに対して新しいトークンが生成され、以前のトークンは無効になります。 この機能は、あなたのパスワードを変更するとき、あなたがこのアプリケーションにログインしているどこでも(他のすべてのブラウザ)からログアウトされるので、あなたのアプリケーションにセキュリティの余分な層を提供します。
- **ユーザーとロールの主キーの種類を拡張可能に**する : ASP.NET ID 1.0 では、テーブルユーザーとロールの主キーの種類は文字列でした。 これは、エンティティ フレームワークを使用して ASP.NET ID システムが SQL Server に永続化されたとき、nvarchar を使用していたことを意味します。 スタックオーバーフローに関するこのデフォルトの実装の周りに多くの議論があり、着信フィードバックに基づいています。 ユーザーとロール テーブルの主キーを指定できる機能拡張フックを提供しました。 この機能拡張フックは、アプリケーションを移行する際に、アプリケーションが Guid または ints である UserId を格納していた場合に特に便利です。
- **ユーザーとロールでの IQueryable**のサポート : ユーザーストアおよびロールストアでの IQueryable のサポートが追加され、ユーザーとロールの一覧を簡単に取得できます。
- **ユーザー マネージャーを使用して削除操作をサポートします。**
- **ユーザー名のインデックス作成**: id エンティティ フレームワークの実装ASP.NET、EF 6.1.0 の新しい IndexAttribute を使用して、ユーザー名に一意のインデックスを追加しました。 これにより、ユーザー名は常に一意であり、重複するユーザー名で終わる可能性のある競合状態が発生しません。
- **拡張パスワード検証ツール:** ASP.NET Identity 1.0 に付属していたパスワード検証コントロールは、最短長のみを検証する非常に基本的なパスワード検証コントロールでした。 パスワードの複雑さをより詳細に制御できる新しいパスワード検証コントロールがあります。 このパスワードのすべての設定を有効にした場合でも、ユーザー アカウントに対して 2 要素認証を有効にすることをお勧めします。
- **アイデンティティファクトリーミドルウェア/CreatePerOwinContext**:

    - **ユーザー マネージャ**: ファクトリ実装を使用して、OWIN コンテキストから UserManager のインスタンスを取得できます。 このパターンは、サインインとサインアウトの OWIN コンテキストから認証マネージャを取得する場合と似ています。 これは、アプリケーションの要求ごとに UserManager のインスタンスを取得する場合に推奨される方法です。
    - **DbContextFactory**: ASP.NET ID は、エンティティ フレームワークを使用して、SQL Server で ID システムを永続化します。 これを行うには、ID システムにアプリケーションDbContext への参照があります。 アプリケーションで使用できる要求ごとに ApplicationDbContext のインスタンスを返します。
- **ASP.NET ID サンプルの NuGet パッケージ**: サンプル NuGet パッケージを使用すると、ASP.NET ID のサンプルを簡単にインストールして実行し、ベスト プラクティスに従うことができます。 これは、MVC アプリケーションASP.NETサンプルです。 実稼働環境にデプロイする前に、アプリケーションに合わせてコードを変更してください。 サンプルは空のASP.NET アプリケーションにインストールする必要があります。 パッケージの詳細については、次のブログ記事を参照してください: [ASP.NET ID 2.0.0 の RTM を発表する](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>マイクロソフト OWIN コンポーネント

このリリースでは修正されたバグが多数ありました。 詳細については[、2.1.0 リリースのリリース ノート](https://katanaproject.codeplex.com/releases/view/113281)を参照してください。

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET信号機 2.0.2

このリリースでは修正されたバグが多数ありました。 詳細については[、2.0.2 リリースのリリースノート](https://github.com/SignalR/SignalR/releases/tag/2.0.2)を参照してください。
