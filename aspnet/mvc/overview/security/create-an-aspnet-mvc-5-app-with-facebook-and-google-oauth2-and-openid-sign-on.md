---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: フェイスブック、ツイッター、リンクトイン、グーグルOAuth2サインオン(C#)でMVC 5アプリを作成する |マイクロソフトドキュメント
author: Rick-Anderson
description: このチュートリアルでは、ユーザーが外部認証からの資格情報を使用して OAuth 2.0 を使用してログインできるようにする ASP.NET MVC 5 Web アプリケーションを構築する方法を示します。
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675917"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>Facebook、Twitter、LinkedIn、Google の OAuth2 サインオンを使用して ASP.NET MVC 5 アプリを作成する (C#)

[リック・アンダーソン](https://twitter.com/RickAndMSFT)著

> このチュートリアルでは、ユーザーがFacebook、Twitter、LinkedIn、マイクロソフト、Google などの外部認証プロバイダーからの資格情報を使用して[OAuth 2.0](http://oauth.net/2/)を使用してログインできるようにする、ASP.NET MVC 5 Web アプリケーションを構築する方法を示します。 簡単にするために、このチュートリアルでは、FacebookとGoogleからの資格情報を使用して作業することに焦点を当てています。
> 
> Web サイトでこれらの資格情報を有効にすると、何百万ものユーザーが既にこれらの外部プロバイダーにアカウントを持っているため、大きな利点があります。 これらのユーザーは、新しい資格情報のセットを作成して覚えておく必要がない場合は、サイトにサインアップする傾向が高くなります。
> 
> SMS[と電子メール 2 要素認証を使用して MVC 5 アプリをASP.NET](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)も参照してください。
> 
> このチュートリアルでは、ユーザーのプロファイル データを追加する方法、およびメンバーシップ API を使用してロールを追加する方法も示します。 このチュートリアルは[リック・アンダーソン](https://blogs.msdn.com/rickAndy)によって書かれた (Twitterで私[@RickAndMSFT](https://twitter.com/RickAndMSFT)に従ってください: ).

<a id="start"></a>
## <a name="getting-started"></a>作業の開始

まず、Web 用または[Visual Studio 2013 用の Visual Studio Express](https://go.microsoft.com/fwlink/?LinkId=299058) [2013](https://go.microsoft.com/fwlink/?LinkId=306566)をインストールして実行します。 Visual Studio [2013 更新プログラム 3](https://go.microsoft.com/fwlink/?LinkId=390521)以降をインストールします。 Dropbox、GitHub、リンクティン、インスタグラム、バッファ、セールスフォース、スチーム、スタックエクスチェンジ、トリジット、トゥイッチ、ツイッター、Yahoo!、その他のヘルプについては、この[サンプルプロジェクト](https://github.com/matthewdunsdon/oauthforaspnet)を参照してください。

> [!NOTE]
> Google OAuth 2 を使用して、SSL 警告なしでローカルでデバッグするには、Visual Studio [2013 更新プログラム 3](https://go.microsoft.com/fwlink/?LinkId=390521)以降をインストールする必要があります。

**[スタート**] ページで [**新しいプロジェクト**] をクリックするか、メニューを使用して **[ファイル**] をクリックし、[**新しいプロジェクト**] をクリックします。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a>最初のアプリケーションの作成

[**新しいプロジェクト**] をクリックし、左側の **[Visual C#]** を選択してから **、[Web]** を選択して **、[Web アプリケーションASP.NET]** を選択します。 プロジェクトに "MvcAuth" という名前を付け **、[OK]** をクリックします。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

[**新しいASP.NET プロジェクト**] ダイアログボックスで **、[MVC]** をクリックします。 [認証] が **[個別のユーザー アカウント**] でない場合は、[**認証の変更**] ボタンをクリックし、[**個別のユーザー アカウント**] を選択します。 **クラウドでホスト を**チェックすることで、アプリは Azure でホストすることが非常に簡単になります。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

**[クラウドでホスト**] を選択した場合は、[構成] ダイアログボックスに入力します。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>NuGet を使用して最新の OWIN ミドルウェアを更新する

NuGet パッケージ マネージャーを使用して[OWIN ミドルウェア](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)を更新する 。 左側のメニューで[**更新]** を選択します。 **[すべて更新**] ボタンをクリックするか、次の画像に示すように OWIN パッケージのみを検索できます。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

下の図では、OWIN パッケージのみが表示されます。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

パッケージ マネージャ コンソール (PMC) からコマンド`Update-Package`を入力すると、すべてのパッケージが更新されます。

**F5**キーまたは**Ctrl キーを押しながら F5 キー**を押して、アプリケーションを実行します。 下の図では、ポート番号は 1234 です。 アプリケーションを実行すると、別のポート番号が表示されます。

ブラウザウィンドウのサイズによっては、ナビゲーションアイコンをクリックして **、ホーム**、**情報**、**連絡先**、**登録**、ログインの各リンク**を**表示する必要があります。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>プロジェクトでの SSL の設定

グーグルやフェイスブックなどの認証プロバイダに接続するには、SSLを使用するようにIIS-Expressを設定する必要があります。 ログイン後もSSLを使用し続け、HTTPに戻らないようにすることが重要であり、ログインクッキーはあなたのユーザー名とパスワードと同じくらい秘密であり、SSLを使用せずにワイヤーを介してクリアテキストで送信します。 また、MVC パイプラインが実行される前にハンドシェイクを実行し、チャネル (HTTPS が HTTP よりも遅くなる部分の大部分) をセキュリティで保護する時間が既に取られているため、ログイン後に HTTP にリダイレクトしても、現在の要求や今後の要求が大幅に速くなりません。

1. **ソリューション エクスプローラー**で **、MvcAuth**プロジェクトをクリックします。
2. F4 キーを押してプロジェクトのプロパティを表示します。 または、[**表示**] メニューの [**プロパティ ウィンドウ]** を選択することもできます。
3. **[SSL の有効化**] を [True] に変更します。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. SSL URL をコピーします`https://localhost:44300/`(他の SSL プロジェクトを作成していない場合)。
5. **ソリューション エクスプローラー**で **、 MvcAuth**プロジェクトを右クリックし、[**プロパティ ]** をクリックします。
6. **[Web]** タブを選択し、[**プロジェクト URL]** ボックスに SSL URL を貼り付けます。 ファイルを保存します (Ctl+S)。 FacebookとGoogleの認証アプリを設定するには、このURLが必要です。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. すべての要求で HTTPS を`Home`使用する必要がある場合は[、RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)属性をコントローラーに追加します。 より安全な方法は、アプリケーションに[RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)フィルターを追加することです。 「SSL&quot;によるアプリケーションの保護」セクションと「認証&quot;と SQL DB を[使用してASP.NET MVC アプリを作成し、Azure App Service にデプロイする](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)」の「属性を認証する」を参照してください。 ホームコントローラの一部を以下に示します。

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。 過去に証明書をインストールした場合は、このセクションの残りの部分をスキップして[、OAuth 2 用の Google アプリを作成し、プロジェクトに接続するに](#goog)移動し、指示に従って IIS Express が生成した自己署名証明書を信頼します。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. localhost を表す証明書をインストールする場合は、**セキュリティの警告**ダイアログを読み、[**はい**] をクリックします。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. IE は *ホーム* ページを表示し、SSL の警告はありません。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome も証明書を受け入れ、警告なしに HTTPS コンテンツを表示します。 Firefox は独自の証明書ストアを使用するため、警告が表示されます。 このアプリケーションでは、[**リスクを理解しています**] をクリックしても安全に行うことができます。   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>OAuth 2 用の Google アプリを作成し、アプリをプロジェクトに接続する

> [!WARNING]
> 現在の Google OAuth の手順については[、「ASP.NETコアでの Google 認証の設定](/aspnet/core/security/authentication/social/google-logins)」を参照してください。

1. [Google Developers Console](https://console.developers.google.com/)にアクセスします。
2. プロジェクトをまだ作成していない場合は、左側のタブで **[認証情報**] を選択し、[**作成**] を選択します。
3. 左側のタブで 、[**資格情報**] をクリックします。
4. [**資格情報の作成****]、[OAuth クライアント ID]** の順にクリックします。 

    1. [**クライアント ID**の作成] ダイアログで、アプリケーションの種類に応える既定の Web**アプリケーション**をそのまま使用します。
    2. **認証された JavaScript**オリジンを上記で使用した SSL`https://localhost:44300/` URL に設定します (他の SSL プロジェクトを作成していない場合)。
    3. **許可されたリダイレクト URI**を次の値に設定します。  
         `https://localhost:44300/signin-google`
5. OAuth 同意画面のメニュー項目をクリックし、電子メール アドレスと製品名を設定します。 フォームに入力したら、[**保存**] をクリックします。
6. [ライブラリ] メニュー項目をクリックし **、Google+ API**を検索し、それをクリックして [有効] を押します。
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   次の図は、有効な API を示しています。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. Google API マネージャで[**認証情報**]タブにアクセスし、**クライアント ID**を取得します。 ダウンロードして、アプリケーションシークレットと共に JSON ファイルを保存します。 **ClientId**と**ClientSecret**をコピーして`UseGoogleAuthentication`*、App_Start*フォルダーの*Startup.Auth.cs*ファイルにあるメソッドに貼り付けます。 以下に示す**クライアント ID**値と**クライアント シークレット**値はサンプルであり、動作しません。

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > セキュリティ - ソース コードに機密データを格納しないでください。 アカウントと資格情報は、サンプルをシンプルに保つために上記のコードに追加されます。 [ASP.NETと Azure アプリ サービスにパスワードやその他の機密データをデプロイするためのベスト プラクティスを](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)参照してください。
8. **Ctrl キーを押しながら F5 キー**を押して、アプリケーションをビルドして実行します。 **[Log in]** リンクをクリックします。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. [**別のサービスを使用してログイン**] の下にある **[Google]** をクリックします。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > 上記の手順のいずれかを見逃すと、HTTP 401エラーが発生します。 上記の手順を再確認してください。 必要な設定 (**製品名**など) を見逃した場合は、不足しているアイテムを追加して保存します。認証が機能するまでに数分かかることがあります。
10. 認証情報を入力する Google サイトにリダイレクトされます。   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. 資格情報を入力すると、作成した Web アプリケーションにアクセス許可を与えるプロンプトが表示されます。
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. **[Accept]\(受け入れる\)** をクリックします。 これで、Google アカウントを登録できる MvcAuth アプリケーションの **[登録**] ページにリダイレクトされます。 Google アカウントに使用するローカルの電子メール登録名を変更できますが、通常は既定の電子メール エイリアス (認証に使用したエイリアス) を変更しません。 **[登録]** をクリックします。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>Facebookでアプリを作成し、プロジェクトにアプリを接続する

> [!WARNING]
> 現在の Facebook OAuth2 認証手順については[、Facebook 認証の設定を](/aspnet/core/security/authentication/social/facebook-logins)参照してください。

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>メンバーシップ データを確認する

[**表示**] メニューの [**サーバー エクスプローラ**] をクリックします。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

**[既定の接続 (MvcAuth)]** を展開し **、[テーブル**] を展開し **、[AspNetUsers]** を右クリックして 、[**テーブル データの表示**] をクリックします。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers テーブル データ](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>ユーザー クラスへのプロファイル データの追加

このセクションでは、次の図に示すように、登録時にユーザー データに生年月日と出身地を追加します。

![故郷とBdayとのreg](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

*モデル\IdentityModels.cs*ファイルを開き、生年月日とホームタウンのプロパティを追加します。

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

*モデル\AccountViewModels.cs*ファイルと設定された生年月日とホームタウンの`ExternalLoginConfirmationViewModel`プロパティを開きます。

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

*コントローラ\AccountController.cs*ファイルを開き、次のようにアクションメソッドで生年月日と`ExternalLoginConfirmation`故郷のコードを追加します。

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

生年月日と故郷を*ビュー\アカウント\外部ログイン確認.cshtml*ファイルに追加します。

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

メンバーシップデータベースを削除して、Facebookアカウントをアプリケーションに再登録し、新しい生年月日とホームタウンのプロフィール情報を追加できることを確認します。

**ソリューション エクスプローラー**で 、[**すべてのファイルの表示**] アイコンをクリックし、[*データの\_追加]、[aspnet-MvcAuth-&lt;dateStamp&gt;.mdf]* の順にクリックして 、[**削除**] をクリックします。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

[**ツール**] メニューの **[NuGet パッケージ マネージャ**] をクリックし、[パッケージ マネージャー**コンソール**(PMC)] をクリックします。 PMCに次のコマンドを入力します。

1. 移行を有効にする
2. アドイン移行のイニト
3. データベースの更新

アプリケーションを実行し、ログインし、一部のユーザーを登録するには、FaceBookとGoogleを使用しています。

## <a name="examine-the-membership-data"></a>メンバーシップ データを確認する

[**表示**] メニューの [**サーバー エクスプローラ**] をクリックします。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

**AspNetUsers**を右クリックし、[**テーブル データの表示**] をクリックします。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

および`HomeTown``BirthDate`フィールドは以下に示します。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>アプリをログオフして別のアカウントでログインする

Facebookでアプリにログインし、ログアウトして(同じブラウザを使用して)別のFacebookアカウントでログインしようとすると、すぐに以前に使用していたFacebookアカウントにログインします。 別のアカウントを使用するには、Facebookに移動してFacebookでログアウトする必要があります。 同じ規則が他のサード パーティ認証プロバイダにも適用されます。 別のブラウザを使用して、別のアカウントでログインすることもできます。

## <a name="next-steps"></a>次の手順

YahooとLinkedInの指示のためのジェリー・ペルサーによる[OWINのためのヤフーとLinkedIn OAuthセキュリティプロバイダの紹介](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/)を参照してください。 ソーシャルログインボタンを有効にするには、MVC 5ASP.NETJerrieのかなりソーシャルログインボタンを参照してください。

このチュートリアルを続けて、次の手順を示す、[認証と SQL DB を使用して ASP.NET MVC アプリを作成し、Azure アプリ サービス にデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)するチュートリアルに従ってください。

1. アプリを Azure にデプロイする方法。
2. ロールを使用してアプリを保護する方法。
3. [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx)フィルターと[承認](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)フィルターを使用してアプリを保護する方法。
4. メンバーシップ API を使用してユーザーとロールを追加する方法。

このチュートリアルを気に入った方法と改善できる内容についてのフィードバックを残してください。 新しいトピックは、「[コードを使用して表示する方法」でも](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)リクエストできます。 ASP.NETに追加する新機能を要求して投票することもできます。 たとえば、ツールに投票して[、ユーザーとロールを作成および管理できます。](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)

外部認証サービスの仕組ASP.NET詳細については、 Robert McMurray の[外部認証サービス](https://asp.net/web-api/overview/security/external-authentication-services)を参照してください。 ロバートの記事では、マイクロソフトとTwitterの認証を有効にする方法についても詳しく説明しています。 Tom Dykstra の優れた[EF/MVC チュートリアル](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)では、エンティティ フレームワークを操作する方法を示します。
