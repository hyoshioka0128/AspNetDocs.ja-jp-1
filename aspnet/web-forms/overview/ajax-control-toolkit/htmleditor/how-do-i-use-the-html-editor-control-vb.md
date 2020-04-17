---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
title: HTML エディタ コントロールを使用する方法 (VB) |マイクロソフトドキュメント
author: rick-anderson
description: HTMLEditor は、ツールバーのボタンを使用して HTML コンテンツを簡単に作成および編集できる AJAX コントロールASP.NETです。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 32ec9321-7c8c-4b0f-8234-99acb56df6b5
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
msc.type: authoredcontent
ms.openlocfilehash: bba42b4b6ff130b209b92c1608bc37f2f574c19c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542834"
---
# <a name="how-do-i-use-the-html-editor-control-vb"></a><span data-ttu-id="d8b92-104">HTML エディタ コントロールを使用する方法</span><span class="sxs-lookup"><span data-stu-id="d8b92-104">How do I use the HTML Editor Control?</span></span> <span data-ttu-id="d8b92-105">(VB)</span><span class="sxs-lookup"><span data-stu-id="d8b92-105">(VB)</span></span>

<span data-ttu-id="d8b92-106">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d8b92-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d8b92-107">HTMLEditor は、ツールバーのボタンを使用して HTML コンテンツを簡単に作成および編集できる AJAX コントロールASP.NETです。</span><span class="sxs-lookup"><span data-stu-id="d8b92-107">HTMLEditor is an ASP.NET AJAX Control that allows you to easily create and edit HTML content via buttons in a toolbar.</span></span>

<span data-ttu-id="d8b92-108">このチュートリアルの目的は、AJAX コントロール ツールキットに含まれている HTML エディター コントロールの概要を提供することです。</span><span class="sxs-lookup"><span data-stu-id="d8b92-108">The goal of this tutorial is to provide you with an overview of the HTML Editor control included with the AJAX Control Toolkit.</span></span> <span data-ttu-id="d8b92-109">HTML エディタには、フォント サイズの変更、フォントの選択、背景色の変更、前景色の変更、リンクの追加、画像の追加、テキストの配置の変更、切り取り、コピー、および貼り付け操作を行うためのオプションがあります (図 1 参照)。</span><span class="sxs-lookup"><span data-stu-id="d8b92-109">The HTML Editor includes options for changing font size, selecting a font, changing background color, modifying the foreground color, adding links, adding images, changing text alignment, and performing cut, copy, and paste operations (see Figure 1).</span></span>

<span data-ttu-id="d8b92-110">[![HTML エディタ](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d8b92-110">[![The HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="d8b92-111">**図 01**: HTML エディタ ([フルサイズの画像を表示する をクリック](how-do-i-use-the-html-editor-control-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="d8b92-111">**Figure 01**: The HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image2.png))</span></span>

<span data-ttu-id="d8b92-112">HTML エディタを使用すると、デザイン モードを使用してコンテンツを入力したり、HTML を直接入力したりできます。</span><span class="sxs-lookup"><span data-stu-id="d8b92-112">The HTML editor enables you to enter content using a design mode or you can enter HTML directly.</span></span> <span data-ttu-id="d8b92-113">HTML コンテンツをプレビューするオプションも提供されています (図 2 参照)。</span><span class="sxs-lookup"><span data-stu-id="d8b92-113">You also are provided with the option to preview your HTML content (see Figure 2).</span></span>

<span data-ttu-id="d8b92-114">[![デザイン、HTML、プレビューボタン](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d8b92-114">[![Design, HTML, and Preview buttons](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)</span></span>

<span data-ttu-id="d8b92-115">**図 02**: デザイン、HTML、およびプレビュー ボタン ([フルサイズの画像を表示する をクリック](how-do-i-use-the-html-editor-control-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="d8b92-115">**Figure 02**: Design, HTML, and Preview buttons([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image4.png))</span></span>

<span data-ttu-id="d8b92-116">このチュートリアルでは、HTML エディターを表示する方法、HTML エディターに表示されるツール バー ボタンをカスタマイズする方法、およびクロスサイト スクリプティング攻撃を回避する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d8b92-116">In this tutorial, you learn how to display the HTML Editor, how to customize the toolbar buttons that appear in the HTML Editor, and how to avoid Cross-Site Scripting Attacks.</span></span>

## <a name="displaying-the-html-editor"></a><span data-ttu-id="d8b92-117">HTML エディタの表示</span><span class="sxs-lookup"><span data-stu-id="d8b92-117">Displaying the HTML Editor</span></span>

<span data-ttu-id="d8b92-118">ASP.NETページで HTML エディタを使用する前に、まず ScriptManager コントロールをページに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d8b92-118">Before you can use the HTML Editor in an ASP.NET page, you must first add a ScriptManager control to the page.</span></span> <span data-ttu-id="d8b92-119">コントロールは、Visual Studio/Visual Web 開発者エクスプレス ツールボックスの [AJAX 拡張機能] タブの下にあります。</span><span class="sxs-lookup"><span data-stu-id="d8b92-119">The ScriptManager control is located beneath the AJAX Extensions tab in the Visual Studio/Visual Web Developer Express toolbox.</span></span>

<span data-ttu-id="d8b92-120">ページ上の他のコントロールの前に、ページの上部に ScriptManager コントロールを配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d8b92-120">You should place the ScriptManager control at the top of the page before any other controls on the page.</span></span> <span data-ttu-id="d8b92-121">たとえば、開いているサーバー側&lt;フォーム&gt;タグのすぐ下に配置できます。</span><span class="sxs-lookup"><span data-stu-id="d8b92-121">For example, you can place it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="d8b92-122">HTML エディター コントロールは、ツールボックスに AJAX コントロール ツールキット コントロールの残りの部分があります。</span><span class="sxs-lookup"><span data-stu-id="d8b92-122">The HTML Editor control is located in the toolbox with the rest of the AJAX Control Toolkit controls.</span></span> <span data-ttu-id="d8b92-123">Editor コントロールと呼ばれます (図 3 参照)。</span><span class="sxs-lookup"><span data-stu-id="d8b92-123">It is named the Editor control (see Figure 3).</span></span>

<span data-ttu-id="d8b92-124">[![HTML エディター コントロール](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="d8b92-124">[![The HTML Editor control](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)</span></span>

<span data-ttu-id="d8b92-125">**図 03**: HTML エディタ コントロール ([フルサイズの画像を表示する をクリック](how-do-i-use-the-html-editor-control-vb/_static/image6.png)します )</span><span class="sxs-lookup"><span data-stu-id="d8b92-125">**Figure 03**: The HTML Editor control([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image6.png))</span></span>

<span data-ttu-id="d8b92-126">HTML エディタをページにドラッグした後、プロパティ シートでプロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="d8b92-126">After you drag the HTML Editor onto a page, you can set its properties in the property sheet.</span></span> <span data-ttu-id="d8b92-127">たとえば、通常は幅と高さのプロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="d8b92-127">For example, you normally want to set the Width and Height properties.</span></span> <span data-ttu-id="d8b92-128">リスト 1 には、HTML エディターを含む ASP.NET ページのソースが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d8b92-128">Listing 1 contains the source for an ASP.NET page that contains an HTML editor.</span></span>

<span data-ttu-id="d8b92-129">**リスト 1 - シンプルエディター.aspx**</span><span class="sxs-lookup"><span data-stu-id="d8b92-129">**Listing 1 - SimpleEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample1.aspx)]

<span data-ttu-id="d8b92-130">リスト 1 のページには、HTML エディター コントロール、ボタン コントロール、およびリテラル コントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d8b92-130">The page in Listing 1 contains an HTML Editor control, a Button control, and a Literal control.</span></span> <span data-ttu-id="d8b92-131">ボタンをクリックすると、HTML エディターの内容が Literal コントロールに表示されます (図 4 を参照)。</span><span class="sxs-lookup"><span data-stu-id="d8b92-131">When you click the button, the contents of the HTML Editor appear in the Literal control (see Figure 4).</span></span>

<span data-ttu-id="d8b92-132">[![HTML エディタを使用したフォームの送信](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="d8b92-132">[![Submitting a form with an HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)</span></span>

<span data-ttu-id="d8b92-133">**図 04**: HTML エディタを使用してフォームを送信する ([フルサイズの画像を表示するには、](how-do-i-use-the-html-editor-control-vb/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="d8b92-133">**Figure 04**: Submitting a form with an HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image8.png))</span></span>

<span data-ttu-id="d8b92-134">HTML エディタのコンテンツ プロパティは、HTML エディタに入力された HTML コンテンツを取得するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="d8b92-134">The HTML Editor Content property is used to retrieve the HTML content entered into the HTML Editor.</span></span> <span data-ttu-id="d8b92-135">この HTML コンテンツには JavaScript が含まれている可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="d8b92-135">Be aware that this HTML content can contain JavaScript.</span></span> <span data-ttu-id="d8b92-136">次のセクションでは、JavaScript インジェクション攻撃を防ぐ方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d8b92-136">In the next section, we discuss how you can prevent JavaScript Injection Attacks.</span></span>

## <a name="customizing-the-html-editor-toolbar"></a><span data-ttu-id="d8b92-137">HTML エディタ ツールバーのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="d8b92-137">Customizing the HTML Editor Toolbar</span></span>

<span data-ttu-id="d8b92-138">エディターに表示するボタンを正確にカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="d8b92-138">You can customize exactly which buttons appear in the editor.</span></span> <span data-ttu-id="d8b92-139">たとえば、HTML タブを削除して、HTML エディターを HTML モードに切り替えないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="d8b92-139">For example, you might want to remove the HTML tab to prevent users from switching the HTML Editor into HTML mode.</span></span> <span data-ttu-id="d8b92-140">または、フォント サイズのドロップダウン リストを削除して、ユーザーがフォーラム メッセージの投稿に過度に大きなテキストを作成できないようにすることができます (図 5 参照)。</span><span class="sxs-lookup"><span data-stu-id="d8b92-140">Or, you might want to remove the font size dropdown list to prevent users from creating overly large text in a forum message post (see Figure 5).</span></span>

<span data-ttu-id="d8b92-141">[![カスタマイズされた HTML エディタ](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="d8b92-141">[![A customized HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)</span></span>

<span data-ttu-id="d8b92-142">**図 05**: カスタマイズされた HTML エディタ ([フルサイズの画像を表示する をクリック](how-do-i-use-the-html-editor-control-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="d8b92-142">**Figure 05**: A customized HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image10.png))</span></span>

<span data-ttu-id="d8b92-143">ツール バーのボタンをカスタマイズするには、基本エディタ クラスから新しい HTML エディタを派生します。</span><span class="sxs-lookup"><span data-stu-id="d8b92-143">You customize the toolbar buttons by deriving a new HTML Editor from the base Editor class.</span></span> <span data-ttu-id="d8b92-144">たとえば、リスト 2 のカスタム エディターには、太字と斜体のツールバー ボタンのみが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d8b92-144">For example, the custom editor in Listing 2 only contains toolbar buttons for bold and italic.</span></span> <span data-ttu-id="d8b92-145">その他のツールバー ボタンはすべて削除されました。</span><span class="sxs-lookup"><span data-stu-id="d8b92-145">All other toolbar buttons have been removed.</span></span> <span data-ttu-id="d8b92-146">さらに、エディタの下部から HTML タブが削除されました (ただし、[デザイン] タブと [プレビュー] タブは表示されません)。</span><span class="sxs-lookup"><span data-stu-id="d8b92-146">Furthermore, the HTML tab has been removed from the bottom of the editor (but the Design and Preview tabs are still there).</span></span>

<span data-ttu-id="d8b92-147">**リスト 2\_- アプリ コード\カスタム エディター.vb**</span><span class="sxs-lookup"><span data-stu-id="d8b92-147">**Listing 2 - App\_Code\CustomEditor.vb**</span></span>

[!code-vb[Main](how-do-i-use-the-html-editor-control-vb/samples/sample2.vb)]

<span data-ttu-id="d8b92-148">クラスが自動的にコンパイルされるように、リスト 2\_のクラスを App Code フォルダーに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d8b92-148">You must add the class in Listing 2 to your App\_Code folder so that the class will be compiled automatically.</span></span> <span data-ttu-id="d8b92-149">アプリ\_コードフォルダがウェブサイトに存在しない場合は、フォルダを追加するだけです。</span><span class="sxs-lookup"><span data-stu-id="d8b92-149">If the App\_Code folder does not exist in your website then you can simply add the folder.</span></span>

<span data-ttu-id="d8b92-150">カスタム エディターを作成した後、通常の HTML エディターを追加するのと同じ方法で、ASP.NETページに追加できます (リスト 3 を参照)。</span><span class="sxs-lookup"><span data-stu-id="d8b92-150">After you create a custom editor, you can add it to an ASP.NET page in the same way as you add the normal HTML Editor (see Listing 3).</span></span>

<span data-ttu-id="d8b92-151">**リスト 3 - カスタムエディター.aspx を表示します。**</span><span class="sxs-lookup"><span data-stu-id="d8b92-151">**Listing 3 - ShowCustomEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a><span data-ttu-id="d8b92-152">クロスサイト スクリプティング (XSS) 攻撃を回避する</span><span class="sxs-lookup"><span data-stu-id="d8b92-152">Avoiding Cross-Site Scripting (XSS) Attacks</span></span>

<span data-ttu-id="d8b92-153">ユーザーからの入力を受け入れ、その入力を Web サイトに再表示すると、Web サイトをクロスサイト スクリプティング (XSS) 攻撃に対して開く可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d8b92-153">Whenever you accept input from a user, and redisplay that input on your website, you potentially open your website to Cross-Site Scripting (XSS) Attacks.</span></span> <span data-ttu-id="d8b92-154">理論的には、悪意のあるハッカーは、入力が再表示されたときに実行されるJavaScriptコードを送信する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d8b92-154">In theory, a malicious hacker could submit JavaScript code that gets executed when the input is redisplayed.</span></span> <span data-ttu-id="d8b92-155">JavaScriptは、ユーザーのパスワードやその他の機密情報を盗むために使用することができます。</span><span class="sxs-lookup"><span data-stu-id="d8b92-155">The JavaScript could be used to steal user passwords or other sensitive information.</span></span>

<span data-ttu-id="d8b92-156">通常、Web ページに表示する前に、ユーザーから取得した入力を HTML エンコードすることで XSS 攻撃を打ち破ることができます。</span><span class="sxs-lookup"><span data-stu-id="d8b92-156">Normally, you can defeat XSS attacks by HTML encoding whatever input you retrieve from a user before displaying it in a web page.</span></span> <span data-ttu-id="d8b92-157">しかし、HTML エディタの出力を HTML エンコードすると、&lt;スクリプト&gt;タグをエンコードするだけでなく、すべての HTML タグもエンコードされます。</span><span class="sxs-lookup"><span data-stu-id="d8b92-157">However, HTML encoding the output of the HTML Editor would not only encode &lt;script&gt; tags, it would also encode all HTML tags.</span></span> <span data-ttu-id="d8b92-158">つまり、フォントの種類、フォント サイズ、背景色などの書式設定がすべて失われます。</span><span class="sxs-lookup"><span data-stu-id="d8b92-158">In other words, you would lose all of the formatting such as the font type, font size, and background color.</span></span>

<span data-ttu-id="d8b92-159">パスワード、クレジット カード番号、社会保障番号などの機密情報をユーザーから収集する場合は、HTML エディタを使用してユーザーから取得したエンコードされていないコンテンツを表示しないでください。</span><span class="sxs-lookup"><span data-stu-id="d8b92-159">If you are collecting sensitive information from your users -- such as passwords, credit-card numbers, and social security numbers - then you should not display un-encoded content that you retrieve from a user with the HTML Editor.</span></span> <span data-ttu-id="d8b92-160">HTML エディタは、HTML コンテンツを再表示しない場合や、信頼できるユーザーが WEB サイトに HTML コンテンツを送信している場合にのみ使用してください。</span><span class="sxs-lookup"><span data-stu-id="d8b92-160">You should use the HTML Editor only in situations in which you are not redisplaying the HTML content, or the HTML content is being submitted to your website by a trusted party.</span></span>

<span data-ttu-id="d8b92-161">たとえば、ブログ アプリケーションを作成しているとします。</span><span class="sxs-lookup"><span data-stu-id="d8b92-161">Imagine, for example, that you are creating a blog application.</span></span> <span data-ttu-id="d8b92-162">このような場合は、ブログの投稿を作成するときに HTML エディターを使用する意味があります。</span><span class="sxs-lookup"><span data-stu-id="d8b92-162">In this situation, it makes sense to use the HTML Editor when composing blog posts.</span></span> <span data-ttu-id="d8b92-163">ブログ投稿を投稿するのはあなただけであり、おそらく、悪意のあるJavaScriptを提出しないように自分を信頼することができます。</span><span class="sxs-lookup"><span data-stu-id="d8b92-163">You are the only one who submits a blog post and, presumably, you can trust yourself not to submit malicious JavaScript.</span></span> <span data-ttu-id="d8b92-164">ただし、匿名ユーザーがコメントを投稿できるようにする場合は、HTML エディタを使用しても意味がありません。</span><span class="sxs-lookup"><span data-stu-id="d8b92-164">However, it does not make sense to use the HTML Editor when allowing anonymous users to post comments.</span></span> <span data-ttu-id="d8b92-165">ユーザーがパスワードなどの機密情報を送信する場合は、特に注意が必要です。</span><span class="sxs-lookup"><span data-stu-id="d8b92-165">You should be especially careful in situations in which users submit sensitive information such as passwords.</span></span> <span data-ttu-id="d8b92-166">悪意のあるユーザーが、パスワードを盗むのに適した JavaScript を含むコメントを投稿する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d8b92-166">Potentially, a malicious user could post a comment that contains the right JavaScript for stealing a password.</span></span>

## <a name="summary"></a><span data-ttu-id="d8b92-167">まとめ</span><span class="sxs-lookup"><span data-stu-id="d8b92-167">Summary</span></span>

<span data-ttu-id="d8b92-168">このチュートリアルでは、AJAX コントロール ツールキットに含まれている HTML エディター コントロールの簡単な概要を提供しました。</span><span class="sxs-lookup"><span data-stu-id="d8b92-168">In this tutorial, you were provided with a brief overview of the HTML Editor control included in the AJAX Control Toolkit.</span></span> <span data-ttu-id="d8b92-169">HTML エディタを使用して、ユーザーからのリッチ コンテンツを受け入れ、コンテンツをサーバーに送信する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="d8b92-169">You learned how to use the HTML Editor to accept rich content from a user and submit the content to the server.</span></span> <span data-ttu-id="d8b92-170">HTML エディタで表示されるツール バー ボタンをカスタマイズする方法についても説明しました。</span><span class="sxs-lookup"><span data-stu-id="d8b92-170">We also discussed how you can customize the toolbar buttons that are displayed by the HTML Editor.</span></span> <span data-ttu-id="d8b92-171">最後に、HTML エディタを使用して悪意のある入力を受け入れるときにクロスサイト スクリプティング攻撃を回避する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="d8b92-171">Finally, you learned how to avoid Cross-Site Scripting Attacks when using the HTML Editor to accept potentially malicious input.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d8b92-172">前へ</span><span class="sxs-lookup"><span data-stu-id="d8b92-172">Previous</span></span>](how-do-i-use-the-html-editor-control-cs.md)
