---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Visual Studio ASP.NET を使用した Web ページ (Razor) のプログラミング |マイクロソフトドキュメント
author: Rick-Anderson
description: この付録では、Visual Studio 2010 または Visual Web 開発者 2010 Express を使用して、Razor 構文を使用して Web ページASP.NETプログラムする方法について説明します。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542899"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>Visual Studio を使用した Web ページ (Razor) ASP.NETプログラミング

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、Visual Studio または Visual Web 開発者用エクスプレスを使用して、Web ページ (Razor) の Web サイト ASP.NET プログラムする方法について説明します。
>
> 学習内容
>
> - Visual Studio のバージョンで Web ページを使用して作業ASP.NET必要なもの (どちらかといえば)
> - ビジュアル Web 開発者 2010 Express に ASP.NET Web ページのサポートを追加する方法。
> - Visual Studio の機能を使用して、IntelliSense やデバッガーを含むASP.NETの Razor ページを操作する方法。
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>チュートリアルで使用するソフトウェアバージョン
>
>
> - ASP.NET ウェブページ (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>
>
> このチュートリアルは、Web ページ 2、Visual Studio 2012、Visual Studio 2010、および WebMatrix 2 ASP.NETでも動作します。

WebMatrix やその他 ASP.NETの多くのコード エディターを使用して、Web ページを Razor 構文でプログラミングできます。 また、多くの種類のアプリケーション (Web サイトだけでなく) を作成するための強力なツール セットを提供する、フル機能の統合開発環境 (IDE) である Microsoft Visual Studio を使用することもできます。 ASP.NET の Razor ページを操作するには[、Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)を使用できます。

ASP.NET Razor Web ページを使用したプログラミングに Visual Studio が提供する、特に便利な 2 つの機能は次のとおりです。

- *インテライセンス*. Visual Studio に組み込まれている IntelliSense 機能は、WebMatrix の IntelliSense よりも包括的です。
- *デバッガ*: デバッガーを使用すると、実行中にプログラムを停止し、変数を調べ、コードを 1 行ずつステップ実行することで、コードのトラブルシューティングを行うことができます。

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>異なるバージョンの web ページでの Visual Studio の使用ASP.NET

Visual Studio 2017 で ASP.NET Web アプリを開発するには **、ASP.NETと Web 開発**ワークロードをインストールします。

Visual Studio 2012 および Visual Studio 2013 には、ASP.NET Web ページのサポートが含まれています。 (ASP.NET Web ページをサポートするために必要なパッケージは、Visual Studio のインストール時にインストールされます)。

Visual Studio 2010 には、ASP.NET Web ページの既定のサポートは含まれていません。 Visual Studio 2010 でASP.NET Web ページを使用するには、ASP.NET MVC パッケージをインストールする必要があります。 web ページ 2 ASP.NETを取得するには、mvc 4 ASP.NETインストールします。

次の表は、さまざまなバージョンの Visual Studio でのASP.NET Web ページのサポートをまとめたものです。

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET Web ページ 2** | ASP.NET MVC 4 をインストールします。 | (含まれる) | (含まれる) |
| **ASP.NET Web ページ 3** |  | NuGet を使用して ASP.NET Web ページ 3 に更新します。 | (含まれる) |

Visual Studio 2010 を使用するには[、「Visual Studio 2010 での ASP.NET Web ページのサポートのインストール](#vs2010support)」を参照してください。

## <a name="launching-visual-studio-from-webmatrix"></a>WebMatrix から Visual Studio を起動する

WebMatrix でプロジェクトを開始し、Visual Studio に切り替える場合は、WebMatrix は、簡単に Visual Studio でプロジェクトを開くボタンを提供します。 このボタンを有効にするには、Visual Studio がコンピューターにインストールされている必要があります。 次の図は、WebMatrix のボタンを示しています。

![Visual Studio 起動](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

ボタンをクリックすると、プロジェクトが Visual Studio で開かれます。 WebMatrix と Visual Studio を切り替えても問題なく切り替えることができます。 他の環境でファイルが変更された場合は、最新の変更を取得するために再ロードする必要がある場合は、通知されます。

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>Visual Studio で ASP.NET Razor サイトを作成する

Visual Studio で ASP.NET の Razor Web サイトを作成するには:

1. Visual Studio を開きます。
2. [**ファイル]** メニューの [**新しい Web サイト**] をクリックします。

    ![新しい Web サイトを作成する](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. [**新しい Web サイト]** ダイアログ ボックスで、使用する言語を選択します (Visual C# または Visual Basic)。
4. **[ASP.NET Web サイト (Razor)]** テンプレートを選択します。

    ![Razor サイト](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. **[OK]** をクリックします。

新しいプロジェクトが存在し、作業を開始するのに役立ついくつかの既定の Web ページが設定されます。

### <a name="using-intellisense"></a>Using IntelliSense

サイトを作成したので、IntelliSense が Visual Studio でどのように機能するかを確認できます。

1. 作成した Web サイトで *、Default.cshtml*ページを開きます。
2. ページ内`<h3>`のタグの後に、`@ServerInfo.`ドットを含むタグを入力します。 ドロップダウン リストにヘルパーに使用可能なメソッドが IntelliSense によって`ServerInfo`表示される様子に注目してください。

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. リストから`GetHtml`方法を選択し、Enter キーを押します。 IntelliSense はメソッドに自動的に入力します。 (C# の他のメソッドと同様に、`()`メソッドの後に文字を追加する必要があります。メソッドの完成した`GetHtml`コードは、次の例のようになります。

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. Ctrl キーを押しながら F5 キーを押してページを実行します。 ブラウザーで表示される場合のページの外観は次のようになります。

    ![ブラウザの既定のページ](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. ブラウザーを閉じます。

### <a name="using-the-debugger"></a>デバッガの使用

1. *Default.cshtml*ページの上部で、で始まる`Page.Title`行の後に次のコード行を追加します。

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. コードの左側にあるエディタの灰色の余白で、この新しい行の横をクリックして*ブレークポイント*を追加します。 ブレークポイントは、デバッガーに対して、その時点でプログラムの実行を停止し、何が起こっているかを確認できるように指示するマーカーです。

    ![ブレークポイントの設定](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. メソッドの呼び出`ServerInfo.GetHtml`しを削除し、その代わりに`@myTime`変数への呼び出しを追加します。 この呼び出しは、新しいコード行によって返される現在の時刻の値を表示します。
4. F5 キーを押して、デバッガーでページを実行します。 ページは、設定したブレークポイントで停止します。 次の図は、ブレークポイントが付いたエディターでのページの外観を示しています (黄色)。

    ![デバッグ ブレークポイント](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. [デバッグ] ツールバーの [**ステップ**イン] ボタンをクリック (または F11 キーを押します) をクリックして、次のコード行を実行します。 このボタンをクリックするたびに、次のコード行に実行を進めます。

    ![ステップインボタン](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. 変数の値を調`myTime`べるには、マウス ポインターをその上に置くか、[**ローカル**] ウィンドウと [**呼び出し履歴**] ウィンドウに表示される値を調べます。 変数の値が表示されます。

    ![時間の値を表示する](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. 変数の検査とコードのステップ実行が完了したら、F5 キーを押して、各行で停止することなくページの実行を続けます。 すべてのコードのステップ実行が完了すると、ブラウザーにページが表示されます。

デバッガーの詳細と Visual Studio でのコードのデバッグ方法については、「[チュートリアル: Visual Web 開発者の Web ページのデバッグ](https://msdn.microsoft.com/library/z9e7w6cs.aspx)」を参照してください。

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>visual Studio で ASP.NET MVC プロジェクトでの Razor の使用

Razor 構文は、ASP.NET MVC プロジェクトでも広く使用されます。 MVC は、動的な Web サイトを構築するための強力なパターン ベースの方法です。 ASP.NET Web ページ サイトの保守が困難になった場合は、そのサイトを ASP.NET MVC アプリケーションに変換することを検討してください。 MVC アプリケーションの作成例については[、「mvc 5 の概要ASP.NET」](../../../mvc/overview/getting-started/introduction/getting-started.md)を参照してください。

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>Visual Studio 2010 での ASP.NET Web ページのサポートのインストール

このセクションでは、Visual Web Developer 2010 Express と Visual Studio 用の ASP.NET Web ページ ツールをインストールする方法を示します。

1. Web プラットフォーム インストーラーをまだインストールしていない場合は、次の URL からダウンロードしてください。

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. Web プラットフォーム インストーラーを実行します。
3. [**製品]** タブをクリックします。

    ![[WebPI 製品] タブ](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. mvc **4 ASP.NET**検索 (ASP.NET Web ページ 2 の場合) し、[**追加**] をクリックします。 これらの製品には、ASP.NET Razor Web サイトを構築するための Visual Studio ツールが含まれます。

    ![WebPi インストール オプション](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. [**インストール**] をクリックしてインストールを完了します。
