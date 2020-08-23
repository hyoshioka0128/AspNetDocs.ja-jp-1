---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET ウェブページ (Razor) に関するよくある質問 |マイクロソフトドキュメント
author: Rick-Anderson
description: この記事では、web ページ (Razor) と WebMatrix に関してよく寄せられる質問ASP.NET一覧を示します。 チュートリアルで使用されるソフトウェアバージョンは、Web ページASP.NET(R..
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: a312d1327bc88e721bf7fc7459e420e3f582c88d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543705"
---
# <a name="aspnet-web-pages-razor-faq"></a>ASP.NET Web ページ (Razor) のよくあるご質問

[Tom FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > WebMatrix は、web ページをASP.NETするための統合開発環境として推奨されなくなりました。 [Visual Studio](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio)または [Visual Studio Code](https://code.visualstudio.com/) を使用する 。
>
> この記事では、web ページ (Razor) と WebMatrix に関してよく寄せられる質問ASP.NET一覧を示します。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>チュートリアルで使用するソフトウェアバージョン
> 
> 
> - ASP.NET ウェブページ (Razor) 3
> - Visual Studio 2013
> - ウェブマトリックス 3
>   
> 
> このチュートリアルは、web ページ 2、Web マトリックス 2、および Visual Studio 2012 ASP.NETでも動作します。

- [ASP.NET Web ページ、ASP.NET Web フォーム、および ASP.NET MVC の違いは何ですか。](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [Web ページを操作するためには、WebMatrix が必要ですか?](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [Web ページ上ASP.NET Web フォーム コントロールを使用できますか。](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [WebMatrix を使用せずに、ASP.NET Web ページ サイトを展開できますか。](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [ログインをサポートするには、Web セキュリティ ヘルパーを使用する必要がありますか?](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [web ページASP.NET HTML5 をサポートしていますか?](#Does_ASP.NET_Web_Pages_support_HTML5)
- [ウェブページでJavaScriptとjQueryを使用できますか?](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [その他のリソース](#AdditionalResources)

エラーやその他の問題に関する質問については[、「web ページ (Razor) トラブルシューティング ガイドASP.NET」](https://go.microsoft.com/fwlink/?LinkId=253001)を参照してください。

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>ASP.NET Web ページ、ASP.NET Web フォーム、および ASP.NET MVC の違いは何ですか。

3 つとも、動的な Web アプリケーションを作成するためのASP.NETテクノロジーです。

- web ページASP.NET、動的な (サーバー側) コードとデータベースへのアクセスを HTML ページに追加することに重点を置き、簡単で軽量な構文を備えています。
- ASP.NET Web フォームは、ページ オブジェクト モデルと従来のウィンドウ型コントロール (ボタン、リストなど) に基づいています。 Web フォームでは、クライアント ベース (Windows フォーム) の開発に慣れたユーザーになじみのあるイベント ベースのモデルを使用します。
- mvc ASP.NET、ASP.NETのモデル ビュー コント ローラー パターンを実装します。 「懸念事項の分離」(処理、データ、および UI レイヤー)に重点が置かれています。

3 つのフレームワークはすべて完全にサポートされており、ASP.NET チームによって引き続き開発されています。 一般に、どのフレームワークを使用するかは、バックグラウンドとASP.NETの経験によって異なります。

特にASP.NET Web ページは、HTML を既に知っているユーザーが、ページにサーバー処理を簡単に追加できるように設計されています。 プログラミングが初心者の学生、愛好家、一般的な人々には良い選択です。 また、non-ASP.NETの Web テクノロジの経験を持つ開発者にも適しています。

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>Web ページを操作するためには、WebMatrix が必要ですか?

いいえ。 WebMatrix は、web ページをASP.NETするための統合開発環境として推奨されなくなりました。 [Visual Studio](program-asp-net-web-pages-in-visual-studio.md)またはビジュアル[スタジオ コードを](https://code.visualstudio.com/)使用する 。

Visual Studio または Visual Studio コードを使用しない場合は[、Microsoft Web プラットフォーム インストーラー](https://www.microsoft.com/web/downloads/platform.aspx)を使用してコンポーネント製品を個別にインストールできます。 次の製品が必要です。

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5 (ASP.NET Web ページ フレームワークもインストール)
- IIS エクスプレス (Web サーバー)
- コンパクト 4.0 (データベース)

テキスト エディターを使用して *、.cshtml* (または *.vbhtml)* ページを編集できます。

ツールを使用せずに SQL Server コンパクト データベース *(.sdf*ファイル) を管理するのは少し難しくなります。 Visual Studio には *、.sdf*データベースを管理するためのツールが含まれています。 コード内で SQL コマンドを実行して、SQL Server 管理タスクを多数実行することもできます。

統合開発環境 (IDE) を使用せずに *.cshtml*ページをテストするには、ライブ サーバーに展開します。 (WebMatrix を[使用せずに ASP.NET Web ページ サイトを展開できますか?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)

### <a name="running-iis-express-without-using-an-ide"></a>IDE を使用せずに IIS エクスプレスを実行する

IIS Express を Web サーバーとしてコンピュータにインストールする場合は、それを使用してページをテストできます。 コマンド ラインから IIS Express を実行し、特定のポート番号に関連付けることができます。 次に、ブラウザーで *.cshtml*ファイルを要求するときに、そのポートを指定します。

Windows で、管理者特権を持つコマンド プロンプトを開き *、C:\プログラム ファイル\IIS Express*に変更します。 (64 ビット システムの場合は *、C:\プログラム ファイル (x86)\IIS Express フォルダーを使用します。* 次に、サイトへの実際のパスを使用して、次のコマンドを入力します。

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

他のプロセスによってまだ予約されていないポート番号を使用できます。 (通常、1024 を超えるポート番号は無料です)。値として`path`*、.cshtml*ファイルがある Web サイト フォルダーのパスを使用します。

このコマンドを実行してページを提供するように IIS Express を設定した後、ブラウザーを開いて *.cshtml*ファイルを参照できます。 次のような URL を使用します。

`http://localhost:35896/default.cshtml`

IIS Express コマンド ライン オプションの`iisexpress.exe /?`ヘルプを参照するには、コマンド ラインで入力します。

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>Web ページ上ASP.NET Web フォーム コントロールを使用できますか。

いいえ。 [CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox)コントロール、[検証コントロール](https://msdn.microsoft.com/library/bwd43d0x)[、GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview)コントロールなどの Web フォーム コントロールは、Web フォーム ページ *(.aspx*ファイル) でのみ動作します。 これらのコントロールには、Web フォーム ページ フレームワークが必要です。

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>WebMatrix を使用せずに、ASP.NET Web ページ サイトを展開できますか。

はい。 Web サイトファイルは、通常 FTP を使用してサーバーに手動でコピーできます。 手動でコピーを実行する場合は、SQL Server Compact (データベース) をサポートするファイルもコピーする必要があります。 詳細については、ブログ記事「[ツールを使用しない Web ページ アプリケーションの配置](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)」を参照してください。

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>ログインをサポートするには、Web セキュリティ ヘルパーを使用する必要がありますか?

いいえ。 Web`SimpleMembership`ページの一部であるプロバイダASP.NET 1 つのオプションがあります。 ASP.NETに含まれるセキュリティ プロバイダ (Web フォームでの操作に使用される可能性があります) も利用できます。 たとえば、Web ページの場合と同様に、フォーム認証をASP.NET Web ページで使用できます。 フォーム認証の使用例については、Microsoft サポート記事[「C#.NET を使用してASP.NET アプリケーションにフォーム ベース認証を実装する方法](https://support.microsoft.com/kb/301240)」を参照してください。 簡単な例をダウンロードするには、「[ログイン&amp;パスワード」ASP.NETバージョンを](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)参照してください。

Windows 認証の使用方法については、ブログ記事[「ASP.NET Web ページで Windows 認証を使用](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)する」を参照してください。

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>web ページASP.NET HTML5 をサポートしていますか?

はい。 web ページ (*.cshtml*ページまたは *.vbhtml*ページ ) ASP.NET作成するページは、基本的には、ページがレンダリングされる前にサーバー上で実行されるコードも含む HTML ページです。 ユーザーのブラウザーが HTML5 をサポートしている限り *、.cshtml*または *.vbhtml*ページで HTML5 要素を使用できます。

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>ウェブページでJavaScriptとjQueryを使用できますか?

そして、 Web ページ *(.cshtml*ページまたは *.vbhtml*ページ) を使用して作成ASP.NETページは、サーバー コードが含まれる HTML ページにすぎません。 したがって、JavaScript または jQuery を使用して通常の HTML ページで実行できる操作は *、.cshtml*ページまたは *.vbhtml*ページでも実行できます。

WebMatrix の**スターター サイト**テンプレートには、いくつかの jQuery ライブラリが含まれています。 そのテンプレートを使用してサイトを作成する場合 *、Scripts*フォルダーには jQuery コア ライブラリ *(jquery-1.6.2.js)* と jQuery 検証用のライブラリ *(jquery.validate.js*など) が含まれます。

ASP.NET Web ページで jQuery を使用する方法を示すブログ投稿を次に示します。

- レイチェル・アペルによる[ウェブマトリックスを使用してASP.NETウェブページにjQueryの良さを追加](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/)する
- [5分: ウェブマトリックス + jQuery UI + json + jQuery テンプレート](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/)by ジョナス・エリクソン
- マイク・ブリンドによる[ウェブマトリックスとjQueryフォーム](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>その他のリソース

[ASP.NET Web ページ (Razor) トラブルシューティング ガイド](https://go.microsoft.com/fwlink/?LinkId=253001)

ASP.NET[ウェブサイト上のウェブマトリックスとASP.NETウェブページフォーラム](https://forums.asp.net/1224.aspx/1?WebMatrix)
