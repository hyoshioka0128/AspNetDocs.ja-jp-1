---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Visual Studio 2012 の ASP.NET および Web ツール 2013.1 のリリース ノート |マイクロソフトドキュメント
author: rick-anderson
description: このドキュメントでは、Visual Studio 2012 の ASP.NET と Web ツール 2013.1 のリリースについて説明します。
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543575"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Visual Studio 2012 の ASP.NET と Web 2013.1 ツールのリリース ノート

[マイクロソフト](https://github.com/microsoft)

> このドキュメントでは、Visual Studio 2012 の ASP.NET と Web ツール 2013.1 のリリースについて説明します。

## <a name="contents"></a>内容

- [インストールに関する注意事項](#install)
- [ソフトウェア要件](#requirements)
- ASP.NETおよび Web ツール 2013.1 の新機能 2012 年の Visual Studio の 2012

    - [ブートストラップ](#bootstrap)
    - [テンプレート](#templates)

        - [mvc 5 テンプレートASP.NET](#mvc5template)
        - [Web API 2 テンプレートASP.NET](#apitemplate)
        - [アイテム テンプレート](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET足場](#scaffold)
    - [カミソリエディタ](#razor)
    - [NuGet 2.7](#nuget)
- 既知の問題と互換性に関する変更

    - [ASP.NET足場](#issuescaffolding)

        - [MVC および Web API スキャフォールディング - HTTP 404、見つかりませんエラー](#404issue)
        - [Web 用の Visual Studio Express 2012 は、スキャフォールディングされたアイテムを追加した後に動作を停止します。](#expressissue)
    - [ASP.NETカミソリ3](#issuerazor)

        - [[次の操作で参照] または [F5] を使用して cshtml ファイルを表示すると、サーバー エラーが発生する](#browseissue)
        - [URL書き換えとチルダ(~)](#rewriteissue)
    - [テンプレート](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>インストールに関する注意事項

[インストール](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids)ASP.NETと Web ツール 2013.1 の Visual Studio 2012。

<a id="requirements"></a>
## <a name="software-requirements"></a>ソフトウェア要件

Web 用の Visual Studio 2012 または Visual Studio エクスプレス 2012 のいずれかが必要です。

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>ASP.NETおよび Web ツール 2013.1 の新機能 2012 年の Visual Studio の 2012

<a id="bootstrap"></a>
### <a name="bootstrap"></a>ブートストラップ

MVC 5 のコント ローラーとビューをスキャフォールディングするとき、ビューのマークアップは[Bootstrap](http://getbootstrap.com/)を使用します。

<a id="templates"></a>
### <a name="templates"></a>テンプレート

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>mvc 5 テンプレートASP.NET

新しい MVC 5 テンプレートを追加しました。 最新の MVC 5 NuGet パッケージを参照し、スキャフォールディングを使用してコントローラーとビューを追加できます。

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>Web API 2 テンプレートASP.NET

新しい Web API 2 テンプレートを追加しました。 最新の Web API 2 NuGet パッケージを参照し、スキャフォールディングを使用してコントローラーとビューを追加できます。

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>項目テンプレート

MVC 5 ビュー、Web ページ (Razor 3)、および Web API 2 コント ローラーの新しい項目テンプレートを追加しました。 関連する NuGet パッケージをプロジェクトにインストールし、新しい項目を追加します。

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

エンティティ フレームワークを使用して MVC または Web API コント ローラーをスキャフォールディングするとき、フレームワーク 6 を使用します。 エンティティ フレームワークの詳細については、「[エンティティ フレームワークのバージョン履歴](https://msdn.com/data/jj574253)」を参照してください。

また、ダウンロードして、Visual Studio 2012 のエンティティ フレームワーク 6 ツールをインストールできます。 エンティティ[フレームワークの取得を](https://msdn.com/data/ee712906#tooling)参照してください。

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET足場

ASP.NETスキャフォールディングは、ASP.NET Web アプリケーション用のコード生成フレームワークです。 これにより、データ モデルとやり取りする定型コードをプロジェクトに簡単に追加できます。

以前のバージョンの Visual Studio では、スキャフォールディングは MVC プロジェクトASP.NETに限定されていました。 この更新プログラムを使用すると、Web フォームを含む任意のASP.NET プロジェクトにスキャフォールディングを使用できるようになりました。 この更新プログラムは、Web フォーム プロジェクトのページの生成をサポートしていませんが、プロジェクトに MVC 依存関係を追加することで Web フォームでスキャフォールディングを使用できます。 Web フォームのページ生成のサポートは、今後の更新プログラムで追加される予定です。

スキャフォールディングを使用する場合、必要なすべての依存関係がプロジェクトにインストールされていることを確認します。 たとえば、ASP.NET Web フォーム プロジェクトを使用して Web API コント ローラーを追加するのにはスキャフォールディングを使用する場合は、必要な NuGet パッケージと参照が自動的にプロジェクトに追加されます。

Mvc スキャフォールディングを Web フォーム プロジェクトに追加するには、**新しいスキャフォールディング項目**を追加し、ダイアログ ウィンドウで**MVC 5 の依存関係**を選択します。 スキャフォールディング MVC には 2 つのオプションがあります。最小限とフル。 [最小] を選択した場合は、ASP.NET MVC の NuGet パッケージと参照のみがプロジェクトに追加されます。 [完全] オプションを選択すると、MVC プロジェクトに必要なコンテンツ ファイルと同様に、最小限の依存関係が追加されます。

スキャフォールディング非同期コントローラーのサポートでは、Entity Framework 6 の新しい非同期機能が使用されます。

詳細およびチュートリアルについては、「ASP.NET[スキャフォールディングの概要](../2013/aspnet-scaffolding-overview.md)」を参照してください。 これらのチュートリアルでは、Visual Studio 2013 でスキャフォールディングを示していますが、Visual Studio 2012 の ASP.NET と Web ツール 2013.1 にも適用できます。

<a id="razor"></a>
### <a name="razor-editor"></a>カミソリエディタ

この更新プログラムでは、Visual Studio 2012 は Razor 3 ツール/編集をサポートするようになりました。

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 には[、NuGet 2.7 リリース ノート](http://docs.nuget.org/docs/release-notes/nuget-2.7)で詳細に説明されている新機能の豊富なセットが含まれています。

このバージョンの NuGet では、ユーザーが不足しているパッケージを復元する NuGet を明示的に許可する必要がなくなります。 NuGet 2.7 をインストールする際、ユーザーは、不足しているパッケージを自動的に復元することに暗黙的に同意します。 ユーザーは、Visual Studio の NuGet 設定を使用して、パッケージの復元を明示的にオプトアウトできます。 この変更により、パッケージの復元のしくみが簡略化されます。

## <a name="known-issues-and-breaking-changes"></a>既知の問題と互換性に関する変更

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET足場

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC および Web API スキャフォールディング - HTTP 404、見つかりませんエラー

スキャフォールディングされた項目をプロジェクトに追加するときにエラーが発生した場合、プロジェクトが不整合な状態のままになる可能性があります。 スキャフォールディングに加えられた変更の一部はロールバックされますが、インストールされている NuGet パッケージなどの他の変更はロールバックされません。 ルーティング構成の変更がロールバックされると、スキャフォールディングされたアイテムに移動するときに、ユーザーに HTTP 404 エラーが表示されます。

MVC のこのエラーを修正するには、新しいスキャフォールディングされた項目を追加し、MVC 5 の依存関係 (最小または完全) を選択します。 このプロセスにより、必要な変更がすべてプロジェクトに追加されます。

Web API でこのエラーを修正するには、次の手順を実行します。

1. 次の WebApiConfig クラスをプロジェクトに追加します。

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. 次のようにして、Global.asax\_のアプリケーション開始メソッドで WebApiConfig.Register を構成します。

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>Web 用の Visual Studio Express 2012 は、スキャフォールディングされたアイテムを追加した後に動作を停止します。

Web 用の Visual Studio Express 2012 が、エンティティ フレームワーク (エンティティ フレームワークを使用した Web API 2 コントローラーなど) でスキャフォールディングされたアイテムを追加した後に動作を停止した場合、Visual Studio Express が System.Web.Extensions に依存するアセンブリのネイティブ イメージを読み込めなかった可能性があります。

この問題を解決するには、システム.Web.拡張機能の MSIL イメージで動作するように Visual Studio Express を構成します。

1. 管理者モードでコマンドプロンプトを開きます。
2. %プログラムファイル%\マイクロソフトビジュアルスタジオ11.0\コモン7\IDEまたは%プログラムファイル(x86)%\マイクロソフトビジュアルスタジオ11.0\コモン7\IDE(64ビットウィンドウ用)に移動します。
3. テキスト エディターで VWDExpress.exe.config を開きます。
4. 構成&lt;&gt;/ランタイム&lt;要素の下に次の行を追加&gt;します。  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. Web 用のビジュアル スタジオ エクスプレス 2012 を再起動します。

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NETカミソリ3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>[次の操作で参照] または [F5] を使用して cshtml ファイルを表示すると、サーバー エラーが発生する

Visual Studio 2012 で MVC 5 プロジェクトを作成し (または Visual Studio 2013 で作成された MVC 5 プロジェクトを Visual Studio 2012 で開く)、参照または F5 を使用して cshtml ファイルを表示しようとすると、エラーが表示**されます。** サーバーは、`http://localhost:XXXX/Views/../XXXX.cshtml`

この問題を解決するには、プロジェクトの **[開始動作]** の設定を **[特定のページ]** に変更します。 ページの値を指定する必要はありません。

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

この変更を行った後、F5 を選択すると、アプリケーションのルート`http://localhost:XXXX`( ) に移動します。 この動作は、**現在のページ**の設定が開いているページを起動する Visual Studio 2013 の MVC 5 プロジェクトの動作と同じではありません。

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>URL書き換えとチルダ(~)

ASP.NET Razor 3 または mvc 5 ASP.NETにアップグレードした後、URL の書き換えを使用している場合、チルダ(~) 表記が正しく動作しなくなる可能性があります。 URL の書き換えは、A/ 、 SCRIPT / &lt;&gt;、 &lt;&gt; &lt;LINK/&gt;などの HTML 要素のチルダ (~) 表記に影響を与え、その結果、チルダがルート ディレクトリにマップされなくなりました。

たとえば **、asp.net/content**の**要求を書**き換えてasp.netすると&lt;、A href="~/content/"/&gt;の href 属性は **/content/content/** の代わりに解決**/** されます。 この変更を抑制するには、各 Web ページまたは Global.asax の**アプリケーション\_の開始要求**で**\_、IIS WasUrlRewrite の**コンテキストを false に設定します。

<a id="templateissue"></a>
### <a name="templates"></a>テンプレート

Windows 8.1 または Windows Server 2012 R2 で Visual Studio 2012 でASP.NET MVC プロジェクトを作成すると、Visual Studio は、エラー メッセージを表示します"ASP.NET 4.5 の Web [url] を構成できませんでした。

![構成エラー](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

Visual Studio 2012 では、これらのリリースの Windows にインストールされている場合、ASP.NET 4.5 機能が有効になっていないため、このエラーが表示されます。 ASP.NET 4.5 を有効にするには、「 [Windows 機能のオンとオフを切り替える](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)」で説明されている手順を実行します。

![Windows 機能のオンとオフを切り替える](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

または、コマンド ラインを使用して ASP.NET 4.5 を有効にすることもできます。

1. 管理者モードでコマンドプロンプトを開きます。
2. 次のコマンドを実行して、ASP.NET 4.5 を有効にします。  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
