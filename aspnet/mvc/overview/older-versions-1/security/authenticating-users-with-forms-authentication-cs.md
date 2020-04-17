---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
title: フォーム認証を使用したユーザーの認証 (C#) |マイクロソフトドキュメント
author: rick-anderson
description: '[Authorize] 属性を使用して、MVC アプリケーションの特定のページをパスワードで保護する方法について説明します。 Web サイト管理の使用方法も学習します。'
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 239fd3ca-5630-4b8d-bc4b-2f906b1d3504
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: f14f996c0b3a438647b5d181675457735e473354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540975"
---
# <a name="authenticating-users-with-forms-authentication-c"></a>フォーム認証でユーザーを認証する (C#)

[マイクロソフト](https://github.com/microsoft)

> [Authorize] 属性を使用して、MVC アプリケーションの特定のページをパスワードで保護する方法について説明します。 Web サイト管理ツールを使用してユーザーとロールを作成および管理する方法について説明します。 また、ユーザー アカウントとロール情報の格納場所を構成する方法についても説明します。

このチュートリアルの目的は、フォーム認証を使用して、ASP.NET MVC アプリケーションのビューをパスワード保護する方法を説明することです。 Web サイト管理ツールを使用してユーザーとロールを作成する方法について説明します。 また、権限のないユーザーがコントローラのアクションを呼び出すことを防ぐ方法についても学習します。 最後に、ユーザー名とパスワードの保存場所を構成する方法を学習します。

#### <a name="using-the-web-site-administration-tool"></a>Web サイト管理ツールの使用

他の作業を行う前に、ユーザーとロールを作成する必要があります。 新しいユーザーとロールを作成する最も簡単な方法は、Visual Studio 2008 Web サイト管理ツールを利用することです。 このツールを起動するには、メニュー オプションの **[プロジェクト]、ASP.NET構成を選択**します。 または、ソリューション エクスプローラ ウィンドウの上部に表示される世界に当たるハンマーの (やや怖い) アイコンをクリックして Web サイト管理ツールを起動することもできます (図 1 参照)。

**図 1 – Web サイト管理ツールの起動**

![clip_image002](authenticating-users-with-forms-authentication-cs/_static/image1.jpg)

Web サイト管理ツールで、新しいユーザーとロールを作成するには、[セキュリティ] タブを**Create user**クリックします。 Stephen ユーザーに必要なパスワード (*たとえば、シークレット*) を指定します。

**図 2 – 新しいユーザーの作成**

![clip_image004](authenticating-users-with-forms-authentication-cs/_static/image2.jpg)

新しいロールを作成するには、まずロールを有効にし、1 つ以上のロールを定義します。 [ロールを有効にする] リンクをクリックして **、ロールを有効に**します。 次に、[役割の作成] または [**役割の管理**] リンクをクリックして *、管理者*という名前の役割を作成します (図 3 参照)。

**図 3 – 新しいロールの作成**

![clip_image006](authenticating-users-with-forms-authentication-cs/_static/image3.jpg)

最後に、Sally という名前の新しいユーザーを作成し、[ユーザーの作成] リンクをクリックし、Sally の作成時に [管理者] を選択して、Sally を管理者ロールに関連付けます (図 4 参照)。

**図 4 – ロールへのユーザーの追加**

![clip_image008](authenticating-users-with-forms-authentication-cs/_static/image4.jpg)

すべてが言われ、完了したら、Stephen と Sally という名前の 2 人の新しいユーザーを持つ必要があります。 また、管理者という名前の新しい役割も必要です。 サリーは管理者ロールのメンバーであり、スティーブンは属していません。

#### <a name="requiring-authorization"></a>認証の要求

ユーザーがコントローラー アクションを呼び出す前に、アクションに [Authorize] 属性を追加して、ユーザーを認証するように要求できます。 [Authorize] 属性を個々のコントローラー アクションに適用するか、この属性をコントローラ クラス全体に適用できます。

たとえば、リスト 1 のコントローラは、CompanySecrets() という名前のアクションを公開します。 このアクションは [Authorize] 属性で修飾されているため、ユーザーが認証されない限り、このアクションを呼び出すことはできません。

**リスト 1 - コントローラ\ホームコントローラー.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample1.cs)]

ブラウザーのアドレス バーに URL /Home/CompanySecrets を入力して CompanySecrets() アクションを呼び出し、認証されたユーザーでない場合は、自動的にログイン ビューにリダイレクトされます (図 5 参照)。

**図5 – ログインビュー**

![clip_image010](authenticating-users-with-forms-authentication-cs/_static/image5.jpg)

ログインビューを使用して、ユーザー名とパスワードを入力できます。 登録ユーザーでない場合は、登録リンクをクリックして**登録**ビューに移動できます (図 6 参照)。 登録ビューを使用して、新しいユーザー アカウントを作成できます。

**図6 – レジスタビュー**

![clip_image012](authenticating-users-with-forms-authentication-cs/_static/image6.jpg)

正常にログインすると、会社の秘密のビューが表示されます (図 7 参照)。 デフォルトでは、ブラウザウィンドウを閉じるまでログインし続けます。

**図 7 – 会社秘密ビュー**

![clip_image014](authenticating-users-with-forms-authentication-cs/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>ユーザー名またはユーザー ロールによる承認

[Authorize] 属性を使用すると、特定のユーザーセットまたは特定のユーザー ロール セットに対するコントローラ アクションへのアクセスを制限できます。 たとえば、リスト 2 で変更されたホーム コント ローラーには、StephenSecrets() と管理者の秘密() という名前の 2 つの新しいアクションが含まれています。

**リスト 2 - コントローラ\ホームコントローラー.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample2.cs)]

スティーブンというユーザー名を持つユーザーのみが、StephenSecrets() アクションを呼び出すことができます。 他のすべてのユーザーはログインビューにリダイレクトされます。 Users プロパティは、ユーザー アカウント名のコンマ区切りのリストを受け入れます。

管理者ロールのユーザーのみが管理者秘密() アクションを呼び出すことができます。 たとえば、サリーは管理者グループのメンバーであるため、管理者の秘密() アクションを呼び出すことができます。 他のすべてのユーザーはログインビューにリダイレクトされます。 ロール プロパティは、ロール名のコンマ区切りのリストを受け入れます。

#### <a name="configuring-authentication"></a>認証の構成

この時点で、ユーザー アカウントとロール情報がどこに格納されているか疑問に思うかもしれません。 既定では、情報は、MVC アプリケーションのアプリ\_データ フォルダーにある ASPNETDB.mdf という名前の (RANU) SQL Express データベースに格納されます。 このデータベースは、メンバーシップの使用を開始すると、ASP.NET フレームワークによって自動的に生成されます。

ソリューション エクスプ ローラー ウィンドウで ASPNETDB.mdf データベースを表示するには、最初にメニュー オプションプロジェクト、すべてのファイルを表示を選択する必要があります。

アプリケーションを開発する場合は、既定の SQL Express データベースを使用しても問題ありません。 ただし、ほとんどの場合、運用アプリケーションでは既定の ASPNETDB.mdf データベースを使用する必要はありません。 この場合、次の 2 つの手順を実行して、ユーザー アカウント情報の格納場所を変更できます。

1. アプリケーション サービス データベース オブジェクトを運用データベースに追加する - 実稼働データベースを指すアプリケーション接続文字列を変更する

最初の手順では、必要なデータベース オブジェクト (テーブルとストアド プロシージャ) をすべて運用データベースに追加します。 これらのオブジェクトを新しいデータベースに追加する最も簡単な方法は、sql Server セットアップ ウィザードASP.NETを利用することです (図 8 参照)。 このツールを起動する場合は、Visual Studio 2008 プログラム グループから Visual Studio 2008 コマンド プロンプトを開き、コマンド プロンプトから次のコマンドを実行します。

aspnet\_のレジストリー

**図 8 – sql Server セットアップ ウィザードASP.NET**

![clip_image016](authenticating-users-with-forms-authentication-cs/_static/image8.jpg)

SQL Serversql Server セットアップ ウィザードASP.NETを使用すると、ネットワーク上の SQL Server データベースを選択し、ASP.NET アプリケーション サービスに必要なすべてのデータベース オブジェクトをインストールできます。 データベース サーバーはローカル マシン上に配置する必要はありません。

> [!NOTE] 
> 
> SQL Server SQL Server セットアップ ウィザードASP.NETを使用しない場合は、次のフォルダにアプリケーション サービス データベース オブジェクトを追加するための SQL スクリプトを検索できます。
> 
> > C:\Windows\マイクロソフト.NET\フレームワーク\v2.0.50727

必要なデータベース オブジェクトを作成した後、MVC アプリケーションで使用されるデータベース接続を変更する必要があります。 Web 構成 (web.config) ファイル内の ApplicationServices 接続文字列を変更して、運用データベースを指します。 たとえば、リスト 3 の変更された接続は、MyProductionDB という名前のデータベースを指しています (元の ApplicationServices 接続文字列はコメント アウトされています)。

**リスト 3 - Web.config**

[!code-xml[Main](authenticating-users-with-forms-authentication-cs/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>データベース権限の設定

統合セキュリティを使用してデータベースに接続する場合は、データベースへのログインとして正しい Windows ユーザー アカウントを追加する必要があります。 正しいアカウントは、web サーバーとして開発サーバーまたはインターネット インフォメーション サービスASP.NETを使用しているかどうかによって異なります。 正しいユーザー アカウントは、オペレーティング システムによっても異なります。

ASP.NET開発サーバー (Visual Studio で使用される既定の Web サーバー) を使用している場合、アプリケーションは Windows ユーザー アカウントのコンテキスト内で実行されます。 その場合は、Windows ユーザー アカウントをデータベース サーバー ログインとして追加する必要があります。

または、インターネット インフォメーション サービスを使用している場合は、データベース サーバー ログインとして ASPNET アカウントまたは NT AUTHORITY/NETWORK SERVICE アカウントを追加する必要があります。 Windows XP を使用している場合は、データベースへのログインとして ASPNET アカウントを追加します。 Windows Vista や Windows Server 2008 など、より新しいオペレーティング システムを使用している場合は、NT オーソリティ/ネットワーク サービス アカウントをデータベース ログインとして追加します。

新しいユーザー アカウントをデータベースに追加するには、Microsoft SQL Server 管理スタジオを使用します (図 9 参照)。

**図 9 – 新しい SQL Server ログインの作成**

![clip_image018](authenticating-users-with-forms-authentication-cs/_static/image9.jpg)

必要なログインを作成したら、適切なデータベース ロールを持つデータベース ユーザーにログインをマップする必要があります。 ログインをダブルクリックし、[ユーザー マッピング] タブを選択します。 たとえば、ユーザーを認証するには、aspnet\_メンバーシップ\_の BasicAccess データベース ロールを有効にする必要があります。 新しいユーザーを作成するには、aspnet\_メンバーシップ\_FullAccess データベース ロールを有効にする必要があります (図 10 を参照)。

**図 10 – アプリケーション サービス データベース ロールの追加**

![clip_image020](authenticating-users-with-forms-authentication-cs/_static/image10.jpg)

#### <a name="summary"></a>まとめ

このチュートリアルでは、ASP.NETの MVC アプリケーションを構築するときにフォーム認証を使用する方法を学習しました。 最初に、Web サイト管理ツールを利用して新しいユーザーとロールを作成する方法を学習しました。 次に、[Authorize] 属性を使用して、承認されていないユーザーがコントローラアクションを呼び出すことを防ぐ方法を学習しました。 最後に、ユーザーとロールの情報を運用データベースに格納するように MVC アプリケーションを構成する方法を学習しました。

> [!div class="step-by-step"]
> [次へ](authenticating-users-with-windows-authentication-cs.md)
