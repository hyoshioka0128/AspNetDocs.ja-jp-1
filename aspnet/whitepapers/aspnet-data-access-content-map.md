---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NETデータアクセス - 推奨リソース |マイクロソフトドキュメント
author: rick-anderson
description: このトピックでは、主に Entity Framework と SQL Se.. を使用して、ASP.NET Web アプリケーションのデータにアクセスする方法に関するドキュメント リソースへのリンクを提供します。
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675785"
---
# <a name="aspnet-data-access---recommended-resources"></a>ASP.NET データ アクセス - 推奨リソース

> このトピックでは、主に Entity Framework と SQL Server を使用して、ASP.NET Web アプリケーションのデータにアクセスする方法に関するドキュメント リソースへのリンクを提供します。
> 
> ブログ投稿、[スタックオーバーフロー](http://stackoverflow.com)スレッド、または役に立つその他のリンクを知っている場合は、リンク[を記載したメールを送信してください](mailto:aspnetue@microsoft.com?subject=Data Access Content Map)。
> 
> 最終更新日 2014年4月3日

このトピックは、次のセクションで構成されています。

- [ASP.NET でのデータ アクセスの概要](#gettingstarted)
- [エンティティ フレームワークの使用](#ef)

    - [エンティティ フレームワーク コードを最初に使用する](#cf)
    - [エンティティ フレームワーク コードの最初の移行の使用](#efcfmigrations)
    - [エンティティ フレームワーク データベースを最初に使用するか、モデルを先に使用する (EF デザイナー)](#efdbf)
    - [エンティティ フレームワークでの関連データの読み込み (遅延読み込み、一括読み込み、および明示的な読み込み)](#efrelateddata)
    - [エンティティ フレームワークのパフォーマンスの最適化](#optimizingef)
    - [エンティティ フレームワーク アプリケーションでの同時実行の処理](#efconcurrency)
    - [エンティティ フレームワークに関する書籍](#efbooks)
    - [追加のエンティティ フレームワーク リソース](#otherefresources)
- [web フォーム アプリケーションのASP.NETデータ バインディング](#wfdatabinding)

    - [Web フォーム モデル バインドの使用](#wfmodelbinding)
    - [Web フォーム データ ソース コントロールの使用](#wfdsc)
    - [Web フォームのデータ バインド コントロールとデータ 連結式の使用](#wfdbc)
- [SQL Server データベースの操作](#sqlserver)

    - [SQL サーバー エクスプレス ローカルデータベースの操作](#sslocaldb)
    - [SQL Server 高速データベースの操作](#sse)
    - [データベースの操作](#ssdb)
    - [SQL サーバーと Windows Azure SQL データベースの選択](#ssdbchoosing)
- [NoSQL データベース管理システムの使用](#nosql)
- [ASP.NET アプリケーションで LINQ クエリを使用する](#linq)
- [動的データスキャフォールディングの使用](#dd)
- [データ アクセスのセキュリティ保護](#securing)
- [データ アクセス パフォーマンスの最適化](#optimizingdataaccess)
- [データベースの配置](#deploying)
- [Web サービスを介したデータへのアクセス](#webservice)
- [その他のリソース](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>ASP.NET でのデータ アクセスの概要

- [データ ストレージ オプション (Windows Azure を使用した実際のクラウド アプリの構築)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) クラウド向けの開発に関する電子書籍の章。 リレーショナル データベースに精通している多くの開発者が見落としがちな代わりに NoSQL データベースを導入します。 リレーショナルまたはNoSQLを選択する場合、または特定のプラットフォームを選択する際の注意事項に関するガイドラインを示します。
- [ASP.NETデータ アクセス オプション](https://msdn.microsoft.com/library/ms178359.aspx)(MSDN) ASP.NET用のリレーショナル データベースのデータ アクセス オプションの概要と、シナリオに適したプラットフォームとアクセス方法の選択方法に関するガイダンス。
- [リレーショナル データベース](http://en.wikipedia.org/wiki/Relational_database): ウィキペディア)。 リレーショナル データベースを使用したことがない場合は、リレーショナル データベースの用語と概念の概要については、このページを参照してください。 特に SQL Server の概要については、このトピックの後半の[「SQL Server データベースの操作](#sqlserver)」を参照してください。

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>エンティティ フレームワークの使用

- [エンティティ フレームワーク開発アプローチ](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)(MSDN)。 Entity Framework 開発アプローチデータベース ファースト、モデル ファースト、またはコード ファーストの選択方法に関するガイダンスです。

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>エンティティ フレームワーク コードを最初に使用する

次のチュートリアルでは、ダウンロード可能なサンプル アプリケーションを提供します。

- [MVC 5 を使用して EF 6 の概要](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). 移行や EF 6 の機能 (接続の回復性、コマンドの傍受、非同期など) など、さまざまな Entity Framework コード ファースト のシナリオについて説明します。 これは[、EF 5 / MVC 4シリーズ](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)の更新版です。 前述のシリーズには、新しいシリーズに含まれていないリポジトリと作業単位パターンに関するチュートリアルが含まれています。
- [mvc 5 ASP.NETの概要](../mvc/overview/getting-started/introduction/getting-started.md). Entity Framework コードファーストシナリオの狭い範囲をカバーしていますが、MVC 機能を導入するより包括的な仕事を行います。
- [モデル バインドと Web フォーム](https://go.microsoft.com/fwlink/?LinkId=286117): Web フォーム アプリケーションでコードファーストを使用します。
- [ASP.NET 4.5 Web フォームの概要](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)」 コードファーストの一部を対象にした Web フォームの概要。 モデル バインドを使用します。
- [MVCミュージックストア](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md). メンバーシップと承認も実装する電子商取引 MVC 3 アプリケーションで Code First を使用します。 ここで使用されるMVCバージョンとASP.NETメンバーシップ(認証と承認)システムは古くなっています。メンバーシップに関する最新情報については、ASP.NETのメンバーシップに関する[https://asp.net/identity](https://asp.net/identity)最新情報を参照してください。

その他のリソース:

- [エンティティ フレームワーク - 既存のデータベースへのコードファースト](https://msdn.microsoft.com/data/jj200620)。 Msdn。 既存のデータベースで Code First を使用する方法を示すビデオとチュートリアル。
- [データ デベロッパー センター - エンティティ フレームワーク](https://msdn.microsoft.com/data/ef). Msdn。 Entity Framework チームによって作成および管理された Entity Framework ドキュメントのガイドについては、「[はじめに](https://msdn.microsoft.com/data/ee712907)」リンクを参照してください。

このトピック[の「エンティティ フレームワーク](#efbooks)」および[「追加のエンティティ フレームワーク リソース](#otherefresources)」も参照してください。

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>エンティティ フレームワーク コードの最初の移行の使用

上記の Code First チュートリアルのほとんどは、移行について説明しています。 以下のリソースも参照してください。

- [Visual Studio を使用した ASP.NET Web デプロイ](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 コード最初の移行を使用してデータベースを配置する方法を示す 2 部構成のチュートリアル シリーズ。
- [メンバーシップ、OAuth、および SQL データベースを備えたセキュリティで保護された ASP.NET MVC 5 アプリを Windows Azure Web サイトに展開](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)する 。 マイクロソフト Azure)。 移行を使用してメンバーシップとアプリケーション データを Azure にデプロイする方法。
- [Visual Studio および ASP.NET の Web 配置の概要](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment) コード最初の移行が Visual Studio Web 配置機能に統合される方法の説明については **、「Visual Studio でのデータベース配置の構成**」セクションを参照してください。
- [データ デベロッパー センター - コード最初の移行](https://msdn.microsoft.com/data/jj591621)(MSDN) エンティティ フレームワーク チームの移行ドキュメント。
- [移行スクリーンキャスト シリーズ](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx). EF ブログ)。 コードファースト移行の高度なトピックに関する 3 つのビデオ。
- [ASP.NET Web ページ サイトを使用して最初に移行するコード](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites): マイクスドットネッティングブログ)。 Visual Studio クラス ライブラリ プロジェクトにデータ コンテキストを配置することにより、ASP.NET Web ページ サイトでコード ファースト移行を使用する方法について説明します。

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>エンティティ フレームワーク データベースを最初に使用するか、モデルを先に使用する (EF デザイナー)

- [MVC 5 を使用して、最初に Entity Framework 6 データベースの概要](../mvc/overview/getting-started/database-first-development/setting-up-database.md). サーバー エクスプローラーでスクリプトを実行してデータベースを作成し、Entity Framework デザイナーを使用してデータ モデルを作成します。 単純な CRUD Web ページを作成する方法、および他のデータ処理関数の場合は、すべての EF ワークフローが同じ DbContext API を使用するため、コードファーストチュートリアルの 1 つを実行できます。

次のリソースは古いです。 これらの機能は、Entity Framework のバージョン 4.0 を使用する場合に、Web フォーム アプリケーションでデータ バインディングにデータ ソース コントロールを使用する場合に便利です。

- [エンティティ フレームワーク 4.0 の概要](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) **コントロールの**使用方法を示します。
- [エンティティ フレームワークを続行](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)します **(ObjectDataSource**コントロールの使用方法を示します。 同時実行処理のチュートリアル、EF のパフォーマンスに関するチュートリアル、EF 4.0 の新機能に関するチュートリアルが含まれています。

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>Entity Framework での関連データの処理 (遅延読み込み、一括読み込み、および明示的な読み込み)

- [ASP.NET MVC アプリケーションでエンティティ フレームワークを使用して関連データを読み取る](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 コードまず、MVC サンプル アプリケーション。 表示されるメソッドは、Web フォーム モデル バインドおよびデータベース ファースト ワークフローにも適用されます。
- [データ デベロッパー センター - 関連エンティティの読み込み](https://msdn.microsoft.com/data/jj574232)(MSDN)。 関連データの読み込みに関する Entity Framework チームのドキュメント。

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>エンティティ フレームワークのパフォーマンスの最適化

- [ASP.NET アプリケーションの高度なエンティティ フレームワーク シナリオ](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)」 独自の SQL ステートメントを実行する方法、または独自のストアド プロシージャを呼び出す方法、変更検出を無効にする方法、および変更を保存するときに検証を無効にする方法について説明します。
- エンティティ フレームワーク 5 (MSDN)[のパフォーマンスに関する考慮事項](https://msdn.microsoft.com/data/hh949853)。
- [パフォーマンスに関する考慮事項 (エンティティ フレームワーク)](https://msdn.microsoft.com/library/cc853327) (MSDN)。
- [ASP.NET Web アプリケーションでのエンティティ フレームワークによるパフォーマンスの最大化](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md) エンティティ フレームワーク 4.0 に適用されます。
- このトピックの[「ASP.NETデータ アクセスの最適化](#optimizingdataaccess)」も参照してください。

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>エンティティ フレームワーク アプリケーションでの同時実行の処理

- [ASP.NET MVC アプリケーションでのエンティティ フレームワークとの同時実行の処理](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) コードまず、DBContext API、MVC サンプル アプリケーションを使用します。
- [データ デベロッパー センター – オプティミスティック同時実行制御パターン](https://msdn.microsoft.com/data/jj592904)(MSDN)。 エンティティ フレームワーク チームの同時実行ドキュメント。
- [ASP.NET Web アプリケーションでのエンティティ フレームワークとの同時実行制御の処理](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md) エンティティ フレームワーク 4.0 に適用されます。 データベースまず、Web フォーム サンプル アプリケーションを使用した ObjectContext API です。

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>エンティティ フレームワークに関する書籍

- [プログラミング エンティティ フレームワーク: ジュリー](http://shop.oreilly.com/product/0636920022237.do) ・ラーマンとローワン・ミラーによる DbContext。
- [プログラミングエンティティフレームワーク:ジュリー](http://shop.oreilly.com/product/0636920022220.do) ・ラーマンとローワン・ミラーによるコードファースト。

これらの書籍はどちらも最新の手法で最新の手法です。 これらのツールは、インターネット上で利用可能なものよりも包括的でわかりやすい Entity Framework の紹介を提供します。 ジュリー・ラーマンによる[プログラミングエンティティフレームワーク](http://shop.oreilly.com/product/9780596807252.do)は、もう1冊の本は、より大きく、より包括的ですが、古く、それがカバーする技術の多くは、もはやEntity Frameworkを使用するための推奨方法ではありません。 MSDN サイトの「データ デベロッパー センター -[書籍](https://msdn.microsoft.com/data/aa937716)」の Entity Framework チームが推奨する書籍の一覧もご覧ください。

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>その他のエンティティ フレームワーク リソース

- [エンティティ フレームワーク (ADO.NET) チームブログ](https://blogs.msdn.com/b/adonet/). 最新の情報と新しい機能強化の発表に最適なリソースの 1 つ。 他の EF 関連のブログについては、「 エンティティ[フレームワークの概要](https://msdn.microsoft.com/data/ee712907)」のブログロールを参照してください。
- [MSDN マガジン](https://msdn.microsoft.com/magazine/default.aspx). エンティティ フレームワークに関連するトピックに関する多くの場合は、「**データ ポイント**」列を参照してください。

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>web フォーム アプリケーションのASP.NETデータ バインディング

- [web フォーム データ アクセス](https://msdn.microsoft.com/library/jj822927.aspx)オプション<a id="wfmodelbinding"></a>(MSDN) をASP.NETします。

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>Web フォーム モデル バインドの使用

- [モデル バインドと Web フォーム](https://go.microsoft.com/fwlink/?LinkId=286117): EFコードファーストを使用したチュートリアルシリーズ。
- [Web フォーム モデル バインド パート 1: データの選択](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx)(スコット・ガスリーのブログ)。 これらの古いブログ投稿では、現在 ItemType という名前のプロパティは ModelType という名前でしたが、それ以外の場合は、そのプロパティに含まれる情報が有効です。
- [Web フォーム モデル バインド パート 2: データのフィルタリング](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx)(Scott Guthrie のブログ)。
- [Web フォーム モデル バインド パート 3: 更新と検証](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx)(スコット ガスリーのブログ)
- [ASP.NET 4.5 Web フォーム モデル バインド](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md) (ビデオ)。
- [モデル バインドパート 1 - データの選択](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md)(ビデオ)。
- [モデル バインドパート 2 - フィルタリング](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md)(ビデオ)
- [ASP.NET 4.5 Web フォーム - データ項目と詳細の表示](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)の概要 」

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>Web フォーム データ ソース コントロールの使用

- [データ ソース Web サーバー コントロール](https://msdn.microsoft.com/library/ms247258.aspx)(MSDN)。
- エンティティ フレームワーク 6 (マイクロソフト Web 開発ブログ)[の動的データ プロバイダーと EntityDataSource コントロールのリリースを発表](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)します。

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>Web フォームのデータ バインド コントロールとデータ 連結式の使用

- [モデル バインドと Web フォーム](https://go.microsoft.com/fwlink/?LinkId=286117): EF コードファーストを使用するチュートリアル シリーズ。
- [ASP.NET 4.5 Web フォーム - データ項目と詳細の表示](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)の概要 」
- [厳密に型指定されたデータ コントロール](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx)(スコット ガスリーのブログ)。
- [厳密に型指定されたデータ コントロール](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md)(ビデオ)。
- [ASP.NET 4.5 Web フォームの強力な型指定されたデータ コントロール](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md)(ビデオ)
- [データ バインド Web サーバー コントロール](https://msdn.microsoft.com/library/ms228214.aspx)(MSDN)
- [データ バインディング式の概要](https://msdn.microsoft.com/library/ms178366.aspx)(MSDN)。 このページでは **、Eval**と Bind のみを取り上**げ**、**Item**と**BindItem**を含むように更新されていません。

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>SQL Server データベースの操作

- [SQL Server データベースの機能](https://msdn.microsoft.com/library/hh230827.aspx)(MSDN)。 SQL Server のさまざまなトピックの概要については、目次のこのトピックの下にあるエントリを参照してください。
- [SQL サーバー エディション](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver)(MSDN)。 使用可能な SQL Server エディションの概要と、各エディションに関する詳細情報へのリンク)
- [ASP.NET Web アプリケーション用の SQL Server 接続文字列](https://msdn.microsoft.com/library/jj653752.aspx)(MSDN)。
- [ASP.NET Web アプリケーションに対して SQL Server コンパクトを使用](https://msdn.microsoft.com/library/ms247257.aspx)する (MSDN)。
- [SQL Server: データベース製品サンプル](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md) サンプルアドベンチャーワークスデータベース。
- [サンプル データベースのインストール](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)」 ここに示す方法に加えて、サンプルの .mdf ファイルのいずれかを Web プロジェクトの\_[アプリ データ] フォルダーにダウンロードし、データベースを LocalDB に変換して、LocalDB 接続文字列を作成することもできます。 その方法については、「[方法 : LocalDB にアップグレードする](https://msdn.microsoft.com/library/hh873188.aspx)」を参照してください。

SQL Server Express と LocalDB の操作、および SQL Server と SQL データベースの選択については、次のセクションも参照してください。

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>SQL サーバー エクスプレス ローカルデータベースの操作

- [2012 年のローカルデータベースを使用](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx)します。 ローカル DB の公式 MSDN の概要。
- [ASP.NET Web アプリケーション用の SQL Server 接続文字列](https://msdn.microsoft.com/library/jj653752.aspx)(MSDN)。
- [方法 : ローカルデータベースにアップグレードする](https://msdn.microsoft.com/library/hh873188.aspx)(MSDN)。 以前のバージョンの SQL Server Express から LocalDB に .mdf ファイルを移行する方法について説明します。 [SQL Server 2012 サンプル データベース](https://go.microsoft.com/fwlink/?linkid=117483)のいずれかをダウンロードする場合も、このプロセスを実行する必要があります。
- [SQL エクスプレスの改善されたローカルデータベースの概要](https://go.microsoft.com/fwlink/?LinkId=234375)(SQL Server エクスプレス ブログ)。 LocalDB が作成された理由については、MSDN に含まれているよりも多くの背景があります。
- [ローカルデータベース: 私のデータベースはどこにありますか?](https://go.microsoft.com/fwlink/?LinkId=234376) (SQL Server エクスプレス ブログ)。 LocalDB データベース ファイルが作成される場所に関する情報。
- [完全な IIS で LocalDB を使用する、パート 1: ユーザー プロファイル](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx)(SQL Server Express ブログ)。 ローカル DB は IIS で動作するようには設計されていません。 この一連のブログ記事では、問題といくつかの回避策について説明します。

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>SQL Server 高速データベースの操作

- [ASP.NET Web アプリケーション用の SQL Server 接続文字列](https://msdn.microsoft.com/library/jj653752.aspx)(MSDN)。 SQL Server Express で AttachDBFileName 接続文字列設定を使用する場合は、このページの特にユーザー インスタンスセクションを参照してください。
- [ローカル SQL Server Express 2008 の所有権を取得する方法](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx)(SQL Server エクスプレス ブログ)。 一般的な問題は、SQL Server Express インスタンスの管理者ではないため、SQL Server Express データベースを操作できないことです。 既定では、SQL Server Express をインストールしたユーザーのみが管理者になります。 このブログでは、コンピュータの管理者である場合に、自分を SQL Server Express 管理者にする方法について説明します。
- [ASP.NET Web アプリケーションは、実稼働環境で SQL Server Express データベースを使用できますか。](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN)。

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>データベースの操作

- [メンバーシップ、OAuth、および SQL データベースを備えたセキュリティで保護された ASP.NET MVC アプリを Windows Azure Web サイト](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)(マイクロソフト Azure サイト) にデプロイします。
- [SQL データベース](https://docs.microsoft.com/azure/sql-database/)(マイクロソフトの Azure サイト)。 チュートリアルの概要とハウツー ガイド。
- [データベースを使用します](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx)。 MSDN の SQL データベースの目次の最上位ノード。
- [マイクロソフトの SQL データベース TechNet Wiki の記事のインデックス](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx)(マイクロソフトテックネットサイト).
- [一時的な障害処理アプリケーション ブロック](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx): 一時的なネットワーク障害と、スロットルによる接続エラーを処理できるフレームワーク。 NuGet パッケージで利用可能:[エンタープライズ ライブラリ 5.0 - 一時的なフォールト処理アプリケーション ブロック](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling)。
- [SQL データベースとエンティティ フレームワークの概要](https://msdn.microsoft.com/data/jj556244)(MSDN)
- [Windows Azure トレーニング キット](https://www.microsoft.com/download/details.aspx?id=8396)(マイクロソフト ダウンロード センター) SQL データベースの実習が含まれています。
- [データベース コミュニティ フォーラム](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads).
- [データベースへの移行](https://msdn.microsoft.com/library/ff803375.aspx)(MSDN) Microsoft パターンとプラクティス チームによる包括的なエンド ツー エンド シナリオの 1 つの章。 移行する理由と、SQL Server から SQL データベースへの移行方法について説明します。
- [データベースを Windows Azure SQL データベースに移行する](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx)(MSDN)。
- [SQL データベース移行ウィザード](http://sqlazuremw.codeplex.com/) SQL データベースとの間でデータベースを移行するためのオープン ソース ツール。

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>SQL サーバーと Windows Azure SQL データベースの選択

- [SQL サーバーを Windows Azure SQL データベースと比較](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx)します 。
- [データ移行の Windows Azure SQL データベース: ツールと手法](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx)(MSDN)。 SQL Server と SQL データベースを比較し、SQL Server から SQL データベースに移行するタイミングに関するガイダンスを提供するセクションが含まれています。
- [Windows Azure SQL データベース配信ガイド](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx)(マイクロソフト テックネット サイト)。
- [SQL サーバー機能の制限事項 (Windows Azure SQL データベース)](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) (MSDN)。
- [Windows Azure テーブル ストレージと Windows Azure SQL データベース - 比較と対照 (MSDN)。](https://msdn.microsoft.com/library/jj553018.aspx) Windows Azure にデプロイするアプリケーションの場合は、Windows Azure テーブル ストレージが Windows Azure SQL データベースの代わりに使用される場合があります。 このトピックは、これらの選択肢を決定する際に役立ちます。
- [データベースを使用します](https://msdn.microsoft.com/library/windowsazure/ee336279)。
- [ガイドラインと制限事項 (Windows Azure SQL データベース)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>NoSQL データベース管理システムの使用

- [Windows Azure データ サービス](https://www.windowsazure.com/develop/net/data/)(マイクロソフト Azure サイト)。 テーブル[サービス機能ガイド](https://docs.microsoft.com/azure/)およびページの**ビッグ データ**セクションを参照してください。
- [ストレージ テーブル、キュー、および BLOB を使用した多層アプリケーションのASP.NET](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) (Microsoft Azure サイト)。 Windows Azure ストレージ NoSQL テーブルを使用するダウンロード可能なサンプル アプリケーションを使用したエンド ツー エンド のチュートリアル。

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>ASP.NET アプリケーションで LINQ クエリを使用する

- [ASP.NETデータ アクセス オプション](https://msdn.microsoft.com/library/ms178359.aspx#linq)(MSDN) LINQ の概要を示します。
- [LINQ トレーニング ビデオ](http://www.misfitgeek.com/windows-client-linq-training-videos-20/)(ジョー・スタッグナーのブログ)。
- [ASP.NET動的 LINQ リソースへのリンクを含むフォーラム スレッド](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq)。

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>動的データ スキャフォールディングの使用

- [動的データ プロジェクト テンプレート](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata)(MSDN) 動的データ プロジェクトを使用するタイミングに関するガイダンス。
- [ASP.NET動的データ](https://msdn.microsoft.com/library/ee845452.aspx)(MSDN)

<a id="securing"></a>

## <a name="securing-data-access"></a>データ アクセスのセキュリティ保護

- [ASP.NETでデータ アクセスをセキュリティで保護](https://msdn.microsoft.com/library/ms178375.aspx)する (MSDN)。
- [セキュリティに関する考慮事項 (エンティティ フレームワーク)](https://msdn.microsoft.com/library/cc716760.aspx) (MSDN)。
- [方法 : データ ソース コントロールを使用する場合に接続文字列をセキュリティで保護](https://msdn.microsoft.com/library/ms178372.aspx)する (MSDN)。

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>データ アクセス パフォーマンスの最適化

- [ASP.NETパフォーマンスの概要](https://msdn.microsoft.com/library/cc668225.aspx)(MSDN)
- [ASP.NET キャッシュ](https://msdn.microsoft.com/library/xsbfdd8c.aspx)(MSDN)
- [ASP.NETパフォーマンスの向上](https://msdn.microsoft.com/library/ff647787)(MSDN)。 このページの上部に「廃止されたコンテンツ」という警告がありますが、情報のほとんどは依然として関連しており、同等の更新リソースはありません。
- [SQL Server のパフォーマンスを向上](https://msdn.microsoft.com/library/ff647793)させる (MSDN)。 前のリンクと同じコメント。

このトピックの[「Entity Framework のパフォーマンスの最適化](#optimizingef)」も参照してください。

<a id="deploying"></a>

## <a name="deploying-a-database"></a>データベースの配置

- [ASP.NET Web 配置 - 推奨リソース](aspnet-web-deployment-content-map.md)(MSDN)

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>Web サービスを介したデータへのアクセス

- [Web サービスを通じてデータにアクセス](https://msdn.microsoft.com/library/ms178359.aspx#webservice)する (MSDN)。 Web API と WCF を使用するタイミングに関するガイダンス。
- [Web API の概要 ASP.NET](../web-api/index.md)。
- [WCF データ サービス](https://msdn.microsoft.com/data/bb931106)(MSDN)。

<a id="additional"></a>

## <a name="additional-resources"></a>その他のリソース

- [ASP.NETデータ アクセスに関する FAQ](https://msdn.microsoft.com/library/jj653753.aspx) (MSDN)
- [ASP.NET Web フォームチュートリアル - データ](../web-forms/overview/data-access/index.md). これらのチュートリアルのほとんどは比較的古いチュートリアルです。まず[、ASP.NETデータ アクセス オプション](https://msdn.microsoft.com/library/ms178359.aspx)と[データ ストレージ オプション (Windows Azure を使用した実際のクラウド アプリの構築)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md)を読んで、シナリオに合わないデータ アクセス方法に入らないようにしてください。
- [mvc コンテンツ マップをASP.NET](../mvc/overview/getting-started/recommended-resources-for-mvc.md)します。
- [ASP.NET Web ページチュートリアル - データ](../web-pages/overview/data/index.md).
- [データへのアクセス (MSDN)](https://msdn.microsoft.com/library/wzabh8c4.aspx) このコンテンツ マップに似ていますが、ASP.NETではなく Visual Studio に焦点を当てたリンクの一覧を示します。
