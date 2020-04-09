---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: Visual Studio 2013 で ASP.NET Web プロジェクトを作成する |マイクロソフトドキュメント
author: tdykstra
description: このトピックでは、Visual Studio 2013 での Visual Studio 2013 での web プロジェクトASP.NET作成するためのオプションについて説明します。
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675683"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>Visual Studio 2013 で ASP.NET Web プロジェクトを作成する

[トム・ダイクストラ](https://github.com/tdykstra)著

> このトピックでは、更新プログラム 3 で Visual Studio 2013 でASP.NET Web プロジェクトを作成するためのオプションについて説明します。
> 
> 以前のバージョンの Visual Studio と比較した Web 開発の新機能の一部を次に示します。
> 
> - 複数のASP.NETフレームワーク (Web フォーム、MVC、および Web API)[をサポートする](#add)プロジェクトを作成するためのシンプルな UI です。
> - [ASP.NET Identity](#indauth)は、すべてのASP.NETフレームワークで同じように動作し、IIS 以外の Web ホスティング ソフトウェアで動作する新しいASP.NET メンバーシップ システムです。
> - 応答性の高いデザインとテーマ機能を提供する[Bootstrap](#bootstrap)の使用。
> - MVC 専用の Web フォームの新機能 ([自動テスト プロジェクトの作成](#testproj)や[イントラネット サイト テンプレート](#winauth)など )。
> 
> Azure クラウド サービスまたは Azure モバイル サービスの Web プロジェクトを作成する方法については[、「Azure クラウド サービスの概要と ASP.NET](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/)と[Azure Mobile Services .NET バックエンドを使用したスコア ボード アプリの作成](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)」を参照してください。

<a id="prerequisites"></a>
## <a name="prerequisites"></a>前提条件

この資料は、Visual [Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [更新プログラム 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409)がインストールされている場合に適用されます。

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>Web アプリケーション プロジェクトと Web サイト プロジェクト

ASP.NETでは、 Web*アプリケーション プロジェクト*と Web*サイト*プロジェクトの 2 種類の Web プロジェクトを選択できます。 新しい開発のための Web アプリケーション プロジェクトを推奨し、この記事は Web アプリケーション プロジェクトにのみ適用されます。 詳細については、MSDN サイト[の「Visual Studio の Web アプリケーション プロジェクトと Web サイト プロジェクト](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx)」を参照してください。

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>Web アプリケーション プロジェクトの作成の概要

次の手順は、Web プロジェクトを作成する方法を示しています。

1. **[スタート]** ページまたは [ファイル] メニューの [**新しいプロジェクト****]** をクリックします。
2. [**新しいプロジェクト**] ダイアログ ボックスの左側のウィンドウで **[Web]** をクリックし、中央のペインで **[Web アプリケーション] をASP.NET**します。

    ![[新しいプロジェクト] ダイアログ](creating-web-projects-in-visual-studio/_static/image1.png)

    左側のウィンドウで [**クラウド**] を選択して[、Azure クラウド サービス](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)[、Azure モバイル サービス](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)、または Azure [WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs)を作成できます。 このトピックでは、これらのテンプレートについては説明しません。
3. アプリケーションの正常性と使用状況を監視する場合は、右側のウィンドウで[**プロジェクトにアプリケーション インサイトを追加**] チェック ボックスをオンにします。 詳細については、「[Web アプリケーションのパフォーマンスを監視する](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/)」を参照してください。
4. プロジェクト**名**、**場所**、およびその他のオプションを指定し **、[OK]** をクリックします。

    **[新しい ASP.NET プロジェクト]** ダイアログ ボックスが表示されます。

    ![[新しいプロジェクト] ダイアログ](creating-web-projects-in-visual-studio/_static/image2.png)
5. テンプレートをクリックします。

    ![テンプレートの選択](creating-web-projects-in-visual-studio/_static/image3.png)
6. テンプレートに含まれていない追加フレームワークのサポートを追加する場合は、該当するチェック ボックスをオンにします。 (この例では、MVC や Web API を Web フォーム プロジェクトに追加できます)。

    ![フレームワークの追加](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>単体テスト プロジェクトを追加する場合は、[**単体テストの追加 ]** をクリックします。

    ![単体テストを追加する](creating-web-projects-in-visual-studio/_static/image5.png)
8. テンプレートが既定で提供する認証方法とは異なる認証方法を使用する場合は、[**認証の変更**] をクリックします。

    ![認証ボタンの構成](creating-web-projects-in-visual-studio/_static/image6.png)

    ![認証ダイアログを構成する](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>Azure で Web アプリまたは仮想マシンを作成する

Visual Studio には、Web アプリケーションをホストするための Azure サービスを簡単に操作できる機能が含まれています。 たとえば、Visual Studio IDE から次のすべての操作を行うことができます。

- アプリケーションをインターネット経由で利用できるようにする Web アプリまたは仮想マシンを作成および管理します。
- クラウドで実行されるアプリケーションによって作成されたログを表示します。
- アプリケーションがクラウドで実行されている間は、リモートでデバッグ モードで実行します。
- SQL データベースなど、他の Azure サービスを表示および管理します。

Web アプリなどの基本的なサービスを無料で含む[Azure アカウントを作成](https://www.windowsazure.com/pricing/free-trial/)し、MSDN サブスクリプション会員の場合は、追加の Azure サービスに対して毎月のクレジットを付与する特典を[アクティブ化](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/)できます。 

既定では、[**新しいASP.NET プロジェクト**] ダイアログ ボックスでは、新しい Web プロジェクト用の Web アプリまたは仮想マシンを作成できます。 新しい Web アプリまたは仮想マシンを作成しない場合は、[**クラウドでホスト**] チェック ボックスをオフにします。

![リモート リソースの作成](creating-web-projects-in-visual-studio/_static/image8.png)

チェック ボックスのキャプションは、**クラウドの Host**または **[リモート リソースの作成**] で、どちらの場合も同じ効果を持ちます。 このチェック ボックスをオンのままにすると、既定で Azure アプリ サービスに Web アプリが作成されます。 必要に応じて、ドロップダウン ボックスを使用して**仮想マシン**に変更できます。 Azure にまだサインインしていない場合は、Azure 資格情報の入力を求められます。 サインインした後、ダイアログ ボックスを使用して、Visual Studio がプロジェクト用に作成するリソースを構成できます。 次の図は、Web アプリのダイアログを示しています。仮想マシンを作成する場合は、異なるオプションが表示されます。

![Azure アプリ設定の構成](creating-web-projects-in-visual-studio/_static/image9.png)

Azure リソースの作成にこのプロセスを使用する方法の詳細については[、「Azure とASP.NETの概要](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)」および[「Visual Studio を使用した Web サイトの仮想マシンの作成](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/)」を参照してください。

この記事の残りの部分では、使用可能なテンプレートとそのオプションに関する詳細情報を提供します。 また、テンプレートで使用されるブートストラップ、レイアウト、テーマフレームワークについても紹介します。

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>Visual Studio 2013 Web プロジェクト テンプレート

テンプレートを使用して Web プロジェクトを作成します。 プロジェクト テンプレートは、新しいプロジェクトにファイルとフォルダーを作成し、NuGet パッケージをインストールし、基本的な作業アプリケーションのサンプル コードを提供できます。 テンプレートは最新の Web 標準を実装しており、ASP.NETテクノロジを使用する方法のベスト プラクティスを示し、独自のアプリケーションの作成を簡単に開始することを目的としています。

Visual Studio 2013 では、.NET 4.5 以降のバージョンの .NET Framework を対象とするプロジェクトの Web プロジェクト テンプレートに対して、次の選択肢が用意されています。

- [空のテンプレート](#empty)
- [Web フォーム テンプレート](#wf)
- [MVC テンプレート](#mvc)
- [Web API テンプレート](#webapi)
- [単一ページ アプリケーション テンプレート](#spa)
- [Azure モバイル サービス テンプレート](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [ビジュアル スタジオ 2012 テンプレート](#vs2012)

[また、Facebook テンプレート](#facebook)を提供する Visual Studio 拡張機能をインストールすることもできます。

.NET 4 を対象とするプロジェクトを作成する方法については、このトピックの[「Visual Studio 2012 テンプレート](#vs2012)」を参照してください。

モバイル クライアント用のASP.NET アプリケーションを作成する方法については[、ASP.NETのモバイル サポートを](../../../mobile/overview.md)参照してください。

<a id="empty"></a>
### <a name="empty-template"></a>空のテンプレート

空のテンプレートは、プロジェクト ファイル *(.csproj*または など) ASP.NET Web アプリの最低限のフォルダーとファイルを提供します。*)* と*Web.config*ファイル。 Web フォーム、MVC、Web API のサポートを追加するには、[**フォルダーとコア参照を追加する]** ラベルの下のチェック ボックスを使用します。

空テンプレートの場合、認証オプションは使用できません。 認証機能はサンプル アプリケーションに実装され、Empty テンプレートではサンプル アプリケーションは作成されません。

<a id="wf"></a>
### <a name="web-forms-template"></a>Web フォーム テンプレート

Web フォーム フレームワークには、UI およびデータ アクセス機能が豊富な Web サイトを迅速に構築できる次の機能が用意されています。

- ビジュアル スタジオの WYSIWYG デザイナー。
- HTML を表示するサーバー コントロールと、プロパティとスタイルを設定してカスタマイズできます。
- データ アクセスとデータ表示用の豊富なコントロールの品揃え。
- WPF などのクライアント アプリケーションをプログラムする場合と同じようにプログラムできるイベントを公開するイベント モデル。
- HTTP 要求間の状態 (データ) の自動保存。

一般に、Web フォーム アプリケーションを作成する場合、ASP.NET MVC フレームワークを使用して同じアプリケーションを作成するよりも、プログラミング作業が少なくなります。 ただし、Web フォームはアプリケーション開発を迅速に行うだけではありません。 Web フォームの上に構築された多くの複雑な商用アプリケーションやフレームワークがあります。

Web フォーム ページとページ上のコントロールは、ブラウザーに送信されるマークアップの多くを自動的に生成するため、MVC が提供する HTML をきめ細かく制御ASP.NET。 ページとコントロールを構成するための宣言型モデルを使用すると、記述する必要があるコードの量は最小限に抑えられますが、HTML と HTTP の動作の一部は隠されます。 たとえば、コントロールによって生成されるマークアップを正確に指定できるわけではありません。

Web フォーム フレームワークは、[テスト主導開発](http://en.wikipedia.org/wiki/Test-driven_development)、[懸念事項の分離](http://en.wikipedia.org/wiki/Separation_of_concerns)、[制御の反転](http://en.wikipedia.org/wiki/Inversion_of_control)、[依存性注入](http://en.wikipedia.org/wiki/Dependency_injection)などのパターンベースの開発プラクティスに対して MVC ASP.NETほど容易に役立ちません。 そのように因数を考慮してコードを記述する場合は、次の方法を使用できます。ASP.NET MVC フレームワークほど自動ではありません。 [ASP.NET Web フォーム MVP](http://webformsmvp.com/)プロジェクトは、Web フォームが提供するために構築された迅速な開発を維持しながら、懸念事項とテストの容易性を分離するためのアプローチを示しています。 Web フォーム MVP に基づいて構築されています。

Web フォーム テンプレートは、[ブートストラップ](#bootstrap)を使用してレスポンシブ デザインとテーマ機能を提供するサンプル Web フォーム アプリケーションを作成します。 次の図は、ホーム ページを示しています。

![Web フォーム テンプレート アプリのホーム ページ](creating-web-projects-in-visual-studio/_static/image10.png)

Web フォームの詳細については、「 Web フォーム[のASP.NET](https://asp.net/web-forms)」を参照してください。 Web フォーム テンプレートの機能については、「 [Visual Studio 2013 を使用した基本的な Web フォーム アプリケーションのビルド](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx)」を参照してください。

<a id="mvc"></a>
### <a name="mvc-template"></a>MVC テンプレート

ASP.NET MVC は、[テスト主導開発](http://en.wikipedia.org/wiki/Test-driven_development)、[懸念事項の分離](http://en.wikipedia.org/wiki/Separation_of_concerns)、[制御の反転](http://en.wikipedia.org/wiki/Inversion_of_control)、[依存関係の注入](http://en.wikipedia.org/wiki/Dependency_injection)など、 パターンベースの開発プラクティスを容易にするように設計されました。 フレームワークは、Web アプリケーションのビジネス ロジック層をプレゼンテーション層から分離することを推奨します。 アプリケーションをモデル (M)、ビュー (V)、およびコントローラ (C) に分割することで、MVC ASP.NET、大規模なアプリケーションでの複雑さの管理が容易になります。

ASP.NET MVC では、Web フォームよりも HTML と HTTP を直接操作できます。 たとえば、Web フォームは HTTP 要求間の状態を自動的に保持できますが、MVC で明示的にコーディングする必要があります。 MVC モデルの利点は、アプリケーションが何を行っているか、および Web 環境での動作を正確に制御できる点です。 欠点は、より多くのコードを記述する必要があるということです。

MVC は、アプリケーションのニーズに合わせてフレームワークをカスタマイズする機能をパワー開発者に提供し、拡張可能な設計されました。 さらに、ASP.NET MVC ソース コードは、OSI ライセンスの下で使用できます。

MVC テンプレートは、応答性の高いデザインとテーマ機能を提供するために[ブートストラップ](#bootstrap)を使用するサンプル MVC 5 アプリケーションを作成します。 次の図は、ホーム ページを示しています。

![MVC サンプル アプリケーション](creating-web-projects-in-visual-studio/_static/image11.png)

MVC の詳細については、「ASP.NET [MVC」](https://asp.net/mvc)を参照してください。 MVC 4 テンプレートを選択する方法については、この記事の後半の[「Visual Studio 2012 テンプレート](#vs2012)」を参照してください。

<a id="webapi"></a>
### <a name="web-api-template"></a>ウェブ API テンプレート

Web API テンプレートは、MVC に基づく API ヘルプ ページを含む、Web API に基づくサンプル Web サービスを作成します。

ASP.NET Web API は、ブラウザーやモバイル デバイスなどを含む多様なクライアントに提供できる HTTP サービスの構築が容易になるフレームワークです。 ASP.NET Web API は、.NET Framework 上で RESTful サービスを構築するための理想的なプラットフォームです。

Web API テンプレートは、サンプル Web サービスを作成します。 次の図は、ヘルプ ページの例を示しています。

![Web API ヘルプ ページ](creating-web-projects-in-visual-studio/_static/image12.png)

![GET API の Web API ヘルプ ページ](creating-web-projects-in-visual-studio/_static/image13.png)

Web API の詳細については、「 web API [ASP.NET」](https://asp.net/web-api)を参照してください。

<a id="spa"></a>
### <a name="single-page-application-template"></a>単一ページ アプリケーション テンプレート

単一ページ アプリケーション (SPA) テンプレートは、クライアント上で JavaScript、HTML 5、および[KnockoutJS](http://knockoutjs.com/)を使用するサンプル アプリケーションを作成し、サーバー上の Web API ASP.NETします。

SPA テンプレートの唯一の認証オプションは[、個別のユーザー アカウントです](#indauth)。

次の図は、SPA テンプレートが構築するサンプル アプリケーションの初期状態を示しています。

![SPA サンプル アプリケーション](creating-web-projects-in-visual-studio/_static/image14.png)

SPA テンプレートを使用してアプリケーションを作成する方法については[、「Web API - 外部認証サービス](../../../web-api/overview/security/external-authentication-services.md)」を参照してください。

シングル ページ アプリケーションASP.NET、および KnockoutJS 以外の JavaScript フレームワークを使用する追加の SPA テンプレートの詳細については、次のリソースを参照してください。

- [ASP.NET単一ページ アプリケーション](../../../single-page-application/index.md):
- [VS2013 RC の SPA テンプレートのセキュリティ機能について](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [単一ページ アプリケーション: ASP.NETを使用して、最新の応答性の高い Web アプリを構築する](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>フェイスブックテンプレート

Facebook テンプレートを[提供する Visual Studio 拡張機能を](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409)インストールできます。 このテンプレートは、Facebook Web サイト内で実行するように設計されたサンプル アプリケーションを作成します。 これは、mvc ASP.NET基づいており、リアルタイムの更新機能に Web API を使用します。

FacebookアプリケーションはFacebookサイト内で実行され、Facebookの認証に依存しているため、Facebookテンプレートの認証オプションはありません。

FacebookアプリケーションASP.NETについて詳しくは[、MVC Facebook APIの更新を](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx)参照してください。

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>ビジュアル スタジオ 2012 テンプレート

Visual Studio 2013 Web プロジェクトの作成ダイアログ ボックスには、Visual Studio 2012 で使用できるいくつかのテンプレートへのアクセスは提供されません。 これらのテンプレートのいずれかを使用する場合は、Visual Studio の [新しいプロジェクト] ダイアログ ボックスの左側のウィンドウで Visual Studio 2012 ノードをクリックします。

![ビジュアル スタジオ 2012 テンプレート](creating-web-projects-in-visual-studio/_static/image15.png)

**Visual Studio 2012**ノードでは、Visual Studio 2013 の既定のテンプレートの一覧でアクセスできない次の Web テンプレートを選択できます。

- ASP.NET MVC 4 Web アプリケーション
- ASP.NET 動的データ エンティティ Web アプリケーション
- AJAX サーバー コントロールをASP.NETします。
- aJAX サーバー コントロール エクステンダASP.NET
- ASP.NET サーバー コントロール

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>Visual Studio 2013 Web プロジェクト テンプレートのブートストラップ

Visual Studio 2013 プロジェクト テンプレートは[、ブートストラップ](http://getbootstrap.com/)、レイアウト、および Twitter によって作成されたテーマ フレームワークを使用します。 ブートストラップはCSS3を使用してレスポンシブなデザインを提供するため、レイアウトはさまざまなブラウザウィンドウサイズに動的に適応できます。 たとえば、ワイド ブラウザ ウィンドウでは、Web フォーム テンプレートで作成されたホーム ページは次の図のようになります。

![Web フォーム テンプレート アプリのホーム ページ](creating-web-projects-in-visual-studio/_static/image16.png)

ウィンドウを狭くし、水平方向に配置された列を垂直方向に移動します。

![ブートストラップ縦列配置](creating-web-projects-in-visual-studio/_static/image17.png)

ウィンドウをもう少し狭くすると、水平方向のトップ メニューがアイコンに変わり、クリックして垂直方向のメニューに展開できます。

![ブートストラップメニューアイコン](creating-web-projects-in-visual-studio/_static/image18.png)

![ブートストラップの垂直メニュー](creating-web-projects-in-visual-studio/_static/image19.png)

また、ブートストラップのテーマ機能を使用して、アプリケーションの外観の変化に簡単に影響を与えることができます。 たとえば、テーマを変更するには、次の手順を実行します。

1. ブラウザで、 に[http://Bootswatch.com](http://Bootswatch.com)進み、テーマを選択して 、[**ダウンロード**] をクリックします。 (これはデフォルトで*bootstrap.min.css*をダウンロードします。 CSS コードを調べる場合は、縮小版の代わりに*bootstrap.css*を取得します。
2. ダウンロードした CSS ファイルの内容をコピーします。
3. Visual Studio で、*コンテンツ*フォルダーに*bootstrap-theme.css*という名前の新しい**スタイル シート**ファイルを作成し、ダウンロードした CSS コードを貼り付けます。
4. *アプリケーション\_の開始/バンドル.config*を開き、*ブートストラップ.css*を*ブートストラップテーマ.css*に変更します。

プロジェクトを再度実行すると、アプリケーションの外観が新たに表示されます。 次の図は、アメリアテーマの効果を示しています。

![ブートストラップアメリアのテーマ](creating-web-projects-in-visual-studio/_static/image20.png)

多くのブートストラップテーマは、無料とプレミアムの両方のバージョン、利用可能です。 ブートストラップには、[ドロップダウン](http://twitter.github.io/bootstrap/components.html#dropdowns)、[ボタン グループ](http://twitter.github.io/bootstrap/components.html#buttonGroups)、アイコン など、さまざまな UI コンポーネントも用意[されています](http://twitter.github.io/bootstrap/base-css.html#images)。 ブートストラップの詳細については、ブートストラップ[サイトを](http://twitter.github.io/bootstrap/)参照してください。

Visual Studio で Web フォーム デザイナーを使用する場合は、デザイナーが CSS3 をサポートしていないので、ブートストラップ テーマや応答性レイアウトの変更のすべての効果が正確に表示されない点に注意してください。 ただし、Web フォーム ページは、ブラウザで表示すると正しく表示されます。

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>追加フレームワークのサポートの追加

テンプレートを選択すると、テンプレートで使用されるフレームワークのチェックボックスが自動的にオンになります。 たとえば **、Web フォーム**テンプレートを選択した場合は **、[Web フォーム**] チェック ボックスがオンになり、オフにできません。

![テンプレートの選択](creating-web-projects-in-visual-studio/_static/image21.png)

![フレームワークの追加](creating-web-projects-in-visual-studio/_static/image22.png)

プロジェクトの作成時にそのフレームワークのサポートを追加するために、テンプレートに含まれていないフレームワークのチェック ボックスをオンにできます。 たとえば、MVC テンプレートを選択したときに Web フォーム*の .aspx*ページを使用できるようにするには **、[Web フォーム**] チェック ボックスをオンにします。 または、Web フォーム テンプレートを使用しているときに MVC を有効にするには **、[MVC]** チェック ボックスをオンにします。 フレームワークを追加すると、デザイン時と実行時のサポートが可能になります。 たとえば、Mvc サポートを Web フォーム プロジェクトに追加すると、コントローラーとビューをスキャフォールディングできます。

Web フォームと MVC をプロジェクトに組み合わせて Web フォームで[フレンドリ URL を](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)有効にした場合、1 つの URL に複数のターゲットが存在する予期しないルーティングの問題が発生する可能性があります。 最初に定義されたルートが優先されます。 たとえば、`Home`コントローラーと*Home.aspx*ページがある場合 *、RouteConfig.cs*`Home`で`http://contoso.com/home``MapRoute``EnableFriendlyUrls`メソッドを呼び出す前にメソッドを呼び出すと、URL は*Home.aspx*に移動`MapRoute`します`EnableFriendlyUrls`。

フレームワークを追加しても、サンプル アプリケーション機能は追加されません。 たとえば、MVC テンプレートを選択したときに Web フォーム サポートを追加した場合 *、Default.aspx*ホーム ページ ファイルは作成されません。 フレームワークをサポートするために必要なフォルダー、ファイル、および参照のみが追加されます。 そのため、フレームワークを追加しても認証オプションは変更されません。 たとえば、空のテンプレートを選択し、Web フォームまたは MVC サポートを追加する場合は、**認証の構成**ボタンは無効のままです。

次のセクションでは、各チェック ボックスの効果について簡単に説明します。

### <a name="add-web-forms-support"></a>Web フォームのサポートの追加

空の*アプリ\_データ*と*モデル*フォルダーと*Global.asax*ファイルを作成します。 これらは空のテンプレート以外のすべてのテンプレートによって既に作成されているので、[Web フォーム] チェック ボックスをオンにしても他のテンプレートに違いはありません。

Web フォーム テンプレートでは既定でフレンドリ URL が有効になりますが、[Web フォーム] チェック ボックスをオンにして他のテンプレートに Web フォーム サポートを追加すると、自動的に有効になりません。

### <a name="add-mvc-support"></a>MVC サポートの追加

MVC、Razor、および WebPages NuGet パッケージをインストールし、空の*アプリ\_データ*、*コントローラー*、*モデル*、*およびビュー*フォルダーを作成し *、RouteConfig.cs*ファイルを含む*アプリ\_のスタート*フォルダーを作成し *、Global.asax*ファイルを作成します。

### <a name="add-web-api-support"></a>Web API サポートの追加

WebApi と Newtonsoft.Json NuGet パッケージをインストールし、空の*アプリケーション\_データ*、*コントローラー*、*およびモデル*フォルダーを作成し *、WebApiConfig.cs*ファイルを含む*アプリ\_のスタート*フォルダーを作成し *、Global.asax*ファイルを作成します。

<a id="auth"></a>
## <a name="authentication-methods"></a>認証方法

Visual Studio 2013 には、Web フォーム、MVC、および Web API テンプレートに対して、次のような認証オプションが用意されています。

- [認証なし](#noauth)
- [個々のユーザー アカウント](#indauth)(以前は ASP.NET メンバーシップと呼ばれていたASP.NET ID)
- [組織アカウント](#orgauth)(Windows サーバーアクティブ ディレクトリまたは Azure アクティブ ディレクトリ)
- [Windows 認証](#winauth)(イントラネット)

![認証ダイアログを構成する](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>[認証なし]

**[認証なし**] を選択した場合、サンプル アプリケーションには、ログイン用の Web ページ、ログインしているユーザーを示す UI、メンバーシップ データベースのエンティティ クラス、メンバーシップ データベースの接続文字列が含まれなくなります。

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>個々のユーザー アカウント

**[個別のユーザー アカウント**] を選択すると、サンプル アプリケーションは、ユーザー認証に ASP.NET ID (以前はASP.NET メンバーシップ) を使用するように構成されます。 ASP.NETアイデンティティを使用すると、ユーザーはサイト上でユーザー名とパスワードを作成したり、Facebook、Google、Microsoftアカウント、Twitterなどのソーシャルプロバイダにサインインしたりして、アカウントを登録できます。 ASP.NET ID のユーザー プロファイルの既定のデータ ストアは SQL Server LocalDB データベースであり、運用サイトの SQL Server または Azure SQL データベースに展開できます。

Visual Studio 2013 では、これらの機能は Visual Studio 2012 と同じですが、ASP.NET メンバーシップ システムの基になるコードが書き換えられました。 新しいコード ベースの利点は次のとおりです。

- 新しいメンバーシップ システムは、ASP.NET フォーム認証モジュールではなく[OWIN](http://owin.org/)に基づいています。 つまり、IIS で Web フォームまたは MVC を使用している場合でも、Web API や SignalR を自己ホストしている場合でも、同じ認証メカニズムを使用できます。
- 新しいメンバーシップ データベースは Entity Framework コード ファーストによって管理され、すべてのテーブルは、変更できるエンティティ クラスによって表されます。 つまり、データベース スキーマとプロファイル関連の Web UI を独自のニーズに合わせて簡単にカスタマイズでき、コード優先移行を使用して更新プログラムを簡単に展開できます。

新しいメンバーシップ システムは新しいテンプレートに自動的に実装され、.NET 4.5 以降を対象とする任意のプロジェクトに手動で実装できます。

ASP.NETアイデンティティは、主に外部顧客向けのインターネットWebサイトを作成する場合に適しています。 組織で Active Directory または Office 365 を使用していて、従業員とビジネス パートナーのシングル サインオンを有効にするプロジェクトを作成する場合は、[**組織アカウント**] オプションが適しています。

個別ユーザー アカウント オプションの詳細については、次のリソースを参照してください。

- [www.asp.net/identity](../../../identity/index.md). ASP.NETのウェブサイト上ASP.NETIDに関するドキュメント。
- [フェイスブックとグーグルOAuth2とOpenIDサインオンを使用してASP.NETMVC 5アプリを作成](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)します。 ユーザー プロファイル データをカスタマイズする方法も示します。
- [Web API - 外部認証サービス](../../../web-api/overview/security/external-authentication-services.md)
- [Visual Studio 2013 でASP.NET アプリケーションに外部ログインを追加する](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>組織アカウント

**[組織アカウント**] を選択した場合、サンプル アプリケーションは、Azure アクティブ ディレクトリ (Azure AD(Office 365 を含む) または Windows Server アクティブ ディレクトリのユーザー アカウントに基づいて、認証に Windows ID 基盤 (WIF) を使用するように構成されます。 詳細については、このトピックの「[組織アカウント認証オプション](#orgauthoptions)」を参照してください。

<a id="winauth"></a>
### <a name="windows-authentication"></a>Windows 認証

**[Windows 認証**] を選択した場合、サンプル アプリケーションは、認証に Windows 認証 IIS モジュールを使用するように構成されます。 アプリケーションは、Windows にログインしている Active ディレクトリまたはローカル コンピュータ アカウントのドメインとユーザー ID を表示しますが、ユーザー登録やログイン UI は含みません。 このオプションは、イントラネット Web サイトを対象としています。

または、[組織アカウント] の下の[[オンプレミス] オプション](#orgauthonprem)を選択して、AD 認証を使用するイントラネット サイトを作成することもできます。 オンプレミス オプションでは、Windows 認証モジュールの代わりに Windows ID 基盤 (WIF) が使用されます。 オンプレミス オプションを設定するには追加の手順が必要ですが、WIF は Windows 認証モジュールでは使用できない機能を有効にします。 たとえば、WIF を使用すると、Active Directory でアプリケーション アクセスを構成し、ディレクトリ データを照会できます。

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>組織アカウント認証オプション

**[認証の構成]** ダイアログボックスには、Azure アクティブ ディレクトリ (Office 365 を含む Azure AD) または Windows サーバー アクティブ ディレクトリ (AD) アカウント認証のいくつかのオプションが用意されています。

- [クラウド - 単一組織](#orgauthsingle)(Azure AD、または Azure AD とのディレクトリ統合を使用した AD)
- [クラウド - 複数の組織](#orgauthmulti)(Azure AD、または Azure AD とのディレクトリ統合を使用した AD)
- [オンプレミス](#orgauthonprem)(AD)

Azure AD オプションのいずれかを試してみてもアカウントをまだ持っていない場合は、[こちらをクリックして Azure AD アカウントにサインアップ](https://go.microsoft.com/fwlink/?LinkId=309942)します。

> [!NOTE]
> いずれかの Azure AD オプションを選択した場合、プロジェクトにはデータベースが必要であり、Azure AD テナントのグローバル管理者アカウントにサインインする必要があります。 Azure AD テナントの管理アクセス許可admin@contoso.onmicrosoft.comを持つ組織アカウント (など) の名前とパスワードを入力します。
> 
> **サインイン ダイアログ ボックスに Microsoft アカウントの資格情報 (contoso@hotmail.comたとえば) を入力しないでください。**

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>クラウド - 単一組織認証

![単一組織認証](creating-web-projects-in-visual-studio/_static/image24.png)

1 つの Azure AD[テナント](https://technet.microsoft.com/library/jj573650.aspx)で定義されているユーザー アカウントの認証を有効にする場合は、このオプションを選択します。 たとえば、サイトがcontoso.comされ、contoso.onmicrosoft.comテナントにいる Contoso 社の従業員が利用できるようになります。 他のテナントのユーザーがアプリケーションにアクセスできるように Azure AD を構成することはできません。

#### <a name="domain"></a>Domain

アプリケーションをセットアップする Azure AD ドメインを入力します。 `contoso.onmicrosoft.com` [カスタム ドメイン](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/)などがある場合は、 `contoso.com` `contoso.onmicrosoft.com`の代わりに、 を入力できます。

#### <a name="access-level"></a>アクセス レベル

Graph API を使用してディレクトリ情報の照会または更新を行う必要がある場合は、[**シングル サインオン]、[ディレクトリ データの読み取り]、** または **[シングル サインオン]、[ディレクトリ データの読み取りと書き込み**] を選択します。 それ以外の場合は、[**シングル サインオン**] を選択します。 詳細については、「アプリケーション[アクセス レベル](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels)」および[グラフ API を使用した Azure AD のクエリに関するページを](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx)参照してください。

#### <a name="application-id-uri"></a>アプリケーション ID URI

既定では、テンプレートは、プロジェクト名を Azure AD ドメインに追加することによって、アプリケーション ID URI を作成します。 たとえば、プロジェクト名が`Example`で、ドメインが が`contoso.onmicrosoft.com`の場合、アプリケーション`https://contoso.onmicrosoft.com/Example`ID URI は になります。 アプリケーション ID URI を手動で指定する場合**は、[その他のオプション]** セクションを展開し、テキスト ボックスにアプリケーション ID URI を入力します。 アプリケーション ID URI は`https://`で始まる必要があります。

既定では、Azure AD で既にプロビジョニングされているアプリケーションの URI が、Visual Studio がプロジェクトに使用しているアプリケーション ID URI と同じ場合、プロジェクトは新しいアプリケーションをプロビジョニングする代わりに既存のアプリケーションに接続されます。 その場合に新しいアプリケーションをプロビジョニングする場合は、[**同じ ID のアプリケーション エントリが既に存在する場合は上書き**する] チェック ボックスをオフにします。

**[上書き**] チェック ボックスがオフの場合、Visual Studio は、同じアプリケーション ID URI を持つ既存のアプリケーションを検出すると、使用する URI に番号を追加して新しい URI を作成します。 たとえば、プロジェクト名が`Example`、テキスト ボックスを空白のままにし、[**上書き**] チェック ボックスをオフにし、Azure AD テナントに`https://contoso.onmicrosoft.com/Example`URI を持つアプリケーションが既に存在しているとします。 その場合、新しいアプリケーションは、 のような`https://contoso.onmicrosoft.com/Example_20130619330903`アプリケーション ID URI でプロビジョニングされます。

#### <a name="provisioning-the-application-in-azure-ad"></a>Azure AD でのアプリケーションのプロビジョニング

Azure AD でアプリケーションをプロビジョニングしたり、プロジェクトを既存のアプリケーションに接続したりするために、Visual Studio にはドメインのグローバル管理者の資格情報が必要です。 [**認証の構成**] ダイアログ ボックスで **[OK] を**クリックすると、指定したドメインのグローバル管理者のユーザー名とパスワードを入力するように求められます。 後で、[**新しいASP.NET プロジェクト**] ダイアログ で [**プロジェクトの作成**] をクリックすると、Azure AD でアプリケーションがプロビジョニングされます。 このプロセスの一部として、Visual Studio は、作成後 1 年で期限切れになるクライアント シークレット値を Web.config ファイルに埋め込むことに注意してください。

**クラウド - 単一組織**認証を使用するアプリケーションを作成する方法については、次のリソースを参照してください。

- [Azure 認証](../2012/windows-azure-authentication.md)
- [Azure AD を使用した Web アプリケーションへのサインオンの追加](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [Azure Active Directory を使った ASP.NET アプリの開発](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [Azure AD とマイクロソフト OWIN コンポーネントを使用したセキュリティASP.NET Web API](https://msdn.microsoft.com/magazine/dn463788.aspx)

チュートリアルはまだ Visual Studio 2013 用に更新されていません。チュートリアルの一部は、Visual Studio 2013 で自動化されています手動で行う指示します。

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>クラウド - マルチ組織認証

![複数組織認証](creating-web-projects-in-visual-studio/_static/image25.png)

複数の Azure AD テナントで定義されているユーザー アカウントの認証を有効にする場合は、このオプション[を](https://technet.microsoft.com/library/jj573650.aspx)選択します。 たとえば、サイトがcontoso.comされ、contoso.onmicrosoft.comテナントにいる Contoso 社の従業員と、fabrikam.onmicrosoft.comテナントにいる Fabrikam 社の従業員が利用できるようになります。

入力した設定とアプリケーションのプロビジョニング手順は、[単一組織認証](#orgauthsingle)と似ています。

**クラウドマルチ組織**認証を使用するアプリケーションを作成する方法については、次のリソースを参照してください。

- [Azure アクティブ ディレクトリとの簡単な&amp;Web アプリ統合、ASP.NETアクティブ](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx)ディレクトリ チームブログの Visual Studio。
- [Azure AD チュートリアルを使用してマルチテナント Web アプリケーションを開発](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx)する。 チュートリアルはまだ Visual Studio 2013 用に更新されていません。チュートリアルで手動で行うように指示するもののいくつかは、Visual Studio 2013 で自動化されています。
- [サインインする前に、アプリASP.NET複数の組織でサインアップする必要があります](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/)。 複数組織認証を使用するプロジェクトを作成する際に発生する一般的な問題を解決する方法を説明する Vittorio Bertocci のブログ。

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>オンプレミスの組織認証

![オンプレミスの組織認証](creating-web-projects-in-visual-studio/_static/image26.png)

Windows サーバーのアクティブ ディレクトリ (AD) で定義されているユーザー アカウントの認証を有効にする場合、Azure AD を使用しない場合は、このオプションを選択します。 このオプションを使用して、イントラネット サイトまたはインターネット サイトを作成できます。 インターネット サイトの場合は、Active Directory フェデレーション サービス (ADFS) を使用して AD へのアクセスを提供します。 詳細については、「 [Visual Studio 2013 でのオンプレミス組織認証オプション (ADFS) ASP.NETを使用](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)する 」を参照してください。

イントラネット サイトの場合、このオプションの代わりに[Windows 認証](#winauth)を選択することもできます。 Windows 認証オプションでは、メタデータ ドキュメントの URL を指定する必要はありません。 ただし、Windows 認証では、Active Directory でのアプリケーション アクセスの制御やディレクトリ データのクエリを行う機能はありません。

#### <a name="on-premises-authority"></a>オンプレミスの機関

メタデータ ドキュメントを指す URL を入力します。 メタデータ文書には、権限の座標が含まれています。 アプリケーションは、これらの座標を使用して、Web サインオン フローを駆動します。

#### <a name="application-id-uri"></a>アプリケーション ID URI

AD がこのアプリケーションを識別するために使用できる一意の URI を指定するか、または Visual Studio で作成できるように空白のままにします。

<a id="nextsteps"></a>
## <a name="next-steps"></a>次のステップ

このドキュメントでは、Visual Studio 2013 で新しいASP.NET Web プロジェクトを作成するための基本的なヘルプを提供しています。 Web 開発用の Visual Studio の使用の[https://www.asp.net/visual-studio/](../../index.md)詳細については、を参照してください。
