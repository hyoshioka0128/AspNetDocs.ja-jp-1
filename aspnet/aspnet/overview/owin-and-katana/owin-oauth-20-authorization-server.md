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
<a name="owin-oauth-20-authorization-server"></a>OWIN OAuth 2.0 承認サーバー
====================
[ホンジェ・サン](https://github.com/hongyes)と[プラブラージ・チアガラジャン](https://github.com/Praburaj)

> このチュートリアルでは、OWIN OAuth ミドルウェアを使用して OAuth 2.0 承認サーバーを実装する方法について説明します。 これは、OWIN OAuth 2.0 承認サーバーを作成する手順の概要のみを説明する高度なチュートリアルです。 これは、ステップバイステップチュートリアルではありません。 [サンプル コードをダウンロード](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)します。
>
> > [!NOTE]
> > この概要は、安全な運用アプリの作成に使用することを目的としていません。 このチュートリアルでは、OWIN OAuth ミドルウェアを使用して OAuth 2.0 承認サーバーを実装する方法の概要のみを提供します。
>
>
> ## <a name="software-versions"></a>ソフトウェアバージョン
>
> | **チュートリアルで示されている** | **また、で動作します** |
> | --- | --- |
> | Windows 8.1 | ウィンドウズ 8, ウィンドウズ 7 |
> | [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) | [デスクトップ用のビジュアル スタジオ 2013 エクスプレス](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express). Visual Studio 2012 の最新の更新プログラムは動作するはずですが、チュートリアルではテストされておらず、一部のメニューの選択とダイアログ ボックスが異なります。 |
> | .NET 4.5 |  |
>
> ## <a name="questions-and-comments"></a>質問とコメント
>
> チュートリアルに直接関連しない質問がある場合は[、GitHub の Katana プロジェクトで](https://github.com/aspnet/AspNetKatana/)投稿できます。 チュートリアル自体に関する質問やコメントについては、ページの下部にあるコメントセクションを参照してください。


[OAuth 2.0 フレームワーク](http://tools.ietf.org/html/rfc6749)を使用すると、サードパーティ製のアプリが HTTP サービスへのアクセスを制限できます。 保護されたリソースにアクセスするためにリソース所有者の資格情報を使用する代わりに、クライアントはアクセス トークン (特定のスコープ、有効期間、およびその他のアクセス属性を示す文字列) を取得します。 アクセス トークンは、リソース所有者の承認を得て、承認サーバーによってサードパーティのクライアントに発行されます。

このチュートリアルでは、以下について説明します。

- 承認サーバーを作成して、4 つの承認許可タイプと更新トークンをサポートする方法:
    - 認証コードの付与
    - 暗黙的な許可
    - リソース所有者パスワード資格情報の付与
    - クライアント資格情報の付与
- アクセス トークンによって保護されるリソース サーバーを作成する。
- OAuth 2.0 クライアントを作成しています。

<a id="prerequisites"></a>
## <a name="prerequisites"></a>必須コンポーネント

- ページ上部の**ソフトウェア バージョン**に示されているように[、Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions)または無料の[Visual Studio Express 2013。](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)
- OWIN に精通しています。 [「カタナ プロジェクトの概要](https://msdn.microsoft.com/magazine/dn451439.aspx)」および[「OWIN とカタナの新機能](index.md)」を参照してください。
- [ロール](http://tools.ietf.org/html/rfc6749#section-1.1)、[プロトコル フロー](http://tools.ietf.org/html/rfc6749#section-1.2)、[承認許可](http://tools.ietf.org/html/rfc6749#section-1.3)などの[OAuth](http://tools.ietf.org/html/rfc6749)用語に精通しています。 [OAuth 2.0 の導入は](http://tools.ietf.org/html/rfc6749#section-1)、良い紹介を提供します。

## <a name="create-an-authorization-server"></a>承認サーバーの作成

このチュートリアルでは、承認サーバーを作成する[OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx)と ASP.NET MVC を使用する方法について説明します。 このチュートリアルでは各ステップが含まれていないため、完成したサンプルのダウンロードをすぐに提供したいと考えています。 まず、*認証サーバー*という名前の空の Web アプリケーションを作成し、次のパッケージをインストールします。

- マイクロソフト.AspNet.Mvc
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth
- Microsoft.Owin.Security.Cookies
- マイクロソフト.Owin.Security.グーグル(またはマイクロソフト.Owin.Security.Facebookなどの他のソーシャルログインパッケージ)

スタートアップ という名前のプロジェクト ルート フォルダの下に[、OWIN](owin-startup-class-detection.md) *スタートアップ*クラスを追加します。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

*\_アプリケーションのスタート*フォルダーを作成します。 *[アプリケーションの\_開始]* フォルダーを選択し、Shift + Alt + A を使用して、ダウンロードしたバージョンの*AuthorizationServer\\_アプリケーション開始\スタートアップ.Auth.cs*ファイルを追加します。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

上記のコードは、許可サーバー自体がアカウントを管理するために使用する、アプリケーション/外部サインインクッキーとGoogle認証を有効にします。

拡張`UseOAuthAuthorizationServer`方法は、承認サーバーをセットアップすることです。 セットアップ オプションは次のとおりです。

- `AuthorizeEndpointPath`: ユーザーがトークンまたはコードを発行することに同意するために、クライアント アプリケーションがユーザー エージェントをリダイレクトする要求パス。 先頭のスラッシュ (""`/Authorize`など) で始める必要があります。
- `TokenEndpointPath`: クライアント アプリケーションが直接通信してアクセス トークンを取得する要求パス。 先頭のスラッシュ ("/Token" など) で始める必要があります。 クライアントが[クライアント\_シークレット](http://tools.ietf.org/html/rfc6749#appendix-A.2)を発行される場合は、このエンドポイントにクライアントシークレットを提供する必要があります。
- `ApplicationCanDisplayErrors`: Web`true`アプリケーションがエンドポイントでクライアント検証エラーのカスタム エラー ページを生成する`/Authorize`場合にに設定します。 これは、ブラウザがクライアント アプリケーションにリダイレクトされない場合(たとえば、 または`client_id``redirect_uri`が正しくない場合など)にのみ必要です。 エンドポイント`/Authorize`は"oauth"を見ることを期待するはずです。エラー」、"oauth。エラー説明」と「oauth。"ErrorUri" プロパティが OWIN 環境に追加されます。

    > [!NOTE]
    > true でない場合、承認サーバーはエラーの詳細を示す既定のエラー ページを返します。
- `AllowInsecureHttp`: 承認要求とトークン要求を HTTP URI アドレスに到着させ、受信`redirect_uri`承認要求パラメーターに HTTP URI アドレスを持たできるようにする場合は True。

    > [!WARNING]
    > セキュリティ - これは開発専用です。
- `Provider`: 承認サーバーミドルウェアによって発生したイベントを処理するためにアプリケーションによって提供されるオブジェクト。 アプリケーションは、インターフェイスを完全に実装するか、またはインスタンスを作成`OAuthAuthorizationServerProvider`し、このサーバーがサポートする OAuth フローに必要なデリゲートを割り当てる場合があります。
- `AuthorizationCodeProvider`: クライアント アプリケーションに戻るための、単独使用の認証コードを生成します。 OAuth サーバーをセキュリティで保護するには、`OnCreate/OnCreateAsync`イベントによって生成されたトークン`AuthorizationCodeProvider`が 1 回の呼び出しに対してのみ有効と`OnReceive/OnReceiveAsync`見なされるインスタンスをアプリケーションに提供**する必要があります**。
- `RefreshTokenProvider`: 必要に応じて新しいアクセス トークンを生成するために使用できる更新トークンを生成します。 指定しない場合、承認サーバーはエンドポイントから更新トークンを`/Token`返しません。

## <a name="account-management"></a>アカウント管理

OAuth は、ユーザー アカウント情報をどこでどのように管理するかは気にしません。 それはそれを担当する[ASP.NETアイデンティティ](../../../identity/index.md)です。 このチュートリアルでは、アカウント管理コードを簡素化し、ユーザーが OWIN クッキーミドルウェアを使用してログインできることを確認します。 以下は、 のサンプル コードの`AccountController`簡略化です。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

`ValidateClientRedirectUri`は、登録されたリダイレクト URL を使用してクライアントを検証するために使用されます。 `ValidateClientAuthentication`は、基本スキームヘッダーとフォーム本体をチェックして、クライアントの資格情報を取得します。

ログインページは以下の通りです:

![](owin-oauth-20-authorization-server/_static/image1.png)

IETF の OAuth 2[認証コードの付与](http://tools.ietf.org/html/rfc6749#section-4.1)セクションを今すぐ確認します。

**プロバイダ**(下の表) は[OAuth 認証サーバー オプションです](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx)。プロバイダー ( 型`OAuthAuthorizationServerProvider`) には、すべての OAuth サーバー イベントが含まれます。

| [承認コードの付与] セクションからのフロー ステップ | サンプルダウンロードでは、次の手順を実行します。 |
| --- | --- |
|  |  |
| (A) クライアントは、リソース所有者のユーザー・エージェントを許可エンドポイントに指示することによって、フローを開始します。 クライアントには、クライアント ID、要求されたスコープ、ローカル状態、およびアクセスが許可 (または拒否) された後に承認サーバーがユーザー エージェントを返信するリダイレクト URI が含まれます。 | プロバイダー.マッチエンドポイント プロバイダー.検証クライアント リダイレクト Uri プロバイダー.検証承認要求プロバイダー.承認エンドポイント |
|  |  |
| (B) 認可サーバは、ユーザ エージェントを介してリソース所有者を認証し、リソース所有者がクライアントのアクセス要求を許可するか拒否するかを確立します。 | **ユーザーがアクセス&gt;を許可する場合&lt;** プロバイダー.マッチエンドポイント プロバイダー.検証クライアント リダイレクト Uri プロバイダー.検証承認要求プロバイダー.承認エンドポイント認証コードプロバイダー。 |
|  |  |
| (C) リソース所有者がアクセス権を付与すると仮定すると、承認サーバーは、(要求またはクライアントの登録中に) 前に提供されたリダイレクト URI を使用して、ユーザーエージェントをクライアントにリダイレクトします。 ... |  |
|  |  |
| (D) クライアントは、前の手順で受信した認証コードを含めることによって、承認サーバーのトークン エンドポイントからアクセス トークンを要求します。 要求を行う際、クライアントは承認サーバーで認証します。 クライアントには、検証用の認証コードを取得するために使用されるリダイレクト URI が含まれています。 | プロバイダー.マッチエンドポイントプロバイダー.検証クライアント認証認証コードプロバイダー.受信非同期プロバイダー.検証トークン要求プロバイダー.承認コードプロバイダー.トークンエンドポイントアクセストークンプロバイダー.CreateAsyncリフレッシュトークンプロバイダ. |

認証コードの作成`AuthorizationCodeProvider.CreateAsync`と`ReceiveAsync`検証を制御するためのサンプル実装を以下に示します。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

上記のコードでは、メモリ内の同時実行辞書を使用してコードと ID チケットを格納し、コードを受信した後に ID を復元します。 実際のアプリケーションでは、永続データ ストアに置き換えられます。 承認エンドポイントは、リソース所有者がクライアントにアクセス権を付与するためのエンドポイントです。 通常、ユーザーがボタンをクリックして許可を確認できるようにするには、ユーザー インターフェイスが必要です。 OWIN OAuth ミドルウェアを使用すると、アプリケーション コードで承認エンドポイントを処理できます。 サンプル アプリでは、MVC コントローラーを使用`OAuthController`して処理します。 実装例を次に示します。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

アクション`Authorize`は、ユーザーが許可サーバーにログインしているかどうかを最初に確認します。 認証ミドルウェアが存在しない場合、"Application" Cookie を使用して認証を呼び出し側に要求し、ログイン ページにリダイレクトします。 (上記の強調表示されたコードを参照してください。ユーザーがログインしている場合、次のように[承認]ビューが表示されます。

![](owin-oauth-20-authorization-server/_static/image2.png)

**[許可**] ボタンが選択されている`Authorize`場合、アクションは新しい "Bearer" ID を作成し、それを使用してサインインします。 承認サーバーがベアラー トークンを生成し、JSON ペイロードを持つクライアントに返送します。

### <a name="implicit-grant"></a>暗黙的な許可

IETF の OAuth 2[暗黙的な付与](http://tools.ietf.org/html/rfc6749#section-4.2)のセクションを参照してください。

 図 4 に示す[暗黙的な許可](http://tools.ietf.org/html/rfc6749#section-4.2)フローは、OWIN OAuth ミドルウェアが従うフローとマッピングです。

| 暗黙的な許可セクションからのフロー ステップ | サンプルダウンロードでは、次の手順を実行します。 |
| --- | --- |
|  |  |
| (A) クライアントは、リソース所有者のユーザー・エージェントを許可エンドポイントに指示することによって、フローを開始します。 クライアントには、クライアント ID、要求されたスコープ、ローカル状態、およびアクセスが許可 (または拒否) された後に承認サーバーがユーザー エージェントを返信するリダイレクト URI が含まれます。 | プロバイダー.マッチエンドポイント プロバイダー.検証クライアント リダイレクト Uri プロバイダー.検証承認要求プロバイダー.承認エンドポイント |
|  |  |
| (B) 認可サーバは、ユーザ エージェントを介してリソース所有者を認証し、リソース所有者がクライアントのアクセス要求を許可するか拒否するかを確立します。 | **ユーザーがアクセス&gt;を許可する場合&lt;** プロバイダー.マッチエンドポイント プロバイダー.検証クライアント リダイレクト Uri プロバイダー.検証承認要求プロバイダー.承認エンドポイント認証コードプロバイダー。 |
|  |  |
| (C) リソース所有者がアクセス権を付与すると仮定すると、承認サーバーは、(要求またはクライアントの登録中に) 前に提供されたリダイレクト URI を使用して、ユーザーエージェントをクライアントにリダイレクトします。 ... |  |
|  |  |
| (D) クライアントは、前の手順で受信した認証コードを含めることによって、承認サーバーのトークン エンドポイントからアクセス トークンを要求します。 要求を行う際、クライアントは承認サーバーで認証します。 クライアントには、検証用の認証コードを取得するために使用されるリダイレクト URI が含まれています。 |  |

承認コード付与の承認エンドポイント (`OAuthController.Authorize`アクション) を既に実装しているため、暗黙的なフローも自動的に有効になります。 注:`Provider.ValidateClientRedirectUri`クライアント ID をリダイレクト URL で検証するために使用され、暗黙的な許可フローが悪意のあるクライアントにアクセス トークンを送信するのを防ぐ[(Man-in-the-middle 攻撃](https://www.owasp.org/index.php/Man-in-the-middle_attack))。

### <a name="resource-owner-password-credentials-grant"></a>リソース所有者パスワード資格情報の付与

IETF の OAuth 2[リソース所有者パスワード資格情報の付与セクションを](http://tools.ietf.org/html/rfc6749#section-4.3)参照してください。

 図 5 に示す[リソース所有者パスワード資格情報付与](http://tools.ietf.org/html/rfc6749#section-4.3)フローは、OWIN OAuth ミドルウェアが従うフローとマッピングです。

| リソース所有者パスワード資格情報の付与セクションからのフローステップ | サンプルダウンロードでは、次の手順を実行します。 |
| --- | --- |
|  |  |
| (A) リソース所有者は、クライアントにユーザー名とパスワードを提供します。 |  |
|  |  |
| (B) クライアントは、リソース所有者から受信した資格情報を含めることによって、承認サーバーのトークン エンドポイントからアクセス トークンを要求します。 要求を行う際、クライアントは承認サーバーで認証します。 | プロバイダー.マッチエンドポイントプロバイダー.検証クライアント認証プロバイダー.検証トークン要求プロバイダー.グラントリソースオーナー資格プロバイダー.トークンエンドポイントアクセストークンプロバイダ.CreateAsyncリフレッシュトークンプロバイダ。 |
|  |  |
| (C) 承認サーバーは、クライアントを認証し、リソース所有者の資格情報を検証し、有効であればアクセス トークンを発行します。 |  |

の実装例を次に`Provider.GrantResourceOwnerCredentials`示します。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> 上記のコードは、チュートリアルのこのセクションを説明することを目的としており、安全なアプリや運用アプリでは使用しないでください。 リソース所有者の資格情報はチェックされません。 すべての資格情報が有効であると想定し、新しい ID を作成します。 新しい ID は、アクセス トークンと更新トークンの生成に使用されます。 コードを、セキュリティで保護されたアカウント管理コードに置き換えてください。


### <a name="client-credentials-grant"></a>クライアント資格情報の付与

IETF の OAuth 2[クライアント資格情報の付与](http://tools.ietf.org/html/rfc6749#section-4.4)のセクションを参照してください。

 図 6 に示す[クライアント資格情報の付与](http://tools.ietf.org/html/rfc6749#section-4.4)フローは、OWIN OAuth ミドルウェアが従うフローとマッピングです。

| [クライアント資格情報の付与] セクションからのフロー ステップ | サンプルダウンロードでは、次の手順を実行します。 |
| --- | --- |
|  |  |
| (A) クライアントは承認サーバーで認証を行い、トークン エンドポイントからアクセス トークンを要求します。 | プロバイダー.マッチエンドポイントプロバイダー.検証クライアント認証プロバイダー.検証トークン要求プロバイダー.トークンエンドポイントアクセストークンプロバイダー.CreateAsyncリフレッシュトークンプロバイダー |
|  |  |
| (B) 承認サーバーはクライアントを認証し、有効であればアクセス トークンを発行します。 |  |

の実装例を次に`Provider.GrantClientCredentials`示します。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> 上記のコードは、チュートリアルのこのセクションを説明することを目的としており、安全なアプリや運用アプリでは使用しないでください。 コードを独自のセキュリティで保護されたクライアント管理コードに置き換えてください。


### <a name="refresh-token"></a>トークンの更新

IETF の OAuth 2[更新トークン](http://tools.ietf.org/html/rfc6749#section-1.5)のセクションを参照してください。

 図 2 に示す[更新トークン](http://tools.ietf.org/html/rfc6749#section-1.5)フローは、OWIN OAuth ミドルウェアが従うフローとマッピングです。

| [クライアント資格情報の付与] セクションからのフロー ステップ | サンプルダウンロードでは、次の手順を実行します。 |
| --- | --- |
|  |  |
| (G) クライアントは、承認サーバーで認証し、更新トークンを提示することによって、新しいアクセス トークンを要求します。 クライアント認証の要件は、クライアント・タイプと許可サーバー・ポリシーに基づいています。 | プロバイダー.マッチエンドポイントプロバイダー.検証クライアント認証リフレッシュトークンプロバイダー.受信非同期プロバイダー.検証トークン要求プロバイダー.トークンエンドポイントアクセストークンプロバイダー.CreateAsyncリフレッシュトークンプロバイダー.CreateAsync |
|  |  |
| (H) 承認サーバーは、クライアントを認証し、更新トークンを検証し、有効な場合は、新しいアクセス トークン (およびオプションで新しい更新トークン) を発行します。 |  |

の実装例を次に`Provider.GrantRefreshToken`示します。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a>アクセス トークンによって保護されるリソース サーバーを作成する

空の Web アプリ プロジェクトを作成し、プロジェクトに次のパッケージをインストールします。

- マイクロソフト.AspNet.ウェブApi.オビン
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth

スタートアップ クラスを作成し、認証と Web API を構成します。 サンプル ダウンロードの*承認サーバー\リソース サーバー\スタートアップ.cs*を参照してください。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

サンプル ダウンロードの *「承認サーバー\\_リソース サーバー\アプリの開始\スタートアップ.Auth.cs」* を参照してください。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

サンプル ダウンロードの *「承認サーバー\\_リソース サーバー\アプリの開始\スタートアップ.WebApi.cs」* を参照してください。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- `UseCors`メソッドは、すべてのドメインに CORS を許可します。
- `UseOAuthBearerAuthentication`メソッドは、要求内の承認ヘッダーからベアラー トークンを受信および検証する OAuth ベアラー トークン認証ミドルウェアを有効にします。
- `Config.SuppressDefaultHostAuthenticaiton`は、アプリから既定のホスト認証プリンシパルを抑制するため、この呼び出し後にすべての要求は匿名になります。
- `HostAuthenticationFilter`指定された認証タイプに対して認証を有効にします。 この場合、ベアラー認証タイプです。

認証された ID を示すために、現在のユーザーの要求を出力する ApiController を作成します。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

許可サーバーとリソース・サーバーが同じコンピューター上にない場合、OAuth ミドルウェアは異なるマシン・キーを使用してベアラー・アクセス・トークンを暗号化および復号します。 両方のプロジェクト間で同じ秘密キーを共有するために、両方の`machinekey`*web.config*ファイルに同じ設定を追加します。

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a>OAuth 2.0 クライアントの作成

 クライアント コードを簡略化するために[、DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet パッケージを使用します。

### <a name="authorization-code-grant-client"></a>承認コード交付クライアント

 このクライアントは、MVC アプリケーションです。 バックエンドからアクセス トークンを取得する承認コード許可フローをトリガーします。 以下に示すように、1 つのページがあります。

![](owin-oauth-20-authorization-server/_static/image3.png)

- **[Authorize]** ボタンをクリックすると、ブラウザが承認サーバーにリダイレクトされ、リソース所有者にこのクライアントへのアクセス権を付与するよう通知されます。
- **[更新]** ボタンは、現在の更新トークンを使用して新しいアクセス トークンと更新トークンを取得します。
- [**保護されたリソース API へのアクセス**] ボタンは、リソース サーバーを呼び出して、現在のユーザーの要求データを取得し、ページに表示します。

クライアントのサンプル コードを`HomeController`次に示します。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

`DotNetOpenAuth`にはデフォルトで SSL が必要です。 デモでは HTTP を使用しているため、構成ファイルに次の設定を追加する必要があります。

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> セキュリティ - 運用アプリで SSL を無効にしないでください。 これで、ログイン資格情報がクリア テキストで送信されます。 上記のコードは、ローカルのサンプルデバッグと探索用です。


### <a name="implicit-grant-client"></a>暗黙的な許可クライアント

このクライアントは、次の場合に JavaScript を使用しています。

1. 新しいウィンドウを開き、承認サーバーの承認エンドポイントにリダイレクトします。
2. リダイレクトバック時に URL フラグメントからアクセス トークンを取得します。

次の図は、このプロセスを示しています。

![](owin-oauth-20-authorization-server/_static/image4.png)

クライアントには、ホーム ページ用とコールバック用のページの 2 つのページが必要です。*Index.cshtml*ファイルに含まれるサンプル JavaScript コードを次に示します。

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

*SignIn.cshtml*ファイルのコールバック処理コードを次に示します。

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> ベスト プラクティスは、JavaScript を外部ファイルに移動し、Razor マークアップを埋め込まない方法です。 このサンプルをシンプルにするために、これらを組み合わせて使用しています。


### <a name="resource-owner-password-credentials-grant-client"></a>リソース所有者パスワード資格情報付与クライアント

コンソール アプリを使用して、このクライアントをデモします。 次にコードを示します。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a>クライアント資格情報付与クライアント

リソース所有者パスワード資格情報付与と同様に、コンソール アプリ コードを次に示します。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
