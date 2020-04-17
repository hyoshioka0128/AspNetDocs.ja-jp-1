---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
title: 異なるバージョンの IIS (C#) でのASP.NET MVC の使用 |マイクロソフトドキュメント
author: rick-anderson
description: このチュートリアルでは、さまざまなバージョンのインターネット インフォメーション サービスで、mvc と URL ルーティングASP.NETを使用する方法について説明します。 あなたは異なる戦略を学びます.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: b0cf4a34-2c1d-4717-bb54-ff029e722990
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
msc.type: authoredcontent
ms.openlocfilehash: 8c239c3c7cbbaae5d9c5e4dd91dc66ff4e98bcfb
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542080"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-c"></a>さまざまなバージョンの IIS と共に ASP.NET MVC を使用する (C#)

[マイクロソフト](https://github.com/microsoft)

> このチュートリアルでは、さまざまなバージョンのインターネット インフォメーション サービスで、mvc と URL ルーティングASP.NETを使用する方法について説明します。 IIS 7.0 (クラシック モード)、IIS 6.0、および以前のバージョンの IIS で MVC ASP.NET使用するためのさまざまな戦略を学習します。

mvc フレームワークASP.NETは、ブラウザーの要求をコントローラー アクションにルーティングするASP.NETルーティングに依存します。 ASP.NET ルーティングを利用するには、Web サーバーで追加の構成手順を実行する必要があります。 このすべては、インターネット インフォメーション サービス (IIS) のバージョンと、アプリケーションの要求処理モードによって異なります。

さまざまなバージョンの IIS の概要を次に示します。

- IIS 7.0 (統合モード) - ASP.NET ルーティングを使用するために特別な構成は必要ありません。
- IIS 7.0 (クラシック モード) - ASP.NET ルーティングを使用するには、特別な構成を実行する必要があります。
- IIS 6.0 以下 - ASP.NET ルーティングを使用するには、特別な構成を実行する必要があります。

IIS の最新バージョンはバージョン 7.5 (Win7) です。 IIS の IIS 7 は、Windows Server 2008 と VISTA/SP1 以降に含まれています。 また、ホーム ベーシック (を参照) 以外の Vista オペレーティング システムの任意の[https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)バージョンに IIS 7.0 をインストールすることもできます。

IIS 7.0 では、要求を処理するための 2 つのモードがサポートされています。 統合モードまたはクラシック モードを使用できます。 統合モードで IIS 7.0 を使用する場合は、特別な構成手順を実行する必要はありません。 ただし、クラシック モードで IIS 7.0 を使用する場合は、追加の構成を実行する必要があります。

Windows サーバー 2003 には、IIS 6.0 が含まれています。 Windows Server 2003 オペレーティング システムを使用している場合、IIS 6.0 を IIS 7.0 にアップグレードすることはできません。 IIS 6.0 を使用する場合は、追加の構成手順を実行する必要があります。

Windows XP プロフェッショナルには、IIS 5.1 が含まれています。 IIS 5.1 を使用する場合は、追加の構成手順を実行する必要があります。

最後に、Windows 2000 およびマイクロソフトの Windows 2000 プロフェッショナルには、IIS 5.0 が含まれています。 IIS 5.0 を使用する場合は、追加の構成手順を実行する必要があります。

## <a name="integrated-versus-classic-mode"></a>統合モードとクラシックモード

IIS 7.0 では、統合とクラシックの 2 つの異なる要求処理モードを使用して要求を処理できます。 統合モードは、より良いパフォーマンスとより多くの機能を提供します。 クラシック モードは、以前のバージョンの IIS との下位互換性を保つために用意されています。

要求処理モードは、アプリケーション プールによって決定されます。 アプリケーションに関連付けられているアプリケーション プールを決定することにより、特定の Web アプリケーションで使用されている処理モードを特定できます。 次の手順に従います。

1. インターネット インフォメーション サービス マネージャを起動する
2. [接続] ウィンドウで、アプリケーションを選択します。
3. [操作] ウィンドウで、[**基本設定]** リンクをクリックして [アプリケーションの編集] ダイアログ ボックスを開きます (図 1 を参照)。
4. 選択したアプリケーション プールをメモします。

既定では、IIS は、2 つのアプリケーション プールをサポートするように構成されています:**既定のアプリケーション プール**と**従来の .NET アプリケーション プール**。 DefaultAppPool が選択されている場合、アプリケーションは統合要求処理モードで実行されています。 [従来の .NET アプリケーション プール] が選択されている場合、アプリケーションはクラシック要求処理モードで実行されています。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)

**図1**: リクエスト処理モードを検出する([フルサイズの画像を表示する をクリック](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png))

[アプリケーションの編集] ダイアログ ボックスで要求処理モードを変更できることに注意してください。 [選択] ボタンをクリックし、アプリケーションに関連付けられているアプリケーション プールを変更します。 ASP.NETアプリケーションをクラシックモードから統合モードに変更する場合は、互換性の問題があることを認識してください。 詳細については、次の記事を参照してください。

- Windows Vista および Windows Server 2008 で ASP.NET 1.1 を IIS 7.0 にアップグレードする --[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)
- ASP.NET IIS 7.0 との統合 -[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

ASP.NETアプリケーションが DefaultAppPool を使用している場合は、ASP.NET ルーティング (ASP.NET したがって MVC) を動作させるために追加の手順を実行する必要はありません。 ただし、ASP.NET アプリケーションが従来の .NET AppPool を使用するように構成されている場合は、読み取り続ける必要があります。

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>旧バージョンの IIS で ASP.NET MVC を使用する

IIS 7.0 より古いバージョンの IIS で MVC ASP.NET使用する必要がある場合、またはクラシック モードで IIS 7.0 を使用する必要がある場合は、2 つのオプションがあります。 まず、ファイル拡張子を使用するようにルート テーブルを変更できます。 たとえば、/Store/Details などの URL を要求する代わりに、/Store.aspx/Details などの URL を要求します。

2 つ目のオプションは、*ワイルドカード スクリプト マップ*と呼ばれるものを作成することです。 ワイルドカード スクリプト マップを使用すると、すべての要求をASP.NET フレームワークにマップできます。

Web サーバーにアクセスできない場合 (たとえば、ASP.NET MVC アプリケーションがインターネット サービス プロバイダーによってホストされている場合) は、最初のオプションを使用する必要があります。 URL の外観を変更する必要がない場合、Web サーバーへのアクセス権がある場合は、2 番目のオプションを使用できます。

各オプションについては、以下のセクションで詳しく説明します。

## <a name="adding-extensions-to-the-route-table"></a>ルート テーブルへの拡張機能の追加

以前のバージョンの IIS でASP.NETルーティングを使用する最も簡単な方法は、Global.asax ファイル内のルート テーブルを変更することです。 リスト 1 のデフォルトおよび変更されていない Global.asax ファイルは、デフォルト ルートという名前のルートを 1 つ設定します。

**リスト 1 - グローバル.asax (未変更)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample1.cs)]

リスト 1 で構成された既定のルートでは、次のような URL をルーティングできます。

/ホーム/インデックス

/製品/詳細/3

/Product

残念ながら、古いバージョンの IIS では、これらの要求はASP.NET フレームワークに渡されません。 したがって、これらの要求はコントローラーにルーティングされません。 たとえば、URL /Home/Index のブラウザ要求を行うと、図 2 のエラー ページが表示されます。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)

**図2**: 404 Not Found エラーが表示される ([フルサイズの画像を表示する をクリック](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png))

古いバージョンの IIS では、特定の要求がASP.NET フレームワークにしかマップされません。 要求は、正しいファイル拡張子を持つ URL に対する要求である必要があります。 たとえば、/SomePage.aspx の要求は、ASP.NET フレームワークにマップされます。 ただし、/SomePage.htm の要求は行われません。

したがって、ルーティングASP.NETを動作させるには、ASP.NETフレームワークにマップされたファイル拡張子が含まれるようにデフォルトルートを変更する必要があります。

これは、 という名前`registermvc.wsf`のスクリプトを使用して行います。 MVC 1 のリリース ASP.NET に`C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`含まれていましたが、ASP.NET 2 以降、このスクリプトは ASP.NET 先物に移動[http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)されました。

このスクリプトを実行すると、新しい .mvc 拡張機能が IIS に登録されます。 mvc 拡張機能を登録した後、ルートが .mvc 拡張子を使用するように Global.asax ファイル内のルートを変更できます。

リスト 2 で変更された Global.asax ファイルは、古いバージョンの IIS で動作します。

**リスト 2 - グローバル.asax (拡張機能で変更)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample2.cs)]

**重要**: Global.asax ファイルを変更した後に、ASP.NET MVC アプリケーションを再度ビルドすることを忘れないでください。

リスト 2 の Global.asax ファイルには、2 つの重要な変更があります。 Global.asax で定義されたルートが 2 つあります。 既定のルートの URL パターン(最初のルート)は次のようになります。

{コントローラー}.mvc/{アクション}/{id}

mvc 拡張機能を追加すると、ASP.NETルーティング モジュールがインターセプトするファイルの種類が変更されます。 この変更により、ASP.NET MVC アプリケーションは、次のような要求をルーティングするようになりました。

/ホーム.mvc/インデックス/

/製品.mvc/詳細/3

/製品.mvc/

2 番目のルートルートは新しいルートです。 ルート ルートのこの URL パターンは空の文字列です。 このルートは、アプリケーションのルートに対して行われた要求を照合するために必要です。 たとえば、ルート ルートは次のような要求と一致します。

[http://www.YourApplication.com/](http://www.YourApplication.com/)

ルート テーブルにこれらの変更を加えた後、アプリケーション内のすべてのリンクがこれらの新しい URL パターンと互換性があることを確認する必要があります。 つまり、すべてのリンクに .mvc 拡張子が含まれているか確認してください。 Html.ActionLink() ヘルパー メソッドを使用してリンクを生成する場合は、変更を加える必要はありません。

registermvc.wcf スクリプトを使用する代わりに、手作業でASP.NET フレームワークにマップされている IIS に新しい拡張機能を追加できます。 新しい拡張子を自分で追加する場合は、[**ファイルが存在することを確認**する] チェック ボックスがオンになっていることを確認します。

## <a name="hosted-server"></a>ホストされるサーバー

Web サーバーにアクセスできる必要はありません。 たとえば、インターネット ホスティング プロバイダーを使用して ASP.NET MVC アプリケーションをホストしている場合、必ずしも IIS にアクセスできるわけではありません。

その場合は、ASP.NETフレームワークにマップされている既存のファイル拡張子のいずれかを使用する必要があります。 ASP.NETにマップされたファイル拡張子の例には、.aspx、.axd、および .ashx 拡張子が含まれます。

たとえば、リスト 3 で変更された Global.asax ファイルでは、.mvc 拡張子ではなく .aspx 拡張子が使用されます。

**リスト 3 - Global.asax (.aspx 拡張子で変更)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample3.cs)]

リスト 3 の Global.asax ファイルは、.mvc 拡張子の代わりに .aspx 拡張子を使用する点を除いて、以前の Global.asax ファイルとまったく同じです。 .aspx 拡張機能を使用するために、リモート Web サーバーでセットアップを実行する必要はありません。

## <a name="creating-a-wildcard-script-map"></a>ワイルドカード スクリプト マップの作成

ASP.NET MVC アプリケーションの URL を変更する必要がない場合、Web サーバーにアクセスできる場合は、追加のオプションがあります。 すべての要求を web サーバーにマップするワイルドカード スクリプト マップを作成ASP.NETフレームワーク。 このようにすると、既定の ASP.NET MVC ルート テーブルを IIS 7.0 (クラシック モード) または IIS 6.0 で使用できます。

このオプションを使用すると、IIS は Web サーバーに対して行われた要求をすべてインターセプトすることに注意してください。 これには、イメージ、従来の ASP ページ、および HTML ページの要求が含まれます。 したがって、ワイルドカード スクリプト マップを有効にしてASP.NETすると、パフォーマンスに影響が生じます。

IIS 7.0 のワイルドカード スクリプト マップを有効にする方法を次に示します。

1. [接続] ウィンドウでアプリケーションを選択します。
2. **[機能]** ビューが選択されていることを確認します。
3. [**ハンドラー マッピング**] ボタンをダブルクリックします。
4. [**ワイルドカード スクリプト マップの追加**] リンクをクリックします (図 3 を参照)。
5. aspnet\_isapi.dll ファイルへのパスを入力します (このパスは PageHandlerFactory スクリプト マップからコピーできます)
6. 名前 MVC を入力してください
7. **[OK]** ボタンをクリックします。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)

**図 3**: IIS 7.0 を使用したワイルドカード スクリプト マップの作成 ([フルサイズの画像を表示する をクリック](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png))

IIS 6.0 でワイルドカード スクリプト マップを作成するには、次の手順を実行します。

1. Web サイトを右クリックし、[プロパティ] を選択します。
2. **[ホーム ディレクトリ**] タブを選択します。
3. [**構成]** ボタン
4. [マッピング] タブ**を選択します。**
5. [**挿入**] ボタンをクリックします (図 4 を参照してください)。
6. aspnet\_isapi.dll へのパスを実行可能ファイルのフィールドに貼り付けます (.aspx ファイルのスクリプト マップからこのパスをコピーできます)。
7. [**ファイルが存在することを確認する**] チェック ボックスをオフにします。
8. **[OK]** ボタンをクリックします。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)

**図 4**: IIS 6.0 でワイルドカード スクリプト マップを作成する ([フルサイズの画像を表示する をクリック](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png))

ワイルドカード スクリプト マップを有効にした後、Global.asax ファイル内のルート テーブルを変更してルート ルートを含める必要があります。 それ以外の場合は、アプリケーションのルート ページを要求するときに、図 5 のエラー ページが表示されます。 修正された Global.asax ファイルは、リスト 4 で使用できます。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)

**図5**:ルートルートの欠落エラー([フルサイズの画像を表示するをクリック](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png))

**リスト 4 - グローバル.asax (ルートルートで変更)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample4.cs)]

IIS 7.0 または IIS 6.0 のワイルドカード スクリプト マップを有効にすると、次のような既定のルート テーブルで動作する要求を作成できます。

/

/ホーム/インデックス

/製品/詳細/3

/Product

## <a name="summary"></a>まとめ

このチュートリアルの目的は、旧バージョンの IIS (またはクラシック モードで IIS 7.0) を使用するときに、mvc ASP.NET使用する方法を説明することです。 以前のバージョンの IIS で作業する ASP.NET ルーティングを取得する 2 つの方法について説明しました: 既定のルート テーブルを変更する、またはワイルドカード スクリプト マップを作成します。

最初のオプションでは、ASP.NET MVC アプリケーションで使用される URL を変更する必要があります。 この最初のオプションの非常に大きな利点の 1 つは、ルート テーブルを変更するために Web サーバーにアクセスする必要がなされないことです。 つまり、インターネット ホスティング会社と ASP.NET MVC アプリケーションをホストしている場合でも、この最初のオプションを使用できます。

2 番目のオプションは、ワイルドカード スクリプト マップを作成することです。 この 2 番目のオプションの利点は、URL を変更する必要がなされないことです。 この 2 番目のオプションの欠点は、ASP.NET MVC アプリケーションのパフォーマンスに影響を与える可能性がある点です。

> [!div class="step-by-step"]
> [次へ](using-asp-net-mvc-with-different-versions-of-iis-vb.md)
