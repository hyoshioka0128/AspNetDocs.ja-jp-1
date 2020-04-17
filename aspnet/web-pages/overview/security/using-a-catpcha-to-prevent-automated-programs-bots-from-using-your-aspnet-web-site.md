---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: CAPTCHA を使用してボットが ASP.NET Web Razor) サイトを使用できないようにする |マイクロソフトドキュメント
author: rick-anderson
description: この記事では、ReCaptcha (セキュリティ対策) を使用して、自動化されたプログラム (ボット) が ASP.NET web ページ (Razor) でタスクを実行できないようにする方法について説明します。
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 65f414ae3fed5e2fa28b1e57f5327c6411a43d55
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543757"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>CAPTCHA を使用してボットが ASP.NET Web Razor) サイトを使用できないようにする

[マイクロソフト](https://github.com/microsoft)

> この記事では、ReCaptcha (セキュリティ対策) を使用して、自動化されたプログラム (ボット) が ASP.NET Web ページ (Razor) Web サイトでタスクを実行できないようにする方法について説明します。
> 
> **ここでは、次の内容について学習します。** 
> 
> - CAPTCHA テストをサイトに追加する方法。
> 
> この記事で紹介したASP.NET機能を次に示します。
> 
> - ヘルパー `ReCaptcha` 。
> 
> > [!NOTE]
> > この資料の情報は、Web ページ 1.0 および Web ページ 2 ASP.NETに適用されます。

## <a name="about-captchas"></a>キャプチャスについて

ユーザーがサイトに登録したり、名前や URL (ブログコメントなど) を入力したりするたびに、偽の名前が殺到する可能性があります。 これらは、多くの場合、検索できるすべてのウェブサイトにURLを残そうとする自動化されたプログラム(ボット)によって残されます。 (一般的な動機は、販売のための製品のURLを投稿することです。

ユーザーが登録時にユーザーを検証したり、名前やサイトを入力したりする際に *、ユーザー*が実際のユーザーであり、コンピュータ プログラムではないことを確認できます。 CAPTCHAは、コンピュータと人間を区別するために完全に自動化されたパブリックチューリングテストの略です。 CAPTCHA は、ユーザーが簡単に行うが、自動化されたプログラムが行うには難しいことを行うユーザーを求められる*チャレンジ応答*テストです。 CAPTCHA の最も一般的なタイプは、歪んだ文字を見て、それらを入力するように求められるものです。 (歪みによって、ボットが文字を解読するのが難しくなります。

## <a name="adding-a-recaptcha-test"></a>再キャプチャテストの追加

ASP.NETページでは、ヘルパーを`ReCaptcha`使用して、ReCaptcha サービス ( )[http://recaptcha.net](http://recaptcha.net)に基づく CAPTCHA テストをレンダリングできます。 ヘルパー`ReCaptcha`は、ページが検証される前にユーザーが正しく入力する必要がある 2 つの歪んだ単語のイメージを表示します。 ユーザーの応答は、ReCaptcha.Net サービスによって検証されます。

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. ReCaptcha.Net ( )[http://recaptcha.net](http://recaptcha.net)でウェブサイトを登録する 登録が完了すると、公開キーと秘密キーが取得されます。
2. ASP.NET Web ヘルパー ライブラリを web サイトに追加します[(ASP.NET Web ページ サイトへのヘルパーのインストール](https://go.microsoft.com/fwlink/?LinkId=252372)にまだ必要ない場合)。
3. AppStart.cshtml ファイルをまだ持っていない場合は、Web サイトのルート フォルダに*\_AppStart.cshtml*という名前のファイルが作成されます。 * \_*
4. `Recaptcha` * \_AppStart.cshtml*ファイルに次のヘルパー設定を追加します。 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. 独自の`PublicKey`公開`PrivateKey`キーと秘密キーを使用して、 および プロパティを設定します。
6. *\_ファイル*を保存し、閉じます。
7. Web サイトのルート フォルダに *、Recaptcha.cshtml*という名前の新しいページを作成します。
8. 既存のコンテンツを次の内容に置き換えます。 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. ブラウザーで*Recaptcha.cshtml*ページを実行します。 値が`PrivateKey`有効な場合、ページには ReCaptcha コントロールとボタンが表示されます。 * \_AppStart.html*でキーをグローバルに設定していない場合、ページにエラーが表示されます。 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. テストの単語を入力します。 ReCaptcha テストに合格すると、その効果に対するメッセージが表示されます。 それ以外の場合は、エラー メッセージが表示され、ReCaptcha コントロールが再表示されます。

> [!NOTE]
> コンピュータがプロキシ サーバーを使用するドメイン上にある場合は *、Web.config* `defaultproxy`ファイルの要素を構成する必要があります。 次の例は、ReCaptcha サービスが`defaultproxy`機能するように構成された要素を持つ*Web.config*ファイルを示しています。
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>その他のリソース

- [ASP.NET Web ページ サイトのサイト全体の動作をカスタマイズする](https://go.microsoft.com/fwlink/?LinkId=202906)
- [レカプチャサイト](https://www.google.com/recaptcha)
