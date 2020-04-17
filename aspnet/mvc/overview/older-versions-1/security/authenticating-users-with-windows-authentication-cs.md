---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
title: Windows 認証を使用したユーザーの認証 (C#) |マイクロソフトドキュメント
author: rick-anderson
description: MVC アプリケーションのコンテキストで Windows 認証を使用する方法について説明します。 アプリケーションの Web co.で Windows 認証を有効にする方法を学習します。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 418bb07e-f369-4119-b4b0-08f890f7abb2
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: fb6ba3d52d7c70d61c6aa16b4ada67cc6bdd4f96
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540741"
---
# <a name="authenticating-users-with-windows-authentication-c"></a>Windows 認証でユーザーを認証する (C#)

[マイクロソフト](https://github.com/microsoft)

> MVC アプリケーションのコンテキストで Windows 認証を使用する方法について説明します。 アプリケーションの Web 構成ファイル内で Windows 認証を有効にする方法と、IIS で認証を構成する方法について説明します。 最後に、[Authorize] 属性を使用して、特定の Windows ユーザーまたはグループに対するコントローラ アクションへのアクセスを制限する方法を学習します。

このチュートリアルの目的は、インターネット インフォメーション サービスに組み込まれているセキュリティ機能を利用して、MVC アプリケーションのビューをパスワードで保護する方法を説明することです。 特定の Windows グループのメンバーである特定の Windows ユーザーまたはユーザーのみがコントローラー アクションを呼び出す方法について説明します。

社内の Web サイト (イントラネット サイト) を構築する場合、ユーザーが Web サイトにアクセスするときに標準の Windows ユーザー名とパスワードを使用できるようにする場合は、Windows 認証を使用するのが理にかなっています。 外向きの Web サイト (インターネット Web サイト) を構築する場合は、代わりにフォーム認証を使用することを検討してください。

#### <a name="enabling-windows-authentication"></a>Windows 認証を有効にする

新しいASP.NET MVC アプリケーションを作成すると、Windows 認証は既定で有効になっていません。 フォーム認証は、MVC アプリケーションで有効になっている既定の認証の種類です。 WINDOWS 認証を有効にするには、MVC アプリケーションの Web 構成 (web.config) ファイルを変更する必要があります。 次のように&lt;、&gt;認証セクションを見つけて、フォーム認証の代わりに Windows を使用するように変更します。

[!code-xml[Main](authenticating-users-with-windows-authentication-cs/samples/sample1.xml)]

Windows 認証を有効にすると、Web サーバーがユーザーの認証を担当します。 通常、ASP.NETの MVC アプリケーションを作成および展開するときに使用する Web サーバーには、2 種類の異なる種類があります。

まず、MVC アプリケーションを開発する際に、Visual Studio に含まれる開発 web サーバーASP.NETを使用します。 既定では、開発 ASP.NET Web サーバーは、現在の Windows アカウント (Windows へのログインに使用したアカウント) のコンテキストですべてのページを実行します。

開発用 web サーバーASP.NETは、NTLM 認証もサポートしています。 NTLM 認証を有効にするには、[ソリューション エクスプローラー] ウィンドウでプロジェクトの名前を右クリックし、[プロパティ] を選択します。 次に、[Web] タブを選択し、[NTLM] チェックボックスをオンにします (図 1 参照)。

**図 1 – ASP.NET開発 Web サーバーの NTLM 認証を有効にする**

![clip_image002](authenticating-users-with-windows-authentication-cs/_static/image1.jpg)

運用 Web アプリケーションの場合は、一方で、Web サーバーとして IIS を使用します。 IIS では、次のようないくつかの種類の認証がサポートされています。

- 基本認証 – HTTP 1.0 プロトコルの一部として定義されます。 インターネット経由でユーザー名とパスワードをクリア テキスト (Base64 エンコード) で送信します。 - ダイジェスト認証 – インターネット上でパスワード自体ではなく、パスワードのハッシュを送信します。 - 統合 Windows (NTLM) 認証 – Windows を使用するイントラネット環境で使用する最適な認証の種類。 - 証明書認証 - クライアント側の証明書を使用した認証を有効にします。 証明書は Windows ユーザー アカウントにマップされます。

> [!NOTE] 
> 
> これらの異なる種類の認証の詳細な概要については、を[https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)参照してください。

インターネット インフォメーション サービス マネージャを使用して、特定の種類の認証を有効にすることができます。 すべてのオペレーティング システムの場合、すべての種類の認証を使用できるわけではないことに注意してください。 さらに、Windows Vista で IIS 7.0 を使用している場合は、インターネット インフォメーション サービス マネージャに表示される前に、さまざまな種類の Windows 認証を有効にする必要があります。 **コントロール パネル、[プログラム]、[プログラムと機能]、[Windows の機能のオン/オフ切り替え**] を開き、[インターネット インフォメーション サービス] ノードを展開します (図 2 参照)。

**図 2 – Windows IIS 機能を有効にする**

![clip_image004](authenticating-users-with-windows-authentication-cs/_static/image2.jpg)

インターネット インフォメーション サービスを使用すると、さまざまな種類の認証を有効または無効にできます。 たとえば、図 3 は、IIS 7.0 を使用する場合に、匿名認証を無効にし、統合 Windows (NTLM) 認証を有効にする方法を示しています。

**図 3 – 統合 Windows 認証の有効化**

![clip_image006](authenticating-users-with-windows-authentication-cs/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>Windows ユーザーとグループの承認

Windows 認証を有効にした後、[Authorize] 属性を使用して、コントローラーまたはコントローラーアクションへのアクセスを制御できます。 この属性は、MVC コントローラー全体または特定のコントローラー アクションに適用できます。

たとえば、リスト 1 のホーム コントローラは、インデックス()、カンパニークレッツ()、およびスティーブンシークレット() という名前の 3 つのアクションを公開します。 誰でも Index() アクションを呼び出すことができます。 ただし、Windows ローカル マネージャー グループのメンバーのみが、会社の秘密() アクションを呼び出すことができます。 最後に、スティーブンという名前の Windows ドメイン ユーザー (レドモンド ドメイン内) のみが StephenSecrets() アクションを呼び出すことができます。

**リスト 1 - コントローラ\ホームコントローラー.cs**

[!code-csharp[Main](authenticating-users-with-windows-authentication-cs/samples/sample2.cs)]

> [!NOTE] 
> 
> Windows ユーザー アカウント制御 (UAC) が原因で、Windows Vista または Windows Server 2008 で作業する場合、ローカルの管理者グループは他のグループとは異なる動作をします。 [Authorize] 属性は、コンピューターの UAC 設定を変更しない限り、ローカルの Administrators グループのメンバーを正しく認識しません。

適切なアクセス許可を持たずにコントローラ アクションを呼び出そうとすると、有効な認証の種類によって異なります。 既定では、ASP.NET開発サーバーを使用すると、空白のページが表示されます。 このページには **、401 認証なし**HTTP 応答ステータスが表示されます。

一方、匿名認証を無効にして基本認証を有効にした IIS を使用している場合は、保護されたページを要求するたびにログイン ダイアログ プロンプトが表示されます (図 4 参照)。

**図4 – 基本認証ログインダイアログ**

![clip_image008](authenticating-users-with-windows-authentication-cs/_static/image4.jpg)

#### <a name="summary"></a>まとめ

このチュートリアルでは、ASP.NET MVC アプリケーションのコンテキストで Windows 認証を使用する方法について説明しました。 アプリケーションの Web 構成ファイル内で Windows 認証を有効にする方法と、IIS で認証を構成する方法について学習しました。 最後に、[Authorize] 属性を使用して、特定の Windows ユーザーまたはグループに対するコントローラ アクションへのアクセスを制限する方法を学習しました。

> [!div class="step-by-step"]
> [前へ](authenticating-users-with-forms-authentication-cs.md)
> [次へ](preventing-javascript-injection-attacks-cs.md)
