---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 認証と承認を使用したアプリケーションのセキュリティ保護 |マイクロソフトドキュメント
author: rick-anderson
description: ステップ 9 では、NerdDinner アプリケーションをセキュリティで保護するための認証と承認を追加する方法を示しています。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: d96f2763f6e62f9dd599fdb7977a97993d218305
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542574"
---
# <a name="secure-applications-using-authentication-and-authorization"></a>認証と承認を利用した安全なアプリケーション

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、mvc 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)ASP.NET手順 9 です。
> 
> 手順 9 では、NerdDinner アプリケーションをセキュリティで保護するための認証と承認を追加する方法を示し、ユーザーが登録してサイトにログインして新しいディナーを作成する必要があり、ディナーをホストしているユーザーだけが後で編集できるようにします。
> 
> mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。

## <a name="nerddinner-step-9-authentication-and-authorization"></a>NerdDinner ステップ 9: 認証と承認

今私たちのNerdDinnerアプリケーションは、任意の夕食の詳細を作成し、編集するサイトを訪問する人を付与します。 ユーザーが登録してサイトにログインして新しいディナーを作成し、ディナーをホストしているユーザーだけが後で編集できるように制限を追加するように、これを変更してみましょう。

これを有効にするには、認証と承認を使用してアプリケーションを保護します。

### <a name="understanding-authentication-and-authorization"></a>認証と承認について

*認証*とは、アプリケーションにアクセスするクライアントの ID を識別して検証するプロセスです。 より簡単に言えば、エンドユーザーがウェブサイトを訪れたときに「誰」であるかを特定することです。 ASP.NETは、ブラウザーユーザーを認証する複数の方法をサポートしています。 インターネット Web アプリケーションの場合、最も一般的な認証方法は"フォーム認証" と呼ばれます。 フォーム認証を使用すると、開発者はアプリケーション内で HTML ログイン フォームを作成し、エンド ユーザーが送信するユーザー名とパスワードをデータベースやその他のパスワード資格情報ストアに照らして検証できます。 ユーザー名とパスワードの組み合わせが正しい場合、開発者はASP.NETに、暗号化された HTTP Cookie を発行して、将来の要求を超えてユーザーを識別するように依頼できます。 NerdDinner アプリケーションでは、フォーム認証を使用します。

*承認*とは、認証されたユーザーが特定の URL/リソースにアクセスする権限を持っているかどうか、または何らかのアクションを実行する権限を持っているかどうかを判断するプロセスです。 たとえば、NerdDinner アプリケーションでは、ログインしているユーザーのみが */Dinners/CREATE* URL にアクセスし、新しいディナーを作成することを承認します。 また、ディナーをホストしているユーザーだけが編集できるように承認ロジックを追加し、他のすべてのユーザーに対する編集アクセスを拒否することもできます。

### <a name="forms-authentication-and-the-accountcontroller"></a>フォーム認証とアカウント コントローラー

ASP.NET MVC の既定の Visual Studio プロジェクト テンプレートは、新しいASP.NET MVC アプリケーションが作成されたときに自動的にフォーム認証を有効にします。 また、事前に作成されたアカウントログインページの実装がプロジェクトに自動的に追加され、サイト内のセキュリティを簡単に統合できます。

既定の Site.master マスター ページには、アクセスするユーザーが認証されていない場合、サイトの右上に "ログオン" リンクが表示されます。

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

[ログオン] リンクをクリックすると、ユーザーは */アカウント/ログオン*URL に移動します。

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

登録していない訪問者は *、"* 登録" リンクをクリックして登録できます 。

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

[登録] ボタンをクリックすると、ASP.NET メンバーシップ システム内に新しいユーザーが作成され、フォーム認証を使用してサイトにユーザーを認証します。

ユーザーがログインすると、Site.master はページの右上を変更して"ようこそ [ユーザー名]" を出力します。 メッセージを表示し、"ログオン" リンクではなく "ログオフ" リンクをレンダリングします。 [ログオフ] リンクをクリックすると、ユーザーがログアウトします。

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

上記のログイン、ログアウト、および登録の機能は、プロジェクトの作成時に Visual Studio によってプロジェクトに追加された AccountController クラス内に実装されています。 アカウント コント ローラーの UI は、\ビュー\アカウント ディレクトリ内のビュー テンプレートを使用して実装されます。

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

クラスは、ASP.NETフォーム認証システムを使用して暗号化認証クッキーを発行し、ASP.NETメンバーシップAPIを使用してユーザー名/パスワードを保存および検証します。 ASP.NET メンバーシップ API は拡張可能で、任意のパスワード資格情報ストアを使用できます。 ASP.NETには、SQL データベース内または Active Directory 内にユーザー名とパスワードを格納する組み込みのメンバーシップ プロバイダー実装が付属しています。

NerdDinner アプリケーションが使用するメンバーシップ プロバイダを構成するには、プロジェクトのルートにある "web.config" ファイルを開き、その&lt;中&gt;のメンバーシップ セクションを探します。 プロジェクトの作成時に追加された既定の web.config SQL メンバーシップ プロバイダーを登録し、データベースの場所を指定するのには "ApplicationServices" という名前の接続文字列を使用するように構成します。

既定の "アプリケーション サービス" 接続文字列 (web.config ファイルの&lt;接続文字列&gt;セクションで指定) は、SQL Express を使用するように構成されています。 これは、"ASPNETDB" という名前の SQL Express データベースを指しています。MDF" アプリケーションの 「アプリ\_データ」 ディレクトリの下に表示されます。 アプリケーション内で初めて Membership API を使用するときにこのデータベースが存在しない場合、ASP.NETは自動的にデータベースを作成し、適切なメンバーシップ データベース スキーマをその中にプロビジョニングします。

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

SQL Express を使用する代わりに、完全な SQL Server インスタンスを使用する (またはリモート データベースに接続する) 場合は、web.config ファイル内の "ApplicationServices" 接続文字列を更新し、適切なメンバーシップ スキーマがデータベースに追加されていることを確認するだけです。 \Windows\Microsoft.NET\Framework\v2.0.50727\ ディレクトリ内で "aspnet\_regsql.exe" ユーティリティを実行すると、メンバーシップやその他のASP.NETアプリケーション サービスに対する適切なスキーマをデータベースに追加できます。

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>[承認] フィルターを使用して 、/ディナー/URL の作成を承認します。

NerdDinner アプリケーションの安全な認証とアカウント管理の実装を有効にするコードを記述する必要はありませんでした。 ユーザーは、当社のアプリケーションに新しいアカウントを登録し、サイトのログイン/ログアウトを行うことができます。

これで、承認ロジックをアプリケーションに追加し、訪問者の認証ステータスとユーザー名を使用して、サイト内で何ができるか、またはできないかを制御できるようになりました。 まず、DinnersController クラスの "作成" アクション メソッドに承認ロジックを追加します。 具体的には *、/Dinners/CREATE* URL にアクセスするユーザーがログインする必要があります。 ログインしていない場合は、ログインページにリダイレクトしてログインできるようにします。

このロジックを実装するのは非常に簡単です。 必要なのは、次のように Create アクション メソッドに [Authorize] フィルター属性を追加することだけです。

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC では、アクション メソッドに宣言的に適用できる再使用できるロジックを実装するために使用できる "アクション フィルター" を作成する機能がサポートされています。 [Authorize] フィルターは、ASP.NET MVC によって提供される組み込みのアクション フィルターの 1 つであり、開発者がアクション メソッドとコント ローラー クラスに承認規則を宣言的に適用できるようにします。

上記のようなパラメータを指定せずに適用すると、[Authorize] フィルタはアクションメソッドリクエストを行うユーザーがログインする必要があることを強制し、ログインURLが存在しない場合は自動的にブラウザをリダイレクトします。 このリダイレクトを行うとき、最初に要求された URL はクエリ文字列引数として渡されます (たとえば、/Account/LogOn?を返します。 アカウント コント ローラーは、ユーザーがログインすると、最初に要求された URL にリダイレクトします。

[Authorize] フィルターは、ユーザーがログインし、許可されたユーザーの一覧または許可されたセキュリティ ロールのメンバーの両方に含まれるようにするために使用できる "ユーザー" または "ロール" プロパティを指定する機能をオプションでサポートします。 たとえば、次のコードでは、"scottgu" と "billg" の 2 人の特定のユーザーのみが /Dinners/CREATE URL にアクセスできます。

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

特定のユーザー名をコードに埋め込むと、保守が容易にできない傾向があります。 より良い方法は、コードがチェックする上位レベルの "ロール" を定義し、データベースまたはアクティブディレクトリ システムを使用してユーザーをロールにマップすることです (実際のユーザー マッピング リストをコードから外部に格納できるようにします)。 ASP.NETには、組み込みのロール管理 API と、このユーザー/ロール マッピングの実行に役立つロール プロバイダー (SQL および Active Directory 用のロール プロバイダーを含む) の組み込みセットが含まれます。 次に、特定の 「管理者」ロール内のユーザーのみが /Dinners/CREATE URL にアクセスできるようにコードを更新できます。

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>ディナー作成時にUser.Identity.Nameプロパティを使用する

Controller 基本クラスで公開されるUser.Identity.Nameプロパティを使用して、現在ログインしている要求のユーザーのユーザー名を取得できます。

以前は、Create() アクションメソッドの HTTP-POST バージョンを実装したときに、Dinner の "HostedBy" プロパティを静的な文字列にハードコーディングしていました。 このコードを更新して、User.Identity.Nameプロパティを使用したり、Dinner を作成するホスト用に RSVP を自動的に追加したりできます。

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

Create() メソッドに [Authorize] 属性を追加したので、ASP.NET MVC は、/Dinners/Create URL にアクセスするユーザーがサイトにログインしている場合にのみアクション メソッドが実行されるようにします。 したがって、User.Identity.Nameプロパティ値には常に有効なユーザー名が含まれます。

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>ディナーの編集時にUser.Identity.Nameプロパティを使用する

ここで、ユーザー自身がホストしているディナーのプロパティのみを編集できるように制限する承認ロジックを追加してみましょう。

これを支援するために、まず、Dinner オブジェクトに "IsHostedBy(ユーザー名)" ヘルパー メソッドを追加します (Dinner.cs部分クラス内で以前に構築しました)。 このヘルパー メソッドは、指定されたユーザー名が Dinner HostedBy プロパティと一致するかどうかに応じて true または false を返し、大文字と小文字を区別しない文字列比較を実行するために必要なロジックをカプセル化します。

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

次に、DinnersController クラス内の Edit() アクション メソッドに [Authorize] 属性を追加します。 これにより、ユーザーが */Dinners/Edit/[id]* URL を要求するためにログインする必要があります。

その後、Dinner.IsHostedBy(ユーザー名) ヘルパー メソッドを使用して、ログインしているユーザーが Dinner ホストと一致することを確認するコードを Edit メソッドに追加できます。 ユーザーがホストでない場合は、"無効な所有者" ビューを表示し、要求を終了します。 これを行うコードは次のようになります。

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

次に、\Views\Dinners ディレクトリを右クリックし、[追加-&gt;表示] メニュー コマンドを選択して、新しい "無効な所有者" ビューを作成します。 次のエラー メッセージを設定します。

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

そして今、ユーザーが自分が所有していないディナーを編集しようとすると、エラーメッセージが表示されます。

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

私たちのコントローラ内のDelete()アクションメソッドについても同じ手順を繰り返して、Dinnersを削除する権限をロックダウンし、Dinnerのホストだけがそれを削除できるようにします。

### <a name="showinghiding-edit-and-delete-links"></a>編集リンクと削除リンクの表示/非表示

詳細 URL から DinnersController クラスの編集と削除のアクション メソッドにリンクしています。

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

現在、詳細 URL への訪問者がディナーのホストであるかどうかに関係なく、編集と削除のアクション リンクが表示されます。 訪問先のユーザーがディナーの所有者である場合にのみリンクが表示されるように、これを変更してみましょう。

DinnersController 内の Details() アクション メソッドは、Dinner オブジェクトを取得し、モデル オブジェクトとしてビュー テンプレートに渡します。

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

次のような Dinner.IsHostedBy() ヘルパー メソッドを使用して、ビュー テンプレートを更新して、編集リンクと削除リンクを条件付きで表示/非表示にすることができます。

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>次の手順

それでは、AJAX を使用して、RSVP に対して認証されたユーザーを有効にする方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](implement-efficient-data-paging.md)
> [次へ](use-ajax-to-deliver-dynamic-updates.md)
