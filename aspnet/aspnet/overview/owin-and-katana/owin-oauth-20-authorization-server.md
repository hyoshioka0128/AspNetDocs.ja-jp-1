---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 承認サーバー |マイクロソフトドキュメント
author: hongyes
description: このチュートリアルでは、OWIN OAuth ミドルウェアを使用して OAuth 2.0 承認サーバーを実装する方法について説明します。 これは唯一のoutlin..の高度なチュートリアルです。
ms.author: riande
ms.date: 03/20/2014
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: d758fa2639d10e1b7be8d87c5d1f7adb7e292ac7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540409"
---
<a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="2f7ac-104">OWIN OAuth 2.0 承認サーバー</span><span class="sxs-lookup"><span data-stu-id="2f7ac-104">OWIN OAuth 2.0 Authorization Server</span></span>
====================
<span data-ttu-id="2f7ac-105">[ホンジェ・サン](https://github.com/hongyes)と[プラブラージ・チアガラジャン](https://github.com/Praburaj)</span><span class="sxs-lookup"><span data-stu-id="2f7ac-105">by [Hongye Sun](https://github.com/hongyes) and [Praburaj Thiagarajan](https://github.com/Praburaj)</span></span>

> <span data-ttu-id="2f7ac-106">このチュートリアルでは、OWIN OAuth ミドルウェアを使用して OAuth 2.0 承認サーバーを実装する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-106">This tutorial will guide you on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span> <span data-ttu-id="2f7ac-107">これは、OWIN OAuth 2.0 承認サーバーを作成する手順の概要のみを説明する高度なチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-107">This is an advanced tutorial that only outlines the steps to create an OWIN OAuth 2.0 Authorization Server.</span></span> <span data-ttu-id="2f7ac-108">これは、ステップバイステップチュートリアルではありません。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-108">This is not a step by step tutorial.</span></span> <span data-ttu-id="2f7ac-109">[サンプル コードをダウンロード](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-109">[Download the sample code](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip).</span></span>
>
> > [!NOTE]
> > <span data-ttu-id="2f7ac-110">この概要は、安全な運用アプリの作成に使用することを目的としていません。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-110">This outline should not be intended to be used for creating a secure production app.</span></span> <span data-ttu-id="2f7ac-111">このチュートリアルでは、OWIN OAuth ミドルウェアを使用して OAuth 2.0 承認サーバーを実装する方法の概要のみを提供します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-111">This tutorial is intended to provide only an outline on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span>
>
>
> ## <a name="software-versions"></a><span data-ttu-id="2f7ac-112">ソフトウェアバージョン</span><span class="sxs-lookup"><span data-stu-id="2f7ac-112">Software versions</span></span>
>
> | <span data-ttu-id="2f7ac-113">**チュートリアルで示されている**</span><span class="sxs-lookup"><span data-stu-id="2f7ac-113">**Shown in the tutorial**</span></span> | <span data-ttu-id="2f7ac-114">**また、で動作します**</span><span class="sxs-lookup"><span data-stu-id="2f7ac-114">**Also works with**</span></span> |
> | --- | --- |
> | <span data-ttu-id="2f7ac-115">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="2f7ac-115">Windows 8.1</span></span> | <span data-ttu-id="2f7ac-116">ウィンドウズ 8, ウィンドウズ 7</span><span class="sxs-lookup"><span data-stu-id="2f7ac-116">Windows 8, Windows 7</span></span> |
> | [<span data-ttu-id="2f7ac-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2f7ac-117">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) | <span data-ttu-id="2f7ac-118">[デスクトップ用のビジュアル スタジオ 2013 エクスプレス](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express).</span><span class="sxs-lookup"><span data-stu-id="2f7ac-118">[Visual Studio 2013 Express for Desktop](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express).</span></span> <span data-ttu-id="2f7ac-119">Visual Studio 2012 の最新の更新プログラムは動作するはずですが、チュートリアルではテストされておらず、一部のメニューの選択とダイアログ ボックスが異なります。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-119">Visual Studio 2012 with the latest update should work, but the tutorial has not been tested with it, and some menu selections and dialog boxes are different.</span></span> |
> | <span data-ttu-id="2f7ac-120">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="2f7ac-120">.NET 4.5</span></span> |  |
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="2f7ac-121">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="2f7ac-121">Questions and Comments</span></span>
>
> <span data-ttu-id="2f7ac-122">チュートリアルに直接関連しない質問がある場合は[、GitHub の Katana プロジェクトで](https://github.com/aspnet/AspNetKatana/)投稿できます。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-122">If you have questions that are not directly related to the tutorial, you can post them at [Katana Project on GitHub](https://github.com/aspnet/AspNetKatana/).</span></span> <span data-ttu-id="2f7ac-123">チュートリアル自体に関する質問やコメントについては、ページの下部にあるコメントセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-123">For questions and comments regarding the tutorial itself, see the comments section at the bottom of the page.</span></span>


<span data-ttu-id="2f7ac-124">[OAuth 2.0 フレームワーク](http://tools.ietf.org/html/rfc6749)を使用すると、サードパーティ製のアプリが HTTP サービスへのアクセスを制限できます。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-124">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="2f7ac-125">保護されたリソースにアクセスするためにリソース所有者の資格情報を使用する代わりに、クライアントはアクセス トークン (特定のスコープ、有効期間、およびその他のアクセス属性を示す文字列) を取得します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-125">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="2f7ac-126">アクセス トークンは、リソース所有者の承認を得て、承認サーバーによってサードパーティのクライアントに発行されます。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-126">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="2f7ac-127">このチュートリアルでは、以下について説明します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-127">This tutorial will cover:</span></span>

- <span data-ttu-id="2f7ac-128">承認サーバーを作成して、4 つの承認許可タイプと更新トークンをサポートする方法:</span><span class="sxs-lookup"><span data-stu-id="2f7ac-128">How to create an authorization server to support four authorization grant types and refresh tokens:</span></span>
    - <span data-ttu-id="2f7ac-129">認証コードの付与</span><span class="sxs-lookup"><span data-stu-id="2f7ac-129">Authorization code grant</span></span>
    - <span data-ttu-id="2f7ac-130">暗黙的な許可</span><span class="sxs-lookup"><span data-stu-id="2f7ac-130">Implicit Grant</span></span>
    - <span data-ttu-id="2f7ac-131">リソース所有者パスワード資格情報の付与</span><span class="sxs-lookup"><span data-stu-id="2f7ac-131">Resource Owner Password Credentials Grant</span></span>
    - <span data-ttu-id="2f7ac-132">クライアント資格情報の付与</span><span class="sxs-lookup"><span data-stu-id="2f7ac-132">Client Credentials Grant</span></span>
- <span data-ttu-id="2f7ac-133">アクセス トークンによって保護されるリソース サーバーを作成する。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-133">Creating a resource server which is protected by an access token.</span></span>
- <span data-ttu-id="2f7ac-134">OAuth 2.0 クライアントを作成しています。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-134">Creating OAuth 2.0 clients.</span></span>

<a id="prerequisites"></a>
## <a name="prerequisites"></a><span data-ttu-id="2f7ac-135">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="2f7ac-135">Prerequisites</span></span>

- <span data-ttu-id="2f7ac-136">ページ上部の**ソフトウェア バージョン**に示されているように[、Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions)または無料の[Visual Studio Express 2013。](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)</span><span class="sxs-lookup"><span data-stu-id="2f7ac-136">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) or the free [Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express), as indicated in **Software Versions** at the top of the page.</span></span>
- <span data-ttu-id="2f7ac-137">OWIN に精通しています。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-137">Familiarity with OWIN.</span></span> <span data-ttu-id="2f7ac-138">[「カタナ プロジェクトの概要](https://msdn.microsoft.com/magazine/dn451439.aspx)」および[「OWIN とカタナの新機能](index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-138">See [Getting Started with the Katana Project](https://msdn.microsoft.com/magazine/dn451439.aspx) and [What's new in OWIN and Katana](index.md).</span></span>
- <span data-ttu-id="2f7ac-139">[ロール](http://tools.ietf.org/html/rfc6749#section-1.1)、[プロトコル フロー](http://tools.ietf.org/html/rfc6749#section-1.2)、[承認許可](http://tools.ietf.org/html/rfc6749#section-1.3)などの[OAuth](http://tools.ietf.org/html/rfc6749)用語に精通しています。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-139">Familiarity with [OAuth](http://tools.ietf.org/html/rfc6749) terminology, including [Roles](http://tools.ietf.org/html/rfc6749#section-1.1), [Protocol Flow](http://tools.ietf.org/html/rfc6749#section-1.2), and [Authorization Grant](http://tools.ietf.org/html/rfc6749#section-1.3).</span></span> <span data-ttu-id="2f7ac-140">[OAuth 2.0 の導入は](http://tools.ietf.org/html/rfc6749#section-1)、良い紹介を提供します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-140">[OAuth 2.0 introduction](http://tools.ietf.org/html/rfc6749#section-1) provides a good introduction.</span></span>

## <a name="create-an-authorization-server"></a><span data-ttu-id="2f7ac-141">承認サーバーの作成</span><span class="sxs-lookup"><span data-stu-id="2f7ac-141">Create an Authorization Server</span></span>

<span data-ttu-id="2f7ac-142">このチュートリアルでは、承認サーバーを作成する[OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx)と ASP.NET MVC を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-142">In this tutorial, we will roughly sketch out how to use [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) and ASP.NET MVC to create an authorization server.</span></span> <span data-ttu-id="2f7ac-143">このチュートリアルでは各ステップが含まれていないため、完成したサンプルのダウンロードをすぐに提供したいと考えています。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-143">We hope to soon provide a download for the completed sample, as this tutorial does not include each step.</span></span> <span data-ttu-id="2f7ac-144">まず、*認証サーバー*という名前の空の Web アプリケーションを作成し、次のパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-144">First, create an empty web app named *AuthorizationServer* and install the following packages:</span></span>

- <span data-ttu-id="2f7ac-145">マイクロソフト.AspNet.Mvc</span><span class="sxs-lookup"><span data-stu-id="2f7ac-145">Microsoft.AspNet.Mvc</span></span>
- <span data-ttu-id="2f7ac-146">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="2f7ac-146">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="2f7ac-147">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="2f7ac-147">Microsoft.Owin.Security.OAuth</span></span>
- <span data-ttu-id="2f7ac-148">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="2f7ac-148">Microsoft.Owin.Security.Cookies</span></span>
- <span data-ttu-id="2f7ac-149">マイクロソフト.Owin.Security.グーグル(またはマイクロソフト.Owin.Security.Facebookなどの他のソーシャルログインパッケージ)</span><span class="sxs-lookup"><span data-stu-id="2f7ac-149">Microsoft.Owin.Security.Google (Or any other social login package such as Microsoft.Owin.Security.Facebook)</span></span>

<span data-ttu-id="2f7ac-150">スタートアップ という名前のプロジェクト ルート フォルダの下に[、OWIN](owin-startup-class-detection.md) *スタートアップ*クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-150">Add an [OWIN Startup class](owin-startup-class-detection.md) under the project root folder named *Startup*.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

<span data-ttu-id="2f7ac-151">*\_アプリケーションのスタート*フォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-151">Create an *App\_Start* folder.</span></span> <span data-ttu-id="2f7ac-152">*[アプリケーションの\_開始]* フォルダーを選択し、Shift + Alt + A を使用して、ダウンロードしたバージョンの*AuthorizationServer\\_アプリケーション開始\スタートアップ.Auth.cs*ファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-152">Select the *App\_Start* folder and use Shift+Alt+A to add the downloaded version of the *AuthorizationServer\App\_Start\Startup.Auth.cs* file.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

<span data-ttu-id="2f7ac-153">上記のコードは、許可サーバー自体がアカウントを管理するために使用する、アプリケーション/外部サインインクッキーとGoogle認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-153">The code above enables application/external sign in cookies and Google authentication, which are used by authorization server itself to manage accounts.</span></span>

<span data-ttu-id="2f7ac-154">拡張`UseOAuthAuthorizationServer`方法は、承認サーバーをセットアップすることです。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-154">The `UseOAuthAuthorizationServer` extension method is to setup the authorization server.</span></span> <span data-ttu-id="2f7ac-155">セットアップ オプションは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-155">The setup options are:</span></span>

- <span data-ttu-id="2f7ac-156">`AuthorizeEndpointPath`: ユーザーがトークンまたはコードを発行することに同意するために、クライアント アプリケーションがユーザー エージェントをリダイレクトする要求パス。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-156">`AuthorizeEndpointPath`: The request path where client applications will redirect the user-agent in order to obtain the users consent to issue a token or code.</span></span> <span data-ttu-id="2f7ac-157">先頭のスラッシュ (""`/Authorize`など) で始める必要があります。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-157">It must begin with a leading slash, for example, "`/Authorize`".</span></span>
- <span data-ttu-id="2f7ac-158">`TokenEndpointPath`: クライアント アプリケーションが直接通信してアクセス トークンを取得する要求パス。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-158">`TokenEndpointPath`: The request path client applications directly communicate to obtain the access token.</span></span> <span data-ttu-id="2f7ac-159">先頭のスラッシュ ("/Token" など) で始める必要があります。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-159">It must begin with a leading slash, like "/Token".</span></span> <span data-ttu-id="2f7ac-160">クライアントが[クライアント\_シークレット](http://tools.ietf.org/html/rfc6749#appendix-A.2)を発行される場合は、このエンドポイントにクライアントシークレットを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-160">If the client is issued a [client\_secret](http://tools.ietf.org/html/rfc6749#appendix-A.2), it must be provided to this endpoint.</span></span>
- <span data-ttu-id="2f7ac-161">`ApplicationCanDisplayErrors`: Web`true`アプリケーションがエンドポイントでクライアント検証エラーのカスタム エラー ページを生成する`/Authorize`場合にに設定します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-161">`ApplicationCanDisplayErrors`: Set to `true` if the web application wants to generate a custom error page for the client validation errors on `/Authorize` endpoint.</span></span> <span data-ttu-id="2f7ac-162">これは、ブラウザがクライアント アプリケーションにリダイレクトされない場合(たとえば、 または`client_id``redirect_uri`が正しくない場合など)にのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-162">This is only needed for cases where the browser is not redirected back to the client application, for example, when the `client_id` or `redirect_uri` are incorrect.</span></span> <span data-ttu-id="2f7ac-163">エンドポイント`/Authorize`は"oauth"を見ることを期待するはずです。エラー」、"oauth。エラー説明」と「oauth。"ErrorUri" プロパティが OWIN 環境に追加されます。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-163">The `/Authorize` endpoint should expect to see the "oauth.Error", "oauth.ErrorDescription", and "oauth.ErrorUri" properties are added to the OWIN environment.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2f7ac-164">true でない場合、承認サーバーはエラーの詳細を示す既定のエラー ページを返します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-164">If not true, the authorization server will return a default error page with the error details.</span></span>
- <span data-ttu-id="2f7ac-165">`AllowInsecureHttp`: 承認要求とトークン要求を HTTP URI アドレスに到着させ、受信`redirect_uri`承認要求パラメーターに HTTP URI アドレスを持たできるようにする場合は True。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-165">`AllowInsecureHttp`: True to allow authorize and token requests to arrive on HTTP URI addresses, and to allow incoming `redirect_uri` authorize request parameters to have HTTP URI addresses.</span></span>

    > [!WARNING]
    > <span data-ttu-id="2f7ac-166">セキュリティ - これは開発専用です。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-166">Security - This is for development only.</span></span>
- <span data-ttu-id="2f7ac-167">`Provider`: 承認サーバーミドルウェアによって発生したイベントを処理するためにアプリケーションによって提供されるオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-167">`Provider`: The object provided by the application to process events raised by the Authorization Server middleware.</span></span> <span data-ttu-id="2f7ac-168">アプリケーションは、インターフェイスを完全に実装するか、またはインスタンスを作成`OAuthAuthorizationServerProvider`し、このサーバーがサポートする OAuth フローに必要なデリゲートを割り当てる場合があります。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-168">The application may implement the interface fully, or it may create an instance of `OAuthAuthorizationServerProvider` and assign delegates necessary for the OAuth flows this server supports.</span></span>
- <span data-ttu-id="2f7ac-169">`AuthorizationCodeProvider`: クライアント アプリケーションに戻るための、単独使用の認証コードを生成します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-169">`AuthorizationCodeProvider`: Produces a single-use authorization code to return to the client application.</span></span> <span data-ttu-id="2f7ac-170">OAuth サーバーをセキュリティで保護するには、`OnCreate/OnCreateAsync`イベントによって生成されたトークン`AuthorizationCodeProvider`が 1 回の呼び出しに対してのみ有効と`OnReceive/OnReceiveAsync`見なされるインスタンスをアプリケーションに提供**する必要があります**。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-170">For the OAuth server to be secure the application **MUST** provide an instance for `AuthorizationCodeProvider` where the token produced by the `OnCreate/OnCreateAsync` event is considered valid for only one call to `OnReceive/OnReceiveAsync`.</span></span>
- <span data-ttu-id="2f7ac-171">`RefreshTokenProvider`: 必要に応じて新しいアクセス トークンを生成するために使用できる更新トークンを生成します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-171">`RefreshTokenProvider`: Produces a refresh token which may be used to produce a new access token when needed.</span></span> <span data-ttu-id="2f7ac-172">指定しない場合、承認サーバーはエンドポイントから更新トークンを`/Token`返しません。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-172">If not provided the authorization server will not return refresh tokens from the `/Token` endpoint.</span></span>

## <a name="account-management"></a><span data-ttu-id="2f7ac-173">アカウント管理</span><span class="sxs-lookup"><span data-stu-id="2f7ac-173">Account Management</span></span>

<span data-ttu-id="2f7ac-174">OAuth は、ユーザー アカウント情報をどこでどのように管理するかは気にしません。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-174">OAuth doesn't care where or how you manage your user account information.</span></span> <span data-ttu-id="2f7ac-175">それはそれを担当する[ASP.NETアイデンティティ](../../../identity/index.md)です。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-175">It's [ASP.NET Identity](../../../identity/index.md) which is responsible for it.</span></span> <span data-ttu-id="2f7ac-176">このチュートリアルでは、アカウント管理コードを簡素化し、ユーザーが OWIN クッキーミドルウェアを使用してログインできることを確認します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-176">In this tutorial, we will simplify the account management code and just make sure that user can login using OWIN cookie middleware.</span></span> <span data-ttu-id="2f7ac-177">以下は、 のサンプル コードの`AccountController`簡略化です。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-177">Here is the simplified sample code for the `AccountController`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

<span data-ttu-id="2f7ac-178">`ValidateClientRedirectUri`は、登録されたリダイレクト URL を使用してクライアントを検証するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-178">`ValidateClientRedirectUri` is used to validate the client with its registered redirect URL.</span></span> <span data-ttu-id="2f7ac-179">`ValidateClientAuthentication`は、基本スキームヘッダーとフォーム本体をチェックして、クライアントの資格情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-179">`ValidateClientAuthentication` checks the basic scheme header and form body to get the client's credentials.</span></span>

<span data-ttu-id="2f7ac-180">ログインページは以下の通りです:</span><span class="sxs-lookup"><span data-stu-id="2f7ac-180">The login page is shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image1.png)

<span data-ttu-id="2f7ac-181">IETF の OAuth 2[認証コードの付与](http://tools.ietf.org/html/rfc6749#section-4.1)セクションを今すぐ確認します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-181">Review the IETF's OAuth 2 [Authorization Code Grant](http://tools.ietf.org/html/rfc6749#section-4.1) section now.</span></span>

<span data-ttu-id="2f7ac-182">**プロバイダ**(下の表) は[OAuth 認証サーバー オプションです](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx)。プロバイダー ( 型`OAuthAuthorizationServerProvider`) には、すべての OAuth サーバー イベントが含まれます。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-182">**Provider** (in the table below) is [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx).Provider, which is of type `OAuthAuthorizationServerProvider`, which contains all OAuth server events.</span></span>

| <span data-ttu-id="2f7ac-183">[承認コードの付与] セクションからのフロー ステップ</span><span class="sxs-lookup"><span data-stu-id="2f7ac-183">Flow steps from Authorization Code Grant section</span></span> | <span data-ttu-id="2f7ac-184">サンプルダウンロードでは、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-184">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="2f7ac-185">(A) クライアントは、リソース所有者のユーザー・エージェントを許可エンドポイントに指示することによって、フローを開始します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-185">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="2f7ac-186">クライアントには、クライアント ID、要求されたスコープ、ローカル状態、およびアクセスが許可 (または拒否) された後に承認サーバーがユーザー エージェントを返信するリダイレクト URI が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-186">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="2f7ac-187">プロバイダー.マッチエンドポイント プロバイダー.検証クライアント リダイレクト Uri プロバイダー.検証承認要求プロバイダー.承認エンドポイント</span><span class="sxs-lookup"><span data-stu-id="2f7ac-187">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="2f7ac-188">(B) 認可サーバは、ユーザ エージェントを介してリソース所有者を認証し、リソース所有者がクライアントのアクセス要求を許可するか拒否するかを確立します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-188">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="2f7ac-189">**ユーザーがアクセス&gt;を許可する場合&lt;** プロバイダー.マッチエンドポイント プロバイダー.検証クライアント リダイレクト Uri プロバイダー.検証承認要求プロバイダー.承認エンドポイント認証コードプロバイダー。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-189">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="2f7ac-190">(C) リソース所有者がアクセス権を付与すると仮定すると、承認サーバーは、(要求またはクライアントの登録中に) 前に提供されたリダイレクト URI を使用して、ユーザーエージェントをクライアントにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-190">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="2f7ac-191">...</span><span class="sxs-lookup"><span data-stu-id="2f7ac-191">...</span></span> |  |
|  |  |
| <span data-ttu-id="2f7ac-192">(D) クライアントは、前の手順で受信した認証コードを含めることによって、承認サーバーのトークン エンドポイントからアクセス トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-192">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="2f7ac-193">要求を行う際、クライアントは承認サーバーで認証します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-193">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="2f7ac-194">クライアントには、検証用の認証コードを取得するために使用されるリダイレクト URI が含まれています。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-194">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> | <span data-ttu-id="2f7ac-195">プロバイダー.マッチエンドポイントプロバイダー.検証クライアント認証認証コードプロバイダー.受信非同期プロバイダー.検証トークン要求プロバイダー.承認コードプロバイダー.トークンエンドポイントアクセストークンプロバイダー.CreateAsyncリフレッシュトークンプロバイダ.</span><span class="sxs-lookup"><span data-stu-id="2f7ac-195">Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |

<span data-ttu-id="2f7ac-196">認証コードの作成`AuthorizationCodeProvider.CreateAsync`と`ReceiveAsync`検証を制御するためのサンプル実装を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-196">A sample implementation for `AuthorizationCodeProvider.CreateAsync` and `ReceiveAsync` to control the creation and validation of authorization code is shown below.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

<span data-ttu-id="2f7ac-197">上記のコードでは、メモリ内の同時実行辞書を使用してコードと ID チケットを格納し、コードを受信した後に ID を復元します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-197">The code above uses an in-memory concurrent dictionary to store the code and identity ticket and restore the identity after receiving the code.</span></span> <span data-ttu-id="2f7ac-198">実際のアプリケーションでは、永続データ ストアに置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-198">In a real application, it would be replaced by a persistent data store.</span></span> <span data-ttu-id="2f7ac-199">承認エンドポイントは、リソース所有者がクライアントにアクセス権を付与するためのエンドポイントです。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-199">The authorization endpoint is for the resource owner to grant access to the client.</span></span> <span data-ttu-id="2f7ac-200">通常、ユーザーがボタンをクリックして許可を確認できるようにするには、ユーザー インターフェイスが必要です。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-200">Usually, it needs a user interface to allow the user to click a button and confirm the grant.</span></span> <span data-ttu-id="2f7ac-201">OWIN OAuth ミドルウェアを使用すると、アプリケーション コードで承認エンドポイントを処理できます。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-201">OWIN OAuth middleware allows application code to handle the authorization endpoint.</span></span> <span data-ttu-id="2f7ac-202">サンプル アプリでは、MVC コントローラーを使用`OAuthController`して処理します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-202">In our sample app, we use an MVC controller called `OAuthController` to handle it.</span></span> <span data-ttu-id="2f7ac-203">実装例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-203">Here is the sample implementation:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

<span data-ttu-id="2f7ac-204">アクション`Authorize`は、ユーザーが許可サーバーにログインしているかどうかを最初に確認します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-204">The `Authorize` action will first check if the user has logged in to the authorization server.</span></span> <span data-ttu-id="2f7ac-205">認証ミドルウェアが存在しない場合、"Application" Cookie を使用して認証を呼び出し側に要求し、ログイン ページにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-205">If not, the authentication middleware challenges the caller to authenticate using the "Application" cookie and redirects to the login page.</span></span> <span data-ttu-id="2f7ac-206">(上記の強調表示されたコードを参照してください。ユーザーがログインしている場合、次のように[承認]ビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-206">(See highlighted code above.) If user has logged in, it will render the Authorize view, as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image2.png)

<span data-ttu-id="2f7ac-207">**[許可**] ボタンが選択されている`Authorize`場合、アクションは新しい "Bearer" ID を作成し、それを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-207">If the **Grant** button is selected, the `Authorize` action will create a new "Bearer" identity and sign in with it.</span></span> <span data-ttu-id="2f7ac-208">承認サーバーがベアラー トークンを生成し、JSON ペイロードを持つクライアントに返送します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-208">It will trigger the authorization server to generate a bearer token and send it back to the client with JSON payload.</span></span>

### <a name="implicit-grant"></a><span data-ttu-id="2f7ac-209">暗黙的な許可</span><span class="sxs-lookup"><span data-stu-id="2f7ac-209">Implicit Grant</span></span>

<span data-ttu-id="2f7ac-210">IETF の OAuth 2[暗黙的な付与](http://tools.ietf.org/html/rfc6749#section-4.2)のセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-210">Refer to the IETF's OAuth 2 [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) section now.</span></span>

 <span data-ttu-id="2f7ac-211">図 4 に示す[暗黙的な許可](http://tools.ietf.org/html/rfc6749#section-4.2)フローは、OWIN OAuth ミドルウェアが従うフローとマッピングです。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-211">The [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) flow shown in Figure 4 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="2f7ac-212">暗黙的な許可セクションからのフロー ステップ</span><span class="sxs-lookup"><span data-stu-id="2f7ac-212">Flow steps from Implicit Grant section</span></span> | <span data-ttu-id="2f7ac-213">サンプルダウンロードでは、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-213">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="2f7ac-214">(A) クライアントは、リソース所有者のユーザー・エージェントを許可エンドポイントに指示することによって、フローを開始します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-214">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="2f7ac-215">クライアントには、クライアント ID、要求されたスコープ、ローカル状態、およびアクセスが許可 (または拒否) された後に承認サーバーがユーザー エージェントを返信するリダイレクト URI が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-215">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="2f7ac-216">プロバイダー.マッチエンドポイント プロバイダー.検証クライアント リダイレクト Uri プロバイダー.検証承認要求プロバイダー.承認エンドポイント</span><span class="sxs-lookup"><span data-stu-id="2f7ac-216">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="2f7ac-217">(B) 認可サーバは、ユーザ エージェントを介してリソース所有者を認証し、リソース所有者がクライアントのアクセス要求を許可するか拒否するかを確立します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-217">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="2f7ac-218">**ユーザーがアクセス&gt;を許可する場合&lt;** プロバイダー.マッチエンドポイント プロバイダー.検証クライアント リダイレクト Uri プロバイダー.検証承認要求プロバイダー.承認エンドポイント認証コードプロバイダー。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-218">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="2f7ac-219">(C) リソース所有者がアクセス権を付与すると仮定すると、承認サーバーは、(要求またはクライアントの登録中に) 前に提供されたリダイレクト URI を使用して、ユーザーエージェントをクライアントにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-219">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="2f7ac-220">...</span><span class="sxs-lookup"><span data-stu-id="2f7ac-220">...</span></span> |  |
|  |  |
| <span data-ttu-id="2f7ac-221">(D) クライアントは、前の手順で受信した認証コードを含めることによって、承認サーバーのトークン エンドポイントからアクセス トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-221">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="2f7ac-222">要求を行う際、クライアントは承認サーバーで認証します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-222">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="2f7ac-223">クライアントには、検証用の認証コードを取得するために使用されるリダイレクト URI が含まれています。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-223">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> |  |

<span data-ttu-id="2f7ac-224">承認コード付与の承認エンドポイント (`OAuthController.Authorize`アクション) を既に実装しているため、暗黙的なフローも自動的に有効になります。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-224">Since we already implemented the authorization endpoint (`OAuthController.Authorize` action) for authorization code grant, it automatically enables implicit flow as well.</span></span> <span data-ttu-id="2f7ac-225">注:`Provider.ValidateClientRedirectUri`クライアント ID をリダイレクト URL で検証するために使用され、暗黙的な許可フローが悪意のあるクライアントにアクセス トークンを送信するのを防ぐ[(Man-in-the-middle 攻撃](https://www.owasp.org/index.php/Man-in-the-middle_attack))。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-225">Note: `Provider.ValidateClientRedirectUri` is used to validate the client ID with its redirection URL, which protects the implicit grant flow from sending the access token to malicious clients ([Man-in-the-middle attack](https://www.owasp.org/index.php/Man-in-the-middle_attack)).</span></span>

### <a name="resource-owner-password-credentials-grant"></a><span data-ttu-id="2f7ac-226">リソース所有者パスワード資格情報の付与</span><span class="sxs-lookup"><span data-stu-id="2f7ac-226">Resource Owner Password Credentials Grant</span></span>

<span data-ttu-id="2f7ac-227">IETF の OAuth 2[リソース所有者パスワード資格情報の付与セクションを](http://tools.ietf.org/html/rfc6749#section-4.3)参照してください。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-227">Refer to the IETF's OAuth 2 [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) section now.</span></span>

 <span data-ttu-id="2f7ac-228">図 5 に示す[リソース所有者パスワード資格情報付与](http://tools.ietf.org/html/rfc6749#section-4.3)フローは、OWIN OAuth ミドルウェアが従うフローとマッピングです。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-228">The [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) flow shown in Figure 5 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="2f7ac-229">リソース所有者パスワード資格情報の付与セクションからのフローステップ</span><span class="sxs-lookup"><span data-stu-id="2f7ac-229">Flow steps from Resource Owner Password Credentials Grant section</span></span> | <span data-ttu-id="2f7ac-230">サンプルダウンロードでは、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-230">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="2f7ac-231">(A) リソース所有者は、クライアントにユーザー名とパスワードを提供します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-231">(A) The resource owner provides the client with its username and password.</span></span> |  |
|  |  |
| <span data-ttu-id="2f7ac-232">(B) クライアントは、リソース所有者から受信した資格情報を含めることによって、承認サーバーのトークン エンドポイントからアクセス トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-232">(B) The client requests an access token from the authorization server's token endpoint by including the credentials received from the resource owner.</span></span> <span data-ttu-id="2f7ac-233">要求を行う際、クライアントは承認サーバーで認証します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-233">When making the request, the client authenticates with the authorization server.</span></span> | <span data-ttu-id="2f7ac-234">プロバイダー.マッチエンドポイントプロバイダー.検証クライアント認証プロバイダー.検証トークン要求プロバイダー.グラントリソースオーナー資格プロバイダー.トークンエンドポイントアクセストークンプロバイダ.CreateAsyncリフレッシュトークンプロバイダ。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-234">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="2f7ac-235">(C) 承認サーバーは、クライアントを認証し、リソース所有者の資格情報を検証し、有効であればアクセス トークンを発行します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-235">(C) The authorization server authenticates the client and validates the resource owner credentials, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="2f7ac-236">の実装例を次に`Provider.GrantResourceOwnerCredentials`示します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-236">Here is the sample implementation for `Provider.GrantResourceOwnerCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> <span data-ttu-id="2f7ac-237">上記のコードは、チュートリアルのこのセクションを説明することを目的としており、安全なアプリや運用アプリでは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-237">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="2f7ac-238">リソース所有者の資格情報はチェックされません。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-238">It does not check the resource owners credentials.</span></span> <span data-ttu-id="2f7ac-239">すべての資格情報が有効であると想定し、新しい ID を作成します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-239">It assumes every credential is valid and creates a new identity for it.</span></span> <span data-ttu-id="2f7ac-240">新しい ID は、アクセス トークンと更新トークンの生成に使用されます。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-240">The new identity will be used to generate the access token and refresh token.</span></span> <span data-ttu-id="2f7ac-241">コードを、セキュリティで保護されたアカウント管理コードに置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-241">Please replace the code with your own secure account management code.</span></span>


### <a name="client-credentials-grant"></a><span data-ttu-id="2f7ac-242">クライアント資格情報の付与</span><span class="sxs-lookup"><span data-stu-id="2f7ac-242">Client Credentials Grant</span></span>

<span data-ttu-id="2f7ac-243">IETF の OAuth 2[クライアント資格情報の付与](http://tools.ietf.org/html/rfc6749#section-4.4)のセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-243">Refer to the IETF's OAuth 2 [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) section now.</span></span>

 <span data-ttu-id="2f7ac-244">図 6 に示す[クライアント資格情報の付与](http://tools.ietf.org/html/rfc6749#section-4.4)フローは、OWIN OAuth ミドルウェアが従うフローとマッピングです。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-244">The [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) flow shown in Figure 6 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="2f7ac-245">[クライアント資格情報の付与] セクションからのフロー ステップ</span><span class="sxs-lookup"><span data-stu-id="2f7ac-245">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="2f7ac-246">サンプルダウンロードでは、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-246">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="2f7ac-247">(A) クライアントは承認サーバーで認証を行い、トークン エンドポイントからアクセス トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-247">(A) The client authenticates with the authorization server and requests an access token from the token endpoint.</span></span> | <span data-ttu-id="2f7ac-248">プロバイダー.マッチエンドポイントプロバイダー.検証クライアント認証プロバイダー.検証トークン要求プロバイダー.トークンエンドポイントアクセストークンプロバイダー.CreateAsyncリフレッシュトークンプロバイダー</span><span class="sxs-lookup"><span data-stu-id="2f7ac-248">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="2f7ac-249">(B) 承認サーバーはクライアントを認証し、有効であればアクセス トークンを発行します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-249">(B) The authorization server authenticates the client, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="2f7ac-250">の実装例を次に`Provider.GrantClientCredentials`示します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-250">Here is the sample implementation for `Provider.GrantClientCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="2f7ac-251">上記のコードは、チュートリアルのこのセクションを説明することを目的としており、安全なアプリや運用アプリでは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-251">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="2f7ac-252">コードを独自のセキュリティで保護されたクライアント管理コードに置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-252">Please replace the code with your own secure client management code.</span></span>


### <a name="refresh-token"></a><span data-ttu-id="2f7ac-253">トークンの更新</span><span class="sxs-lookup"><span data-stu-id="2f7ac-253">Refresh Token</span></span>

<span data-ttu-id="2f7ac-254">IETF の OAuth 2[更新トークン](http://tools.ietf.org/html/rfc6749#section-1.5)のセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-254">Refer to the IETF's OAuth 2 [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) section now.</span></span>

 <span data-ttu-id="2f7ac-255">図 2 に示す[更新トークン](http://tools.ietf.org/html/rfc6749#section-1.5)フローは、OWIN OAuth ミドルウェアが従うフローとマッピングです。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-255">The [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) flow shown in Figure 2 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="2f7ac-256">[クライアント資格情報の付与] セクションからのフロー ステップ</span><span class="sxs-lookup"><span data-stu-id="2f7ac-256">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="2f7ac-257">サンプルダウンロードでは、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-257">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="2f7ac-258">(G) クライアントは、承認サーバーで認証し、更新トークンを提示することによって、新しいアクセス トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-258">(G) The client requests a new access token by authenticating with the authorization server and presenting the refresh token.</span></span> <span data-ttu-id="2f7ac-259">クライアント認証の要件は、クライアント・タイプと許可サーバー・ポリシーに基づいています。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-259">The client authentication requirements are based on the client type and on the authorization server policies.</span></span> | <span data-ttu-id="2f7ac-260">プロバイダー.マッチエンドポイントプロバイダー.検証クライアント認証リフレッシュトークンプロバイダー.受信非同期プロバイダー.検証トークン要求プロバイダー.トークンエンドポイントアクセストークンプロバイダー.CreateAsyncリフレッシュトークンプロバイダー.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="2f7ac-260">Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="2f7ac-261">(H) 承認サーバーは、クライアントを認証し、更新トークンを検証し、有効な場合は、新しいアクセス トークン (およびオプションで新しい更新トークン) を発行します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-261">(H) The authorization server authenticates the client and validates the refresh token, and if valid, issues a new access token (and, optionally, a new refresh token).</span></span> |  |

<span data-ttu-id="2f7ac-262">の実装例を次に`Provider.GrantRefreshToken`示します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-262">Here is the sample implementation for `Provider.GrantRefreshToken`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a><span data-ttu-id="2f7ac-263">アクセス トークンによって保護されるリソース サーバーを作成する</span><span class="sxs-lookup"><span data-stu-id="2f7ac-263">Create a Resource Server which is protected by Access Token</span></span>

<span data-ttu-id="2f7ac-264">空の Web アプリ プロジェクトを作成し、プロジェクトに次のパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-264">Create an empty web app project and install following packages in the project:</span></span>

- <span data-ttu-id="2f7ac-265">マイクロソフト.AspNet.ウェブApi.オビン</span><span class="sxs-lookup"><span data-stu-id="2f7ac-265">Microsoft.AspNet.WebApi.Owin</span></span>
- <span data-ttu-id="2f7ac-266">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="2f7ac-266">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="2f7ac-267">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="2f7ac-267">Microsoft.Owin.Security.OAuth</span></span>

<span data-ttu-id="2f7ac-268">スタートアップ クラスを作成し、認証と Web API を構成します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-268">Create a startup class and configure authentication and Web API.</span></span> <span data-ttu-id="2f7ac-269">サンプル ダウンロードの*承認サーバー\リソース サーバー\スタートアップ.cs*を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-269">See *AuthorizationServer\ResourceServer\Startup.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

<span data-ttu-id="2f7ac-270">サンプル ダウンロードの *「承認サーバー\\_リソース サーバー\アプリの開始\スタートアップ.Auth.cs」* を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-270">See *AuthorizationServer\ResourceServer\App\_Start\Startup.Auth.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

<span data-ttu-id="2f7ac-271">サンプル ダウンロードの *「承認サーバー\\_リソース サーバー\アプリの開始\スタートアップ.WebApi.cs」* を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-271">See *AuthorizationServer\ResourceServer\App\_Start\Startup.WebApi.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- <span data-ttu-id="2f7ac-272">`UseCors`メソッドは、すべてのドメインに CORS を許可します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-272">`UseCors` method allows CORS for all domains.</span></span>
- <span data-ttu-id="2f7ac-273">`UseOAuthBearerAuthentication`メソッドは、要求内の承認ヘッダーからベアラー トークンを受信および検証する OAuth ベアラー トークン認証ミドルウェアを有効にします。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-273">`UseOAuthBearerAuthentication` method enables OAuth bearer token authentication middleware which will receive and validate bearer token from authorization header in the request.</span></span>
- <span data-ttu-id="2f7ac-274">`Config.SuppressDefaultHostAuthenticaiton`は、アプリから既定のホスト認証プリンシパルを抑制するため、この呼び出し後にすべての要求は匿名になります。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-274">`Config.SuppressDefaultHostAuthenticaiton` suppresses default host authenticated principal from the app, therefore all requests will be anonymous after this call.</span></span>
- <span data-ttu-id="2f7ac-275">`HostAuthenticationFilter`指定された認証タイプに対して認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-275">`HostAuthenticationFilter` enables authentication just for the specified authentication type.</span></span> <span data-ttu-id="2f7ac-276">この場合、ベアラー認証タイプです。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-276">In this case, it's bearer authentication type.</span></span>

<span data-ttu-id="2f7ac-277">認証された ID を示すために、現在のユーザーの要求を出力する ApiController を作成します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-277">In order to demonstrate the authenticated identity, we create an ApiController to output current user's claims.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

<span data-ttu-id="2f7ac-278">許可サーバーとリソース・サーバーが同じコンピューター上にない場合、OAuth ミドルウェアは異なるマシン・キーを使用してベアラー・アクセス・トークンを暗号化および復号します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-278">If the authorization server and the resource server are not on the same computer, the OAuth middleware will use the different machine keys to encrypt and decrypt bearer access token.</span></span> <span data-ttu-id="2f7ac-279">両方のプロジェクト間で同じ秘密キーを共有するために、両方の`machinekey`*web.config*ファイルに同じ設定を追加します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-279">In order to share the same private key between both projects, we add the same `machinekey` setting in both *web.config* files.</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a><span data-ttu-id="2f7ac-280">OAuth 2.0 クライアントの作成</span><span class="sxs-lookup"><span data-stu-id="2f7ac-280">Create OAuth 2.0 Clients</span></span>

 <span data-ttu-id="2f7ac-281">クライアント コードを簡略化するために[、DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet パッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-281">We use the [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet package to simplify the client code.</span></span>

### <a name="authorization-code-grant-client"></a><span data-ttu-id="2f7ac-282">承認コード交付クライアント</span><span class="sxs-lookup"><span data-stu-id="2f7ac-282">Authorization Code Grant Client</span></span>

 <span data-ttu-id="2f7ac-283">このクライアントは、MVC アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-283">This client is an MVC application.</span></span> <span data-ttu-id="2f7ac-284">バックエンドからアクセス トークンを取得する承認コード許可フローをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-284">It will trigger an authorization code grant flow to get the access token from backend.</span></span> <span data-ttu-id="2f7ac-285">以下に示すように、1 つのページがあります。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-285">It has a single page as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image3.png)

- <span data-ttu-id="2f7ac-286">**[Authorize]** ボタンをクリックすると、ブラウザが承認サーバーにリダイレクトされ、リソース所有者にこのクライアントへのアクセス権を付与するよう通知されます。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-286">The **Authorize** button will redirect browser to the authorization server to notify the resource owner to grant access to this client.</span></span>
- <span data-ttu-id="2f7ac-287">**[更新]** ボタンは、現在の更新トークンを使用して新しいアクセス トークンと更新トークンを取得します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-287">The **Refresh** button will get a new access token and refresh token using the current refresh token.</span></span>
- <span data-ttu-id="2f7ac-288">[**保護されたリソース API へのアクセス**] ボタンは、リソース サーバーを呼び出して、現在のユーザーの要求データを取得し、ページに表示します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-288">The **Access Protected Resource API** button will call the resource server to get current user's claims data and show them on the page.</span></span>

<span data-ttu-id="2f7ac-289">クライアントのサンプル コードを`HomeController`次に示します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-289">Here is the sample code of the `HomeController` of the client.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

<span data-ttu-id="2f7ac-290">`DotNetOpenAuth`にはデフォルトで SSL が必要です。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-290">`DotNetOpenAuth` requires SSL by default.</span></span> <span data-ttu-id="2f7ac-291">デモでは HTTP を使用しているため、構成ファイルに次の設定を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-291">Since our demo is using HTTP, you need to add following setting in the config file:</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> <span data-ttu-id="2f7ac-292">セキュリティ - 運用アプリで SSL を無効にしないでください。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-292">Security - Never disable SSL in a production app.</span></span> <span data-ttu-id="2f7ac-293">これで、ログイン資格情報がクリア テキストで送信されます。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-293">Your login credentials are now being sent in clear-text across the wire.</span></span> <span data-ttu-id="2f7ac-294">上記のコードは、ローカルのサンプルデバッグと探索用です。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-294">The code above is just for local sample debugging and exploration.</span></span>


### <a name="implicit-grant-client"></a><span data-ttu-id="2f7ac-295">暗黙的な許可クライアント</span><span class="sxs-lookup"><span data-stu-id="2f7ac-295">Implicit Grant Client</span></span>

<span data-ttu-id="2f7ac-296">このクライアントは、次の場合に JavaScript を使用しています。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-296">This client is using JavaScript to:</span></span>

1. <span data-ttu-id="2f7ac-297">新しいウィンドウを開き、承認サーバーの承認エンドポイントにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-297">Open a new window and redirect to the authorize endpoint of the Authorization Server.</span></span>
2. <span data-ttu-id="2f7ac-298">リダイレクトバック時に URL フラグメントからアクセス トークンを取得します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-298">Get the access token from URL fragments when it redirects back.</span></span>

<span data-ttu-id="2f7ac-299">次の図は、このプロセスを示しています。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-299">The following image shows this process:</span></span>

![](owin-oauth-20-authorization-server/_static/image4.png)

<span data-ttu-id="2f7ac-300">クライアントには、ホーム ページ用とコールバック用のページの 2 つのページが必要です。*Index.cshtml*ファイルに含まれるサンプル JavaScript コードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-300">The client should have two pages: one for home page and the other for callback.Here is the sample JavaScript code found in the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

<span data-ttu-id="2f7ac-301">*SignIn.cshtml*ファイルのコールバック処理コードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-301">Here is the callback handling code in *SignIn.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> <span data-ttu-id="2f7ac-302">ベスト プラクティスは、JavaScript を外部ファイルに移動し、Razor マークアップを埋め込まない方法です。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-302">A best practice is to move the JavaScript to an external file and not embed it with the Razor markup.</span></span> <span data-ttu-id="2f7ac-303">このサンプルをシンプルにするために、これらを組み合わせて使用しています。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-303">To keep this sample simple, they have been combined.</span></span>


### <a name="resource-owner-password-credentials-grant-client"></a><span data-ttu-id="2f7ac-304">リソース所有者パスワード資格情報付与クライアント</span><span class="sxs-lookup"><span data-stu-id="2f7ac-304">Resource Owner Password Credentials Grant Client</span></span>

<span data-ttu-id="2f7ac-305">コンソール アプリを使用して、このクライアントをデモします。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-305">We uses a console app to demo this client.</span></span> <span data-ttu-id="2f7ac-306">次にコードを示します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-306">Here is the code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a><span data-ttu-id="2f7ac-307">クライアント資格情報付与クライアント</span><span class="sxs-lookup"><span data-stu-id="2f7ac-307">Client Credentials Grant Client</span></span>

<span data-ttu-id="2f7ac-308">リソース所有者パスワード資格情報付与と同様に、コンソール アプリ コードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="2f7ac-308">Similar to the Resource Owner Password Credentials Grant, here is console app code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
