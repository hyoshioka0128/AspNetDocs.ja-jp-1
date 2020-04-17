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
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="cf234-103">CAPTCHA を使用してボットが ASP.NET Web Razor) サイトを使用できないようにする</span><span class="sxs-lookup"><span data-stu-id="cf234-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="cf234-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="cf234-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="cf234-105">この記事では、ReCaptcha (セキュリティ対策) を使用して、自動化されたプログラム (ボット) が ASP.NET Web ページ (Razor) Web サイトでタスクを実行できないようにする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="cf234-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="cf234-106">**ここでは、次の内容について学習します。**</span><span class="sxs-lookup"><span data-stu-id="cf234-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="cf234-107">CAPTCHA テストをサイトに追加する方法。</span><span class="sxs-lookup"><span data-stu-id="cf234-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="cf234-108">この記事で紹介したASP.NET機能を次に示します。</span><span class="sxs-lookup"><span data-stu-id="cf234-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="cf234-109">ヘルパー `ReCaptcha` 。</span><span class="sxs-lookup"><span data-stu-id="cf234-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="cf234-110">この資料の情報は、Web ページ 1.0 および Web ページ 2 ASP.NETに適用されます。</span><span class="sxs-lookup"><span data-stu-id="cf234-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="cf234-111">キャプチャスについて</span><span class="sxs-lookup"><span data-stu-id="cf234-111">About CAPTCHAs</span></span>

<span data-ttu-id="cf234-112">ユーザーがサイトに登録したり、名前や URL (ブログコメントなど) を入力したりするたびに、偽の名前が殺到する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="cf234-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="cf234-113">これらは、多くの場合、検索できるすべてのウェブサイトにURLを残そうとする自動化されたプログラム(ボット)によって残されます。</span><span class="sxs-lookup"><span data-stu-id="cf234-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="cf234-114">(一般的な動機は、販売のための製品のURLを投稿することです。</span><span class="sxs-lookup"><span data-stu-id="cf234-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="cf234-115">ユーザーが登録時にユーザーを検証したり、名前やサイトを入力したりする際に *、ユーザー*が実際のユーザーであり、コンピュータ プログラムではないことを確認できます。</span><span class="sxs-lookup"><span data-stu-id="cf234-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="cf234-116">CAPTCHAは、コンピュータと人間を区別するために完全に自動化されたパブリックチューリングテストの略です。</span><span class="sxs-lookup"><span data-stu-id="cf234-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="cf234-117">CAPTCHA は、ユーザーが簡単に行うが、自動化されたプログラムが行うには難しいことを行うユーザーを求められる*チャレンジ応答*テストです。</span><span class="sxs-lookup"><span data-stu-id="cf234-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="cf234-118">CAPTCHA の最も一般的なタイプは、歪んだ文字を見て、それらを入力するように求められるものです。</span><span class="sxs-lookup"><span data-stu-id="cf234-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="cf234-119">(歪みによって、ボットが文字を解読するのが難しくなります。</span><span class="sxs-lookup"><span data-stu-id="cf234-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="cf234-120">再キャプチャテストの追加</span><span class="sxs-lookup"><span data-stu-id="cf234-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="cf234-121">ASP.NETページでは、ヘルパーを`ReCaptcha`使用して、ReCaptcha サービス ( )[http://recaptcha.net](http://recaptcha.net)に基づく CAPTCHA テストをレンダリングできます。</span><span class="sxs-lookup"><span data-stu-id="cf234-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="cf234-122">ヘルパー`ReCaptcha`は、ページが検証される前にユーザーが正しく入力する必要がある 2 つの歪んだ単語のイメージを表示します。</span><span class="sxs-lookup"><span data-stu-id="cf234-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="cf234-123">ユーザーの応答は、ReCaptcha.Net サービスによって検証されます。</span><span class="sxs-lookup"><span data-stu-id="cf234-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="cf234-124">ReCaptcha.Net ( )[http://recaptcha.net](http://recaptcha.net)でウェブサイトを登録する</span><span class="sxs-lookup"><span data-stu-id="cf234-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="cf234-125">登録が完了すると、公開キーと秘密キーが取得されます。</span><span class="sxs-lookup"><span data-stu-id="cf234-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="cf234-126">ASP.NET Web ヘルパー ライブラリを web サイトに追加します[(ASP.NET Web ページ サイトへのヘルパーのインストール](https://go.microsoft.com/fwlink/?LinkId=252372)にまだ必要ない場合)。</span><span class="sxs-lookup"><span data-stu-id="cf234-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="cf234-127">AppStart.cshtml ファイルをまだ持っていない場合は、Web サイトのルート フォルダに*\_AppStart.cshtml*という名前のファイルが作成されます。 \* \_\*</span><span class="sxs-lookup"><span data-stu-id="cf234-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="cf234-128">`Recaptcha` \* \_AppStart.cshtml\*ファイルに次のヘルパー設定を追加します。</span><span class="sxs-lookup"><span data-stu-id="cf234-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="cf234-129">独自の`PublicKey`公開`PrivateKey`キーと秘密キーを使用して、 および プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="cf234-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="cf234-130">*\_ファイル*を保存し、閉じます。</span><span class="sxs-lookup"><span data-stu-id="cf234-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="cf234-131">Web サイトのルート フォルダに *、Recaptcha.cshtml*という名前の新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf234-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="cf234-132">既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cf234-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="cf234-133">ブラウザーで*Recaptcha.cshtml*ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="cf234-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="cf234-134">値が`PrivateKey`有効な場合、ページには ReCaptcha コントロールとボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="cf234-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="cf234-135">\* \_AppStart.html\*でキーをグローバルに設定していない場合、ページにエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="cf234-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="cf234-136">テストの単語を入力します。</span><span class="sxs-lookup"><span data-stu-id="cf234-136">Enter the words for the test.</span></span> <span data-ttu-id="cf234-137">ReCaptcha テストに合格すると、その効果に対するメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="cf234-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="cf234-138">それ以外の場合は、エラー メッセージが表示され、ReCaptcha コントロールが再表示されます。</span><span class="sxs-lookup"><span data-stu-id="cf234-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="cf234-139">コンピュータがプロキシ サーバーを使用するドメイン上にある場合は *、Web.config* `defaultproxy`ファイルの要素を構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cf234-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="cf234-140">次の例は、ReCaptcha サービスが`defaultproxy`機能するように構成された要素を持つ*Web.config*ファイルを示しています。</span><span class="sxs-lookup"><span data-stu-id="cf234-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="cf234-141">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="cf234-141">Additional Resources</span></span>

- [<span data-ttu-id="cf234-142">ASP.NET Web ページ サイトのサイト全体の動作をカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="cf234-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="cf234-143">レカプチャサイト</span><span class="sxs-lookup"><span data-stu-id="cf234-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
