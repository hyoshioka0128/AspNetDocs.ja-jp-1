---
uid: web-api/overview/security/integrated-windows-authentication
title: 統合 Windows 認証 |Microsoft Docs
author: MikeWasson
description: ASP.NET Web API での統合 Windows 認証の使用について説明します。
ms.author: riande
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: c5fe57c4a20e28fa434659a75484e3a4c37195f8
ms.sourcegitcommit: 000cbcd1de66fe8a766f203ef2d6f009e4435f53
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86424783"
---
# <a name="integrated-windows-authentication"></a>統合 Windows 認証

[Mike Wasson](https://github.com/MikeWasson)

統合 Windows 認証を使用すると、ユーザーは、Kerberos または NTLM を使用して Windows 資格情報でログインできます。 クライアントは、Authorization ヘッダーで資格情報を送信します。 Windows 認証は、イントラネット環境に最適です。 詳細については、[Windows 認証](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)に関する記事を参照してください。

| 長所 | 短所 |
| --- | --- |
| IIS に組み込まれています。 | インターネットアプリケーションには推奨されません。 | 
| は、要求にユーザー資格情報を送信しません。 | クライアントで Kerberos または NTLM のサポートが必要です。 |
| クライアントコンピューターがドメイン (たとえば、イントラネットアプリケーション) に属している場合、ユーザーは資格情報を入力する必要はありません。 | クライアントは Active Directory ドメインに存在する必要があります。 |

> [!NOTE]
> アプリケーションが Azure でホストされていて、オンプレミスの Active Directory ドメインがある場合は、オンプレミスの AD と Azure Active Directory をフェデレーションすることを検討してください。 そうすることで、ユーザーはオンプレミスの資格情報を使用してログインできますが、認証は Azure AD によって実行されます。 詳細については、「 [Azure 認証](../../../visual-studio/overview/2012/windows-azure-authentication.md)」を参照してください。

統合 Windows 認証を使用するアプリケーションを作成するには、MVC 4 プロジェクトウィザードで [イントラネットアプリケーション] テンプレートを選択します。 このプロジェクトテンプレートは、Web.config ファイルに次の設定を格納します。

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

クライアント側では、統合 Windows 認証は、ほとんどの主要なブラウザーを含む[Negotiate](http://www.ietf.org/rfc/rfc4559.txt)認証スキームをサポートするすべてのブラウザーで動作します。 .NET クライアントアプリケーションの場合、 **Httpclient**クラスは Windows 認証をサポートします。

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

Windows 認証は、クロスサイト要求偽造 (CSRF) 攻撃に対して脆弱です。 「[クロスサイト要求偽造 (CSRF) 攻撃の防止](preventing-cross-site-request-forgery-csrf-attacks.md)」を参照してください。
