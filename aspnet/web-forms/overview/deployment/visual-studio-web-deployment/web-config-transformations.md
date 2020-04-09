---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 'ASP.NET Web 配置を使用して Visual Studio: Web.config ファイル変換 |マイクロソフトドキュメント'
author: tdykstra
description: このチュートリアル シリーズでは、azure App Service Web Apps またはサード パーティのホスティング プロバイダーに、ASP.NET Web アプリケーションをデプロイ (公開) する方法を示します。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675749"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>Visual Studio を使用した Web 配置のASP.NET: Web.config ファイル変換

[トム・ダイクストラ](https://github.com/tdykstra)著

[スタート プロジェクトのダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> このチュートリアル シリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、azure App Service Web Apps またはサード パーティのホスティング プロバイダーに ASP.NET Web アプリケーションをデプロイ (発行) する方法を示します。 シリーズの詳細については、[シリーズの最初のチュートリアルを](introduction.md)参照してください。

## <a name="overview"></a>概要

このチュートリアルでは *、Web.config*ファイルを別の配置先環境に配置するときに、ファイルを変更するプロセスを自動化する方法を示します。 ほとんどのアプリケーションは *、Web.config*ファイルに設定を持っていますが、アプリケーションを配置するときには異なる設定をする必要があります。 これらの変更を行うプロセスを自動化すると、展開するたびに手動で行う必要がなくなります。

リマインダー: チュートリアルを進める際にエラーメッセージが表示されたり、何かが機能しない場合は、[トラブルシューティングページ](troubleshooting.md)を確認してください。

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config 変換と Web 配置パラメーターの比較

*Web.config*ファイルの設定を変更するプロセスを自動化するには[、Web.config 変換](https://msdn.microsoft.com/library/dd465326.aspx)と[Web 配置パラメーター](https://msdn.microsoft.com/library/ff398068.aspx)の 2 つの方法があります。 *Web.config*変換ファイルには、配置時に*Web.config*ファイルを変更する方法を指定する XML マークアップが含まれています。 特定のビルド構成と特定の発行プロファイルに対して、異なる変更を指定できます。 既定のビルド構成はデバッグとリリースで、カスタム ビルド構成を作成できます。 発行プロファイルは、通常、宛先環境に対応します。 (発行プロファイルの詳細については、「[テスト環境としての IIS への展開](deploying-to-iis.md)」チュートリアルを参照してください)。

Web 配置パラメーターを使用すると *、Web.config*ファイル内の設定など、配置中に構成する必要があるさまざまな種類の設定を指定できます。 *Web.config*ファイルの変更を指定する場合、Web 配置パラメーターは設定が複雑になりますが、配置するまで設定する値がわからない場合に便利です。 たとえば、エンタープライズ環境では、*展開パッケージ*を作成し、実稼働環境でインストールする IT 部門の担当者に配布を提供し、そのユーザーが知らない接続文字列やパスワードを入力できるようにする必要があります。

このチュートリアル シリーズで説明するシナリオでは *、Web.config*ファイルに対して行う必要があるすべてのことを事前に把握しているので、Web 配置パラメーターを使用する必要はありません。 使用するビルド構成によって異なる変換と、使用する発行プロファイルによって異なる変換を構成します。

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>Azure での Web.config 設定の指定

変更する*Web.config*ファイルの設定が`<connectionStrings>``<appSettings>`要素または要素にある場合、Azure App Service で Web アプリにデプロイする場合は、デプロイ中に変更を自動化する別のオプションがあります。 Azure で有効にする設定を、Web アプリの管理ポータル ページの [**構成**] タブに入力できます (下にスクロールして **、アプリの設定**と**接続文字列**のセクションを表示します)。 プロジェクトをデプロイすると、Azure は変更を自動的に適用します。 詳細については、「 [Windows Azure Web サイト : アプリケーション文字列と接続文字列の動作 」](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)を参照してください。

## <a name="default-transformation-files"></a>既定の変換ファイル

**ソリューション エクスプローラー**で *[Web.config]* を展開し、2 つの既定のビルド構成に対して既定で作成される*Web.Debug.config*および*Web.Release.config*変換ファイルを表示します。

![ウェブconfig_transform_files](web-config-transformations/_static/image1.png)

カスタム ビルド構成の変換ファイルを作成するには、Web.config ファイルを右クリックし、コンテキスト メニューから **[構成変換の追加]** を選択します。 このチュートリアルでは、カスタム ビルド構成を作成していないため、この操作を行う必要はありません。

後で、テスト、ステージング、および運用の発行プロファイルにそれぞれ 1 つずつ、3 つの変換ファイルを作成します。 発行先の環境に依存するため、発行プロファイル変換ファイルで処理する設定の一般的な例は、テストと運用環境で異なる WCF エンドポイントです。 公開プロファイル変換ファイルは、公開プロファイルを作成した後、後のチュートリアルで作成します。

## <a name="disable-debug-mode"></a>デバッグ モードを無効にする

配置先環境ではなくビルド構成に依存する設定の例としては、`debug`属性があります。 リリース ビルドの場合、通常は、配置先の環境に関係なくデバッグを無効にします。 したがって、既定では、Visual Studio プロジェクト テンプレートは、要素から`debug`属性を削除するコードを使用して*Web.Release.config*変換ファイルを作成します。 `compilation` 次に示す既定の*Web.Release.config*は、コメントアウトされたいくつかのサンプル変換コードに加えて、属性を`compilation`削除する要素にコード`debug`が含まれています。

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

この`xdt:Transform="RemoveAttributes(debug)"`属性は、配置された`debug`*Web.config*ファイルの`system.web/compilation`要素から属性を削除することを指定します。 これは、リリース ビルドを配置するたびに行われます。

## <a name="limit-error-log-access-to-administrators"></a>エラー ログへのアクセスを管理者に制限する

アプリケーションの実行中にエラーが発生した場合、アプリケーションはシステム生成エラー ページの代わりに一般的なエラー ページを表示し、エラーログとレポートに[Elmah NuGet パッケージ](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)を使用します。 アプリケーション`customErrors` *Web.config*ファイル内の要素は、エラー ページを指定します。

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

エラー ページを表示するには、一時的に`mode`要素の属性`customErrors`を "RemoteOnly" から "On" に変更し、Visual Studio からアプリケーションを実行します。 エラーが発生するには *、"学生xxx.aspx"* などの無効な URL を要求します。 IIS で生成された "リソースが見つかりません" エラー ページの代わりに *、GenericErrorPage.aspx*ページが表示されます。

![エラー ページ](web-config-transformations/_static/image2.png)

エラー ログを表示するには、ポート番号の後の URL 内のすべてを*elmah.axd* (`http://localhost:51130/elmah.axd`たとえば) に置き換えて、Enter キーを押します。

![エルマページ](web-config-transformations/_static/image3.png)

完了したら、要素を`customErrors`"RemoteOnly"モードに戻すことを忘れないでください。

開発用コンピューターでは、エラー ログ ページへの無料アクセスを許可する便利ですが、運用環境ではセキュリティ上のリスクがあります。 運用サイトでは、エラー ログへのアクセスを管理者に制限する承認規則を追加し、テストとステージングでも必要な制限が機能することを確認します。 したがって、これはリリース ビルドを配置するたびに実装する必要があるもう 1 つの変更であるため *、Web.Release.config*ファイルに属します。

次に示すように *、Web.Release.config*を開き`location`、`configuration`終了タグの直前に新しい要素を追加します。

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

"`Transform`挿入" の属性値を指定`location`すると、この要素は*Web.config* `location`ファイル内の既存の要素に兄弟として追加されます。 (**更新クレジット**ページ`location`の承認規則を指定する要素が既に 1 つあります)。

これで、変換をプレビューして、正しくコーディングされていることを確認できます。

**ソリューション エクスプローラー**で*Web.Release.config*を右クリックし、[**変換のプレビュー**] をクリックします。

![[変換のプレビュー] メニュー](web-config-transformations/_static/image4.png)

左側に開発*用の Web.config*ファイルと、配置された*Web.config*ファイルが右側に表示され、変更が強調表示された状態で表示されるページが開きます。

![デバッグ変換のプレビュー](web-config-transformations/_static/image5.png)

![位置変換のプレビュー](web-config-transformations/_static/image6.png)

(プレビューでは、変換を記述していないいくつかの追加の変更に気付くかもしれません: これらは通常、機能に影響を与えない空白の削除を伴います)。

展開後にサイトをテストする場合は、承認規則が有効であることを確認するテストも行います。

> [!NOTE] 
> 
> **セキュリティに関する注意事項**プロダクション アプリケーションでは、エラーの詳細を公開したり、パブリックな場所に情報を格納したりしないでください。 攻撃者はエラー情報を使用して、サイトの脆弱性を発見することができます。 独自のアプリケーションで ELMAH を使用する場合は、セキュリティリスクを最小限に抑えるために ELMAH を構成します。 このチュートリアルの ELMAH の例は、推奨される構成とは見なされません。 アプリケーションがファイルを作成できるフォルダーを処理する方法を説明するために選択された例です。 詳細については、「 [ELMAH エンドポイントのセキュリティ保護](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)」を参照してください。

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>プロファイル変換ファイルの発行で処理する設定

一般的なシナリオでは、配置する環境ごとに異なる*Web.config*ファイルの設定を行う必要があります。 たとえば、WCF サービスを呼び出すアプリケーションは、テスト環境と運用環境で別のエンドポイントを必要とする場合があります。 Contoso 大学アプリケーションには、この種の設定も含まれています。 この設定は、サイトのページに表示されるインジケータを制御し、開発、テスト、運用など、どの環境に入っているかを示します。 設定値は、アプリケーションが*Site.Master*マスター ページのメイン見出しに "(Dev)" または "(Test)" を追加するかどうかを決定します。

![環境インジケータ](web-config-transformations/_static/image7.png)

アプリケーションがステージングまたはプロダクションで実行されている場合、環境標識は省略されます。

Contoso 大学 Web ページは、アプリケーションが実行`appSettings`されている環境を決定するために *、Web.config*ファイルで設定されている値を読み取ります。

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

値は、テスト環境では "Test" 、ステージングと運用の場合は "Prod" にする必要があります。

変換ファイルの次のコードは、この変換を実装します。

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

`xdt:Transform`属性値 "SetAttributes" は、この変換の目的が*Web.config*ファイル内の既存の要素の属性値を変更することを示します。 `xdt:Locator`属性値"Match(key)"は、変更する要素が、ここで指定された属性と`key`一致する`key`属性を持つ要素であることを示します。 `add`要素の他の属性は`value`、 で、配置された*Web.config*ファイルで変更されるものです。 ここに示すコードにより、`value`配置される`Environment``appSettings`*Web.config*ファイルで要素の属性が "Test" に設定されます。

この変換は、まだ作成していない発行プロファイル変換ファイルに属します。 テスト、ステージング、および運用環境の発行プロファイルを作成するときに、この変更を実装する変換ファイルを作成および更新します。 IIS[への展開](deploying-to-iis.md)で、運用環境のチュートリアル[に展開します](deploying-to-production.md)。

> [!NOTE]
> この設定は`<appSettings>`要素内にあるため、Azure アプリ サービスで Web アプリをデプロイするときに変換を指定する別の方法は、このトピックの前半の[「Azure での Web.config 設定の指定](#watransforms)」を参照してください。

## <a name="setting-connection-strings"></a>接続文字列の設定

既定の変換ファイルには接続文字列を更新する方法を示す例が含まれていますが、ほとんどの場合、発行プロファイルで接続文字列を指定できるため、接続文字列変換を設定する必要はありません。 IIS[への展開](deploying-to-iis.md)で、運用環境のチュートリアル[に展開します](deploying-to-production.md)。

## <a name="summary"></a>まとめ

これで、発行プロファイルを作成する前に*Web.config*変換を使用してできる限り多くの作業が完了し、配置された Web.config ファイルの内容のプレビューが表示されます。

![位置変換のプレビュー](web-config-transformations/_static/image8.png)

次のチュートリアルでは、プロジェクトのプロパティを設定する必要がある配置のセットアップ タスクを処理します。

## <a name="more-information"></a>詳細情報

このチュートリアルで扱うトピックの詳細については[、「Web.config 変換を使用して、配置中に配置中に Web.config 変換を使用して設定を変更](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms)する」を参照ASP.NET。

> [!div class="step-by-step"]
> [前へ](preparing-databases.md)
> [次へ](project-properties.md)
