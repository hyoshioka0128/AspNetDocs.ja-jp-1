---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: Razor 構文を使用した ASP.NET Web プログラミングのC#概要 () |Microsoft Docs
author: Rick-Anderson
description: この章では、Razor 構文を使用した ASP.NET Web ページによるプログラミングの概要について説明します。 ASP.NET は、動的な web pa を実行するための Microsoft のテクノロジです...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: c2f420bb7c2f7d2e31654c20fb9ec7497a30a9f7
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564886"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a><span data-ttu-id="9b4ea-104">Razor 構文を使用した ASP.NET Web プログラミングのC#概要 ()</span><span class="sxs-lookup"><span data-stu-id="9b4ea-104">Introduction to ASP.NET Web Programming Using the Razor Syntax (C#)</span></span>

<span data-ttu-id="9b4ea-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9b4ea-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9b4ea-106">この記事では、Razor 構文を使用した ASP.NET Web ページによるプログラミングの概要について説明します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-106">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax.</span></span> <span data-ttu-id="9b4ea-107">ASP.NET は、web サーバー上で動的 web ページを実行するための Microsoft のテクノロジです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-107">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span> <span data-ttu-id="9b4ea-108">この記事では、プログラミングC#言語の使用に焦点を当てています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-108">This articles focuses on using the C# programming language.</span></span>
> 
> <span data-ttu-id="9b4ea-109">**学習内容**:</span><span class="sxs-lookup"><span data-stu-id="9b4ea-109">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="9b4ea-110">Razor 構文を使用したプログラミング ASP.NET Web ページを開始するための上位8のプログラミングヒントです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-110">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="9b4ea-111">基本的なプログラミング概念が必要です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-111">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="9b4ea-112">ASP.NET のサーバーコードと Razor 構文について説明します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-112">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="9b4ea-113">ソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="9b4ea-113">Software versions</span></span>
> 
> 
> - <span data-ttu-id="9b4ea-114">ASP.NET Web ページ (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="9b4ea-114">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="9b4ea-115">このチュートリアルは ASP.NET Web ページ2でも動作します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-115">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="9b4ea-116">上位8のプログラミングヒント</span><span class="sxs-lookup"><span data-stu-id="9b4ea-116">The Top 8 Programming Tips</span></span>

<span data-ttu-id="9b4ea-117">このセクションでは、Razor 構文を使用して ASP.NET サーバーコードの記述を開始するときに理解しておく必要があるいくつかのヒントを示します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-117">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="9b4ea-118">Razor 構文はC#プログラミング言語に基づいており、ASP.NET Web ページで最も頻繁に使用される言語です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-118">The Razor syntax is based on the C# programming language, and that's the language that's used most often with ASP.NET Web Pages.</span></span> <span data-ttu-id="9b4ea-119">ただし、Razor 構文は Visual Basic の言語をサポートしています。また、Visual Basic でも実行できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-119">However, the Razor syntax also supports the Visual Basic language, and everything you see you can also do in Visual Basic.</span></span> <span data-ttu-id="9b4ea-120">詳細については、付録[Visual Basic の言語と構文](https://go.microsoft.com/fwlink/?LinkId=202908)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-120">For details, see the appendix [Visual Basic Language and Syntax](https://go.microsoft.com/fwlink/?LinkId=202908).</span></span>

<span data-ttu-id="9b4ea-121">これらのプログラミング手法のほとんどの詳細については、この記事の後半で説明します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-121">You can find more details about most of these programming techniques later in the article.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="9b4ea-122">1. @ 文字を使用してコードをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-122">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="9b4ea-123">`@` 文字は、インライン式、単一のステートメントブロック、および複数ステートメントのブロックを開始します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-123">The `@` character starts inline expressions, single statement blocks, and multi-statement blocks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

<span data-ttu-id="9b4ea-124">ブラウザーでページを実行すると、次のようなステートメントが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-124">This is what these statements look like when the page runs in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="9b4ea-126">**HTML エンコード**</span><span class="sxs-lookup"><span data-stu-id="9b4ea-126">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="9b4ea-127">前の例のように `@` 文字を使用してページにコンテンツを表示すると、ASP.NET は出力を HTML エンコードします。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-127">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="9b4ea-128">これにより、予約された HTML 文字 (`<`、`>` や `&`など) が、HTML タグまたはエンティティとして解釈されるのではなく、web ページに文字として表示されるようにするコードに置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-128">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="9b4ea-129">HTML エンコードを使用しないと、サーバーコードからの出力が正しく表示されず、ページがセキュリティ上のリスクにさらされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-129">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="9b4ea-130">タグをマークアップとしてレンダリングする HTML マークアップを出力することが目的である場合 (たとえば、段落や `<em></em>` テキストを強調するための `<p></p>`)、この記事で後述する「[コードブロック内のテキスト、マークアップ、およびコードの結合](#BM_CombiningTextMarkupAndCode)」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-130">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="9b4ea-131">HTML エンコードの詳細については、「[フォームの操作](https://go.microsoft.com/fwlink/?LinkId=202892)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-131">You can read more about HTML encoding in [Working with Forms](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-in-braces"></a><span data-ttu-id="9b4ea-132">2. コードブロックを中かっこで囲みます</span><span class="sxs-lookup"><span data-stu-id="9b4ea-132">2. You enclose code blocks in braces</span></span>

<span data-ttu-id="9b4ea-133">*コードブロック*には、1つまたは複数のコードステートメントが含まれ、中かっこで囲まれています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-133">A *code block* includes one or more code statements and is enclosed in braces.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

<span data-ttu-id="9b4ea-134">結果がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-134">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a><span data-ttu-id="9b4ea-136">3. ブロック内では、各コードステートメントをセミコロンで終了します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-136">3. Inside a block, you end each code statement with a semicolon</span></span>

<span data-ttu-id="9b4ea-137">コードブロック内では、すべての完全なコードステートメントはセミコロンで終わる必要があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-137">Inside a code block, each complete code statement must end with a semicolon.</span></span> <span data-ttu-id="9b4ea-138">インライン式はセミコロンで終了しません。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-138">Inline expressions don't end with a semicolon.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="9b4ea-139">4. 変数を使用して値を格納する</span><span class="sxs-lookup"><span data-stu-id="9b4ea-139">4. You use variables to store values</span></span>

<span data-ttu-id="9b4ea-140">文字列、数値、日付など、*変数*に値を格納することができます。新しい変数を作成するには、`var` キーワードを使用します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-140">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `var` keyword.</span></span> <span data-ttu-id="9b4ea-141">`@`を使用して、変数の値をページに直接挿入できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-141">You can insert variable values directly in a page using `@`.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

<span data-ttu-id="9b4ea-142">結果がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-142">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="9b4ea-144">5. リテラル文字列値を二重引用符で囲みます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-144">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="9b4ea-145">*文字列*は、テキストとして扱われる文字のシーケンスです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-145">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="9b4ea-146">文字列を指定するには、次のように二重引用符で囲みます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-146">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

<span data-ttu-id="9b4ea-147">表示する文字列に円記号 (`\`) または二重引用符 (`"`) が含まれている場合は、`@` 演算子を先頭に付けた*逐語的文字列リテラル*を使用します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-147">If the string that you want to display contains a backslash character ( `\` ) or double quotation marks ( `"` ), use a *verbatim string literal* that's prefixed with the `@` operator.</span></span> <span data-ttu-id="9b4ea-148">(でC#は、逐語的文字列リテラルを使用しない限り、\ 文字は特別な意味を持ちます)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-148">(In C#, the \ character has special meaning unless you use a verbatim string literal.)</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

<span data-ttu-id="9b4ea-149">二重引用符を埋め込むには、逐語的文字列リテラルを使用して、引用符を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-149">To embed double quotation marks, use a verbatim string literal and repeat the quotation marks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

<span data-ttu-id="9b4ea-150">ページで両方の例を使用した結果を次に示します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-150">Here's the result of using both of these examples in a page:</span></span>

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> <span data-ttu-id="9b4ea-152">`@` 文字が、でC#逐語的文字列リテラルをマークし、ASP.NET ページのコードをマークするために使用されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-152">Notice that the `@` character is used both to mark verbatim string literals in C# and to mark code in ASP.NET pages.</span></span>

### <a name="6-code-is-case-sensitive"></a><span data-ttu-id="9b4ea-153">6. コードで大文字と小文字を区別する</span><span class="sxs-lookup"><span data-stu-id="9b4ea-153">6. Code is case sensitive</span></span>

<span data-ttu-id="9b4ea-154">でC#は、キーワード (`var`、`true`、`if`など) と変数名は大文字と小文字が区別されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-154">In C#, keywords (like `var`, `true`, and `if`) and variable names are case sensitive.</span></span> <span data-ttu-id="9b4ea-155">次のコード行では、`lastName` と `LastName.` の2つの異なる変数を作成しています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-155">The following lines of code create two different variables, `lastName` and `LastName.`</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

<span data-ttu-id="9b4ea-156">変数を `var lastName = "Smith";` として宣言し、その変数を `@LastName`としてページ内で参照しようとすると、`"Smith"`ではなく `"Jones"` 値が取得されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-156">If you declare a variable as `var lastName = "Smith";` and try to reference that variable in your page as `@LastName`, you would get the value `"Jones"` instead of `"Smith"`.</span></span>

> [!NOTE]
> <span data-ttu-id="9b4ea-157">Visual Basic では、キーワードと変数の大文字と小文字は区別され*ません*。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-157">In Visual Basic, keywords and variables are *not* case sensitive.</span></span>

### <a name="7-much-of-your-coding-involves-objects"></a><span data-ttu-id="9b4ea-158">7. コーディングの多くがオブジェクトを含む</span><span class="sxs-lookup"><span data-stu-id="9b4ea-158">7. Much of your coding involves objects</span></span>

<span data-ttu-id="9b4ea-159">*オブジェクト*は、ページ、テキストボックス、ファイル、 &#8212;画像、web 要求、電子メールメッセージ、顧客レコード (データベース行) などを使用してプログラミングできることを表します。オブジェクトには、その特性を説明するプロパティがあります。 &#8212;また、テキストボックスオブジェクトの読み取りまたは変更には、`Text` プロパティがあります。また、要求オブジェクトには `Url` プロパティがあり、電子メールメッセージには `From` プロパティがあり、顧客オブジェクトには `FirstName` プロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-159">An *object* represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics and that you can read or change &#8212; a text box object has a `Text` property (among others), a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="9b4ea-160">オブジェクトには、実行できる&quot; &quot;動詞であるメソッドもあります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-160">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="9b4ea-161">例としては、ファイルオブジェクトの `Save` メソッド、イメージオブジェクトの `Rotate` メソッド、電子メールオブジェクトの `Send` メソッドなどがあります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-161">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="9b4ea-162">多くの場合、`Request` オブジェクトを使用します。このオブジェクトは、ページ上のテキストボックス (フォームフィールド) の値、要求を行ったブラウザーの種類、ページの URL、ユーザー id などの情報を提供します。次の例は、`Request` オブジェクトのプロパティにアクセスする方法と、`Request` オブジェクトの `MapPath` メソッドを呼び出す方法を示しています。これにより、サーバー上のページの絶対パスが得られます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-162">You'll often work with the `Request` object, which gives you information like the values of text boxes (form fields) on the page, what type of browser made the request, the URL of the page, the user identity, etc. The following example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

<span data-ttu-id="9b4ea-163">結果がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-163">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="9b4ea-165">8. 決定を行うコードを記述できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-165">8. You can write code that makes decisions</span></span>

<span data-ttu-id="9b4ea-166">動的 web ページの重要な機能は、条件に基づいて何を行うかを決定できることです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-166">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="9b4ea-167">これを行う最も一般的な方法は、`if` ステートメント (および省略可能な `else` ステートメント) を使用することです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-167">The most common way to do this is with the `if` statement (and optional `else` statement).</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

<span data-ttu-id="9b4ea-168">ステートメント `if(IsPost)` は、`if(IsPost == true)`を簡単に記述する方法です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-168">The statement `if(IsPost)` is a shorthand way of writing `if(IsPost == true)`.</span></span> <span data-ttu-id="9b4ea-169">`if` ステートメントと共に、条件のテスト、コードブロックの繰り返しなど、さまざまな方法があります。これについては、この記事の後半で説明します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-169">Along with `if` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="9b4ea-170">ブラウザーに表示される結果 ( **[送信]** をクリックした後):</span><span class="sxs-lookup"><span data-stu-id="9b4ea-170">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a><span data-ttu-id="9b4ea-172">HTTP GET メソッドと POST メソッド、および IsPost プロパティ</span><span class="sxs-lookup"><span data-stu-id="9b4ea-172">HTTP GET and POST Methods and the IsPost Property</span></span>
> 
> <span data-ttu-id="9b4ea-173">Web ページ (HTTP) に使用されるプロトコルでは、サーバーへの要求を行うために使用されるメソッド (動詞) の数が制限されています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-173">The protocol used for web pages (HTTP) supports a very limited number of methods (verbs) that are used to make requests to the server.</span></span> <span data-ttu-id="9b4ea-174">最も一般的な2つの方法は、ページの読み取りに使用される GET と、ページの送信に使用される POST です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-174">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="9b4ea-175">一般に、ユーザーが初めてページを要求したときは、GET を使用してページが要求されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-175">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="9b4ea-176">ユーザーがフォームに入力し、[送信] ボタンをクリックすると、ブラウザーはサーバーに POST 要求を行います。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-176">If the user fills in a form and then clicks a submit button, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="9b4ea-177">Web プログラミングでは、ページの処理方法を把握できるように、ページが GET として要求されているのか、または投稿として要求されているのかを知ることが役に立つことがよくあります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-177">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="9b4ea-178">ASP.NET Web ページでは、`IsPost` プロパティを使用して、要求が GET または POST のどちらであるかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-178">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="9b4ea-179">要求が POST の場合、`IsPost` プロパティは true を返し、フォームのテキストボックスの値を読み取るなどの操作を実行できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-179">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="9b4ea-180">多くの例では、`IsPost`の値に応じて、ページを異なる方法で処理する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-180">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="9b4ea-181">単純なコード例</span><span class="sxs-lookup"><span data-stu-id="9b4ea-181">A Simple Code Example</span></span>

<span data-ttu-id="9b4ea-182">この手順では、基本的なプログラミング手法を示すページを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-182">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="9b4ea-183">この例では、ユーザーが2つの数値を入力できるページを作成し、それらを追加して結果を表示します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-183">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="9b4ea-184">エディターで、新しいファイルを作成し、「 *Addnumbers. cshtml*」という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-184">In your editor, create a new file and name it *AddNumbers.cshtml*.</span></span>
2. <span data-ttu-id="9b4ea-185">次のコードとマークアップをページにコピーして、ページに既に存在するものを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-185">Copy the following code and markup into the page, replacing anything already in the page.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    <span data-ttu-id="9b4ea-186">ここでは、次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-186">Here are some things for you to note:</span></span>

    - <span data-ttu-id="9b4ea-187">`@` 文字は、ページ内の最初のコードブロックを開始し、ページの下部付近に埋め込まれている `totalMessage` 変数の前にあります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-187">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable that's embedded near the bottom of the page.</span></span>
    - <span data-ttu-id="9b4ea-188">ページの上部にあるブロックは、中かっこで囲まれています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-188">The block at the top of the page is enclosed in braces.</span></span>
    - <span data-ttu-id="9b4ea-189">先頭のブロックでは、すべての行の末尾にセミコロンが付きます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-189">In the block at the top, all lines end with a semicolon.</span></span>
    - <span data-ttu-id="9b4ea-190">変数 `total`、`num1`、`num2`、および `totalMessage` には、いくつかの数値と文字列が格納されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="9b4ea-191">`totalMessage` 変数に代入されたリテラル文字列値は、二重引用符で囲まれています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="9b4ea-192">コードでは大文字と小文字が区別されるため、`totalMessage` 変数がページの下部付近で使用されている場合、その名前は一番上の変数と正確に一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-192">Because the code is case-sensitive, when the `totalMessage` variable is used near the bottom of the page, its name must match the variable at the top exactly.</span></span>
    - <span data-ttu-id="9b4ea-193">式 `num1.AsInt() + num2.AsInt()` は、オブジェクトとメソッドを操作する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-193">The expression `num1.AsInt() + num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="9b4ea-194">各変数の `AsInt` メソッドは、ユーザーが入力した文字列を数値 (整数) に変換して、算術演算を実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-194">The `AsInt` method on each variable converts the string entered by a user to a number (an integer) so that you can perform arithmetic on it.</span></span>
    - <span data-ttu-id="9b4ea-195">`<form>` タグには、`method="post"` 属性が含まれています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-195">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="9b4ea-196">これにより、ユーザーが **[追加]** をクリックしたときに、HTTP POST メソッドを使用してページがサーバーに送信されることを指定します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-196">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="9b4ea-197">ページが送信されると、`if(IsPost)` テストが true と評価され、条件コードが実行されて、数値を加算した結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-197">When the page is submitted, the `if(IsPost)` test evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="9b4ea-198">ページを保存し、ブラウザーで実行します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-198">Save the page and run it in a browser.</span></span> <span data-ttu-id="9b4ea-199">(実行する前に、 **[ファイル]** ワークスペースでページが選択されていることを確認してください)。2つの整数を入力し、 **[追加]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-199">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span> 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a><span data-ttu-id="9b4ea-201">基本的なプログラミングの概念</span><span class="sxs-lookup"><span data-stu-id="9b4ea-201">Basic Programming Concepts</span></span>

<span data-ttu-id="9b4ea-202">この記事では、ASP.NET web プログラミングの概要について説明します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-202">This article provides you with an overview of ASP.NET web programming.</span></span> <span data-ttu-id="9b4ea-203">これは完全な検査ではなく、最も頻繁に使用するプログラミングの概念を簡単に説明します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-203">It isn't an exhaustive examination, just a quick tour through the programming concepts you'll use most often.</span></span> <span data-ttu-id="9b4ea-204">それでも、ASP.NET Web ページの使用を開始するために必要なほとんどすべてのことが説明されています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-204">Even so, it covers almost everything you'll need to get started with ASP.NET Web Pages.</span></span>

<span data-ttu-id="9b4ea-205">しかし、まず少し技術的な背景です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-205">But first, a little technical background.</span></span>

### <a name="the-razor-syntax-server-code-and-aspnet"></a><span data-ttu-id="9b4ea-206">Razor 構文、サーバーコード、および ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9b4ea-206">The Razor Syntax, Server Code, and ASP.NET</span></span>

<span data-ttu-id="9b4ea-207">Razor 構文は、web ページにサーバーベースのコードを埋め込むための単純なプログラミング構文です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-207">Razor syntax is a simple programming syntax for embedding server-based code in a web page.</span></span> <span data-ttu-id="9b4ea-208">Razor 構文を使用する web ページでは、クライアントコンテンツとサーバーコードという2種類のコンテンツがあります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-208">In a web page that uses the Razor syntax, there are two kinds of content: client content and server code.</span></span> <span data-ttu-id="9b4ea-209">クライアントコンテンツは、HTML マークアップ (要素)、CSS などのスタイル情報、JavaScript などのクライアントスクリプト、プレーンテキストなど、web ページで使用するものです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-209">Client content is the stuff you're used to in web pages: HTML markup (elements), style information such as CSS, maybe some client script such as JavaScript, and plain text.</span></span>

<span data-ttu-id="9b4ea-210">Razor 構文を使用すると、このクライアントコンテンツにサーバーコードを追加できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-210">Razor syntax lets you add server code to this client content.</span></span> <span data-ttu-id="9b4ea-211">ページにサーバーコードがある場合、サーバーはそのコードを最初に実行してから、ブラウザーにページを送信します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-211">If there's server code in the page, the server runs that code first, before it sends the page to the browser.</span></span> <span data-ttu-id="9b4ea-212">サーバー上で実行することにより、このコードでは、サーバーベースのデータベースへのアクセスなど、クライアントコンテンツのみを使用することにより複雑なタスクを実行できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-212">By running on the server, the code can perform tasks that can be a lot more complex to do using client content alone, like accessing server-based databases.</span></span> <span data-ttu-id="9b4ea-213">ほとんどの場合、サーバーコードは動的にクライアント&#8212;コンテンツを作成できます。これにより、HTML マークアップやその他のコンテンツをその場で生成し、そのページに含まれる静的な html と共にブラウザーに送信できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-213">Most importantly, server code can dynamically create client content &#8212; it can generate HTML markup or other content on the fly and then send it to the browser along with any static HTML that the page might contain.</span></span> <span data-ttu-id="9b4ea-214">ブラウザーの観点からは、サーバーコードによって生成されるクライアントコンテンツは、他のクライアントコンテンツと同じではありません。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-214">From the browser's perspective, client content that's generated by your server code is no different than any other client content.</span></span> <span data-ttu-id="9b4ea-215">既に説明したように、必要なサーバーコードは非常に単純です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-215">As you've already seen, the server code that's required is quite simple.</span></span>

<span data-ttu-id="9b4ea-216">Razor 構文を含む web ページの ASP.NET には、特殊なファイル拡張子 (*cshtml*または*vbhtml*) があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-216">ASP.NET web pages that include the Razor syntax have a special file extension (*.cshtml* or *.vbhtml*).</span></span> <span data-ttu-id="9b4ea-217">サーバーはこれらの拡張機能を認識し、Razor 構文でマークされているコードを実行してから、ブラウザーにページを送信します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-217">The server recognizes these extensions, runs the code that's marked with Razor syntax, and then sends the page to the browser.</span></span>

### <a name="where-does-aspnet-fit-in"></a><span data-ttu-id="9b4ea-218">ASP.NET はどこにありますか。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-218">Where does ASP.NET fit in?</span></span>

<span data-ttu-id="9b4ea-219">Razor 構文は、ASP.NET と呼ばれる Microsoft のテクノロジに基づいています。このテクノロジは、Microsoft .NET フレームワークに基づいています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-219">Razor syntax is based on a technology from Microsoft called ASP.NET, which in turn is based on the Microsoft .NET Framework.</span></span> <span data-ttu-id="9b4ea-220">The.NET Framework は、ほぼすべての種類のコンピューターアプリケーションを開発するための、Microsoft の大きな包括的なプログラミングフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-220">The.NET Framework is a big, comprehensive programming framework from Microsoft for developing virtually any type of computer application.</span></span> <span data-ttu-id="9b4ea-221">ASP.NET は、web アプリケーションの作成専用に設計された .NET Framework の一部です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-221">ASP.NET is the part of the .NET Framework that's specifically designed for creating web applications.</span></span> <span data-ttu-id="9b4ea-222">開発者は ASP.NET を使用して、世界中の最大規模で最大規模の web サイトを作成しました。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-222">Developers have used ASP.NET to create many of the largest and highest-traffic websites in the world.</span></span> <span data-ttu-id="9b4ea-223">(サイトの URL の一部としてファイル名拡張子 *.aspx*が表示されると、サイトが ASP.NET を使用して書き込まれたことがわかります)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-223">(Any time you see the file-name extension *.aspx* as part of the URL in a site, you'll know that the site was written using ASP.NET.)</span></span>

<span data-ttu-id="9b4ea-224">Razor 構文は、ASP.NET のすべての機能を提供しますが、初心者であり、専門家の方が生産性を向上させる簡単な構文を使用します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-224">The Razor syntax gives you all the power of ASP.NET, but using a simplified syntax that's easier to learn if you're a beginner and that makes you more productive if you're an expert.</span></span> <span data-ttu-id="9b4ea-225">この構文は簡単に使用できますが、ASP.NET と .NET Framework との家族の関係は、web サイトがより高度なものになったときに、より大きなフレームワークの機能を利用できることを意味します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-225">Even though this syntax is simple to use, its family relationship to ASP.NET and the .NET Framework means that as your websites become more sophisticated, you have the power of the larger frameworks available to you.</span></span>

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> <span data-ttu-id="9b4ea-227">**クラスとインスタンス**</span><span class="sxs-lookup"><span data-stu-id="9b4ea-227">**Classes and Instances**</span></span>
> 
> <span data-ttu-id="9b4ea-228">ASP.NET サーバーコードは、クラスの概念に基づいて構築されたオブジェクトを使用します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-228">ASP.NET server code uses objects, which are in turn built on the idea of classes.</span></span> <span data-ttu-id="9b4ea-229">クラスは、オブジェクトの定義またはテンプレートです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-229">The class is the definition or template for an object.</span></span> <span data-ttu-id="9b4ea-230">たとえば、アプリケーションには、顧客オブジェクトが必要とするプロパティとメソッドを定義する `Customer` クラスが含まれている場合があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-230">For example, an application might contain a `Customer` class that defines the properties and methods that any customer object needs.</span></span>
> 
> <span data-ttu-id="9b4ea-231">アプリケーションが実際の顧客情報を処理する必要がある場合は、customer オブジェクトのインスタンス *(または*インスタンス) を作成します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-231">When the application needs to work with actual customer information, it creates an instance of (or *instantiates*) a customer object.</span></span> <span data-ttu-id="9b4ea-232">個々の顧客は、`Customer` クラスの個別のインスタンスです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-232">Each individual customer is a separate instance of the `Customer` class.</span></span> <span data-ttu-id="9b4ea-233">すべてのインスタンスは同じプロパティとメソッドをサポートしますが、各顧客オブジェクトが一意であるため、各インスタンスのプロパティ値は通常異なります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-233">Every instance supports the same properties and methods, but the property values for each instance are typically different, because each customer object is unique.</span></span> <span data-ttu-id="9b4ea-234">1つの customer オブジェクトでは、`LastName` プロパティが "Smith" である場合があります。別の customer オブジェクトでは、`LastName` プロパティが "Jones" である場合があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-234">In one customer object, the `LastName` property might be "Smith"; in another customer object, the `LastName` property might be "Jones."</span></span>
> 
> <span data-ttu-id="9b4ea-235">同様に、サイト内の個々の web ページは、`Page` クラスのインスタンスである `Page` オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-235">Similarly, any individual web page in your site is a `Page` object that's an instance of the `Page` class.</span></span> <span data-ttu-id="9b4ea-236">ページ上のボタンは、`Button` クラスのインスタンスである `Button` のオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-236">A button on the page is a `Button` object that is an instance of the `Button` class, and so on.</span></span> <span data-ttu-id="9b4ea-237">各インスタンスには独自の特性がありますが、これらはすべて、オブジェクトのクラス定義で指定されている内容に基づいています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-237">Each instance has its own characteristics, but they all are based on what's specified in the object's class definition.</span></span>

## <a name="basic-syntax"></a><span data-ttu-id="9b4ea-238">基本構文</span><span class="sxs-lookup"><span data-stu-id="9b4ea-238">Basic Syntax</span></span>

<span data-ttu-id="9b4ea-239">前に、ASP.NET Web ページページを作成する方法の基本的な例と、HTML マークアップにサーバーコードを追加する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-239">Earlier you saw a basic example of how to create an ASP.NET Web Pages page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="9b4ea-240">ここでは、プログラミング言語の規則である Razor 構文&#8212;を使用して、ASP.NET サーバーコードを記述する方法の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-240">Here you'll learn the basics of writing ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="9b4ea-241">プログラミングの経験がある場合 (特に、C、 C++、 C#、Visual Basic、または JavaScript を使用している場合)、この記事で読まれている内容の多くは理解しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-241">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="9b4ea-242">場合によっては、ファイル内のマークアップにサーバーコードを追加する方法についてのみ理解しておく必要が*あります。*</span><span class="sxs-lookup"><span data-stu-id="9b4ea-242">You'll probably need to familiarize yourself only with how server code is added to markup in *.cshtml* files.</span></span>

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a><span data-ttu-id="9b4ea-243">コードブロック内のテキスト、マークアップ、およびコードの結合</span><span class="sxs-lookup"><span data-stu-id="9b4ea-243">Combining Text, Markup, and Code in Code Blocks</span></span>

<span data-ttu-id="9b4ea-244">サーバーコードブロックでは、多くの場合、テキストまたはマークアップ (またはその両方) をページに出力します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-244">In server code blocks, you often want to output text or markup (or both) to the page.</span></span> <span data-ttu-id="9b4ea-245">サーバーコードブロックにコード以外のテキストが含まれていて、そのテキストをそのように表示する必要がある場合、ASP.NET はそのテキストをコードから区別できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-245">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="9b4ea-246">これにはいくつかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-246">There are several ways to do this.</span></span>

- <span data-ttu-id="9b4ea-247">テキストを `<p></p>` や `<em></em>`などの HTML 要素で囲みます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-247">Enclose the text in an HTML element like `<p></p>` or `<em></em>`:</span></span>   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    <span data-ttu-id="9b4ea-248">HTML 要素には、テキスト、追加の HTML 要素、およびサーバーコード式を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-248">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="9b4ea-249">ASP.NET が HTML の開始タグ (`<p>`など) を参照すると、要素とそのコンテンツを含むすべてのものがブラウザーに表示されます。これにより、サーバーコード式が解決されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-249">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything including the element and its content as is to the browser, resolving server-code expressions as it goes.</span></span>
- <span data-ttu-id="9b4ea-250">`@:` 演算子または `<text>` 要素を使用します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-250">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="9b4ea-251">`@:` は、プレーンテキストまたは一致しない HTML タグを含む1行のコンテンツを出力します。`<text>` 要素は、出力に複数の行を囲みます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-251">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="9b4ea-252">これらのオプションは、HTML 要素を出力の一部としてレンダリングしない場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-252">These options are useful when you don't want to render an HTML element as part of the output.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    <span data-ttu-id="9b4ea-253">複数行のテキストまたは一致しない HTML タグを出力する場合は、各行の前に `@:`を挿入するか、`<text>` 要素でその行を囲むことができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-253">If you want to output multiple lines of text or unmatched HTML tags, you can precede each line with `@:`, or you can enclose the line in a `<text>` element.</span></span> <span data-ttu-id="9b4ea-254">`@:` 演算子と同様、`<text>` タグはテキストコンテンツを識別するために ASP.NET によって使用され、ページ出力には表示されません。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-254">Like the `@:` operator,`<text>` tags are used by ASP.NET to identify text content and are never rendered in the page output.</span></span>

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    <span data-ttu-id="9b4ea-255">最初の例では、前の例を繰り返しますが、1組の `<text>` タグを使用して、レンダリングするテキストを囲みます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-255">The first example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span> <span data-ttu-id="9b4ea-256">2番目の例では、`<text>` タグと `</text>` タグは3つの行を囲みます。これらの行には、非包含テキストと一致しない HTML タグ (`<br />`) と、サーバーコードおよび一致した HTML タグがあります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-256">In the second example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="9b4ea-257">繰り返しになりますが、各行の前に `@:` 演算子を使用することもできます。どちらの方法でも動作します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-257">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b4ea-258">HTML 要素を使用して、このセクション&#8212;に示すようにテキストを出力する場合、`@:` 演算子、 &#8212;または `<text>` 要素 ASP.NET は、出力を html エンコードしません。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-258">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="9b4ea-259">(前述のように、ASP.NET は、このセクションに記載されている特殊なケースを除き、`@`の前にあるサーバーコード式とサーバーコードブロックの出力をエンコードします)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-259">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="9b4ea-260">Whitespace</span><span class="sxs-lookup"><span data-stu-id="9b4ea-260">Whitespace</span></span>

<span data-ttu-id="9b4ea-261">ステートメント内の余分なスペース (および文字列リテラルの外部) は、ステートメントに影響しません。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-261">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

<span data-ttu-id="9b4ea-262">ステートメント内の改行は、ステートメントには影響しません。また、ステートメントをラップして読みやすくすることもできます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-262">A line break in a statement has no effect on the statement, and you can wrap statements for readability.</span></span> <span data-ttu-id="9b4ea-263">次の 2 つのステートメントでは同じ結果が得られます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-263">The following statements are the same:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

<span data-ttu-id="9b4ea-264">ただし、文字列リテラルの途中では、行をラップすることはできません。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-264">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="9b4ea-265">次の例は機能しません。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-265">The following example doesn't work:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

<span data-ttu-id="9b4ea-266">上のコードのように、折り返される長い文字列を複数の行に結合するには、2つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-266">To combine a long string that wraps to multiple lines like the above code, there are two options.</span></span> <span data-ttu-id="9b4ea-267">連結演算子 (`+`) を使用できます。これについては、この記事の後半で説明します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-267">You can use the concatenation operator (`+`), which you'll see later in this article.</span></span> <span data-ttu-id="9b4ea-268">この記事で既に説明したように、`@` 文字を使用して逐語的文字列リテラルを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-268">You can also use the `@` character to create a verbatim string literal, as you saw earlier in this article.</span></span> <span data-ttu-id="9b4ea-269">逐語的文字列リテラルは、次のように行を越えて分割できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-269">You can break verbatim string literals across lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a><span data-ttu-id="9b4ea-270">コード (およびマークアップ) のコメント</span><span class="sxs-lookup"><span data-stu-id="9b4ea-270">Code (and Markup) Comments</span></span>

<span data-ttu-id="9b4ea-271">コメントを使用すると、自分や他のユーザーにメモを残すことができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-271">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="9b4ea-272">また、実行するのではなく、ページ内に保持する必要のあるコードまたはマークアップを無効 (*コメントアウト*) することもできます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-272">They also allow you to disable (*comment out*) a section of code or markup that you don't want to run but want to keep in your page for the time being.</span></span>

<span data-ttu-id="9b4ea-273">Razor コードと HTML マークアップには、それぞれ異なるコメント構文があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-273">There's different commenting syntax for Razor code and for HTML markup.</span></span> <span data-ttu-id="9b4ea-274">すべての Razor コードと同様に、ページがブラウザーに送信される前に、Razor コメントがサーバー上で処理され、削除されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-274">As with all Razor code, Razor comments are processed (and then removed) on the server before the page is sent to the browser.</span></span> <span data-ttu-id="9b4ea-275">したがって、Razor コメントの構文を使用すると、ファイルを編集するときに表示できるコメントをコード (またはマークアップにも) に含めることができますが、ユーザーにはページソース内であっても表示されません。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-275">Therefore, the Razor commenting syntax lets you put comments into the code (or even into the markup) that you can see when you edit the file, but that users don't see, even in the page source.</span></span>

<span data-ttu-id="9b4ea-276">ASP.NET Razor コメントの場合は、`@*` でコメントを開始し、`*@`で終了します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-276">For ASP.NET Razor comments, you start the comment with `@*` and end it with `*@`.</span></span> <span data-ttu-id="9b4ea-277">コメントは、1行または複数行にすることができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-277">The comment can be on one line or multiple lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

<span data-ttu-id="9b4ea-278">コードブロック内のコメントは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-278">Here is a comment within a code block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

<span data-ttu-id="9b4ea-279">次に示すのは、コードの行をコメントアウトして実行しないようにするコードのブロックです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-279">Here is the same block of code, with the line of code commented out so that it won't run:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

<span data-ttu-id="9b4ea-280">コードブロック内では、Razor コメント構文を使用する代わりに、使用しているプログラミング言語のコメント構文を使用できC#ます。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-280">Inside a code block, as an alternative to using Razor comment syntax, you can use the commenting syntax of the programming language you're using, such as C#:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

<span data-ttu-id="9b4ea-281">でC#は、単一行のコメントの前に `//` 文字が付きます。複数行のコメントは `/*` で始まり、`*/`で終わります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-281">In C#, single-line comments are preceded by the `//` characters, and multi-line comments begin with `/*` and end with `*/`.</span></span> <span data-ttu-id="9b4ea-282">(Razor コメントの場合とC#同様に、コメントはブラウザーに表示されません)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-282">(As with Razor comments, C# comments are not rendered to the browser.)</span></span>

<span data-ttu-id="9b4ea-283">ご存知のように、マークアップでは、HTML コメントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-283">For markup, as you probably know, you can create an HTML comment:</span></span>

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

<span data-ttu-id="9b4ea-284">HTML コメントは `<!--` 文字で始まり `-->`で終わります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-284">HTML comments start with `<!--` characters and end with `-->`.</span></span> <span data-ttu-id="9b4ea-285">HTML コメントを使用すると、テキストだけでなく、ページに保持してもレンダリングしたくない HTML マークアップを囲むことができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-285">You can use HTML comments to surround not only text, but also any HTML markup that you may want to keep in the page but don't want to render.</span></span> <span data-ttu-id="9b4ea-286">この HTML コメントは、タグの内容全体と、タグに含まれるテキストを非表示にします。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-286">This HTML comment will hide the entire content of the tags and the text they contain:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

<span data-ttu-id="9b4ea-287">Razor コメントとは異なり、HTML コメントはページに表示*され*、ユーザーはページソースを表示して表示できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-287">Unlike Razor comments, HTML comments *are* rendered to the page and the user can see them by viewing the page source.</span></span>

<span data-ttu-id="9b4ea-288">Razor には、のC#入れ子になったブロックに関する制限があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-288">Razor has limitations on nested blocks of C#.</span></span> <span data-ttu-id="9b4ea-289">詳細について[はC# 、「名前付き変数と入れ子になったブロックの生成](http://aspnetwebstack.codeplex.com/workitem/1914)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-289">For more information see [Named C# Variables and Nested Blocks Generate Broken Code](http://aspnetwebstack.codeplex.com/workitem/1914)</span></span>

## <a name="variables"></a><span data-ttu-id="9b4ea-290">［変数］</span><span class="sxs-lookup"><span data-stu-id="9b4ea-290">Variables</span></span>

<span data-ttu-id="9b4ea-291">変数は、データを格納するために使用する名前付きオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-291">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="9b4ea-292">変数には任意の名前を指定できますが、名前の先頭には英字を使用する必要があり、空白や予約文字を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-292">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="9b4ea-293">変数とデータ型</span><span class="sxs-lookup"><span data-stu-id="9b4ea-293">Variables and Data Types</span></span>

<span data-ttu-id="9b4ea-294">変数には、変数に格納されているデータの種類を示す特定のデータ型を指定できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-294">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="9b4ea-295">文字列値 (&quot;Hello world&quot;など) を格納する文字列変数、整数値 (3 や79など) を格納する整数変数、および日付値をさまざまな形式で格納する日付変数 (4/12/2012 や2009など) を指定できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-295">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="9b4ea-296">他にもさまざまなデータ型を使用できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-296">And there are many other data types you can use.</span></span>

<span data-ttu-id="9b4ea-297">ただし、通常は変数の型を指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-297">However, you generally don't have to specify a type for a variable.</span></span> <span data-ttu-id="9b4ea-298">ほとんどの場合、ASP.NET は変数のデータがどのように使用されているかに基づいて型を特定できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-298">Most of the time, ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="9b4ea-299">(場合によっては、型を指定する必要があります。これが当てはまる例があります)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-299">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="9b4ea-300">変数を宣言するには、`var` キーワードを使用するか (型を指定しない場合)、または型の名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-300">You declare a variable using the `var` keyword (if you don't want to specify a type) or by using the name of the type:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

<span data-ttu-id="9b4ea-301">次の例は、web ページでの変数の一般的な使用例を示しています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-301">The following example shows some typical uses of variables in a web page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

<span data-ttu-id="9b4ea-302">前の例を1つのページで組み合わせると、次のような画面がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-302">If you combine the previous examples in a page, you see this displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="9b4ea-304">データ型の変換とテスト</span><span class="sxs-lookup"><span data-stu-id="9b4ea-304">Converting and Testing Data Types</span></span>

<span data-ttu-id="9b4ea-305">ASP.NET は通常、データ型を自動的に判断することができますが、できないことがあります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-305">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="9b4ea-306">そのため、明示的な変換を実行して ASP.NET を解決することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-306">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="9b4ea-307">型を変換する必要がない場合でも、使用している可能性のあるデータの種類を確認するためにテストすると便利な場合があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-307">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="9b4ea-308">最も一般的なケースは、文字列を別の型 (整数や日付など) に変換する必要がある場合です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-308">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="9b4ea-309">次の例は、文字列を数値に変換する必要がある一般的なケースを示しています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-309">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

<span data-ttu-id="9b4ea-310">規則として、ユーザーの入力は文字列として取得されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-310">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="9b4ea-311">数字を入力するように求められていても、数字を入力した場合でも、ユーザー入力を送信してコードで読み取ると、データは文字列形式になります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-311">Even if you've prompted users to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="9b4ea-312">したがって、文字列を数値に変換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-312">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="9b4ea-313">この例では、変換せずに値に対して算術演算を実行しようとすると、ASP.NET は2つの文字列を追加できないため、次のエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-313">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

<span data-ttu-id="9b4ea-314">*型 ' string ' を ' int ' に暗黙的に変換することはできません。*</span><span class="sxs-lookup"><span data-stu-id="9b4ea-314">*Cannot implicitly convert type 'string' to 'int'.*</span></span>

<span data-ttu-id="9b4ea-315">値を整数に変換するには、`AsInt` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-315">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="9b4ea-316">変換が成功した場合は、数値を追加できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-316">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="9b4ea-317">次の表に、変数の一般的な変換メソッドとテストメソッドの一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-317">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="9b4ea-318"><strong>メソッド</strong></span><span class="sxs-lookup"><span data-stu-id="9b4ea-318"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-319"><strong>説明</strong></span><span class="sxs-lookup"><span data-stu-id="9b4ea-319"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-320"><strong>例</strong></span><span class="sxs-lookup"><span data-stu-id="9b4ea-320"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-321">整数 ("593" など) を表す文字列を整数に変換します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-321">Converts a string that represents a whole number (like "593") to an integer.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-322">&quot;true&quot; のような文字列または false&quot; &quot;ブール型に変換します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-322">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-323">&quot;1.3&quot; または &quot;7.439&quot; などの10進数値を持つ文字列を浮動小数点数に変換します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-323">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-324">&quot;1.3&quot; または &quot;7.439&quot; などの10進数値を持つ文字列を10進数に変換します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-324">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="9b4ea-325">(ASP.NET では、10進数は浮動小数点数よりも正確です)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-325">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-326">日付と時刻の値を表す文字列を ASP.NET `DateTime` 型に変換します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-326">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-327">その他のデータ型を文字列に変換します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-327">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="9b4ea-328">演算子</span><span class="sxs-lookup"><span data-stu-id="9b4ea-328">Operators</span></span>

<span data-ttu-id="9b4ea-329">演算子は、式で実行するコマンドの種類を ASP.NET に指示するキーワードまたは文字です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-329">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="9b4ea-330">C#言語 (およびそれに基づく Razor 構文) では、多くの演算子がサポートされていますが、最初に知っておく必要があるのはいくつかの操作だけです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-330">The C# language (and the Razor syntax that's based on it) supports many operators, but you only need to recognize a few to get started.</span></span> <span data-ttu-id="9b4ea-331">次の表は、最も一般的な演算子をまとめたものです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-331">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="9b4ea-332"><strong>Operator</strong></span><span class="sxs-lookup"><span data-stu-id="9b4ea-332"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-333"><strong>説明</strong></span><span class="sxs-lookup"><span data-stu-id="9b4ea-333"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-334"><strong>例</strong></span><span class="sxs-lookup"><span data-stu-id="9b4ea-334"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="9b4ea-335">`+` `-` `*` `/`</span><span class="sxs-lookup"><span data-stu-id="9b4ea-335">`+` `-` `*` `/`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-336">数値式で使用される算術演算子。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-336">Math operators used in numerical expressions.</span></span>
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-337">代入。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-337">Assignment.</span></span> <span data-ttu-id="9b4ea-338">ステートメントの右辺の値を左側のオブジェクトに代入します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-338">Assigns the value on the right side of a statement to the object on the left side.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-339">等値。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-339">Equality.</span></span> <span data-ttu-id="9b4ea-340">値が等しい場合は `true` を返します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-340">Returns `true` if the values are equal.</span></span> <span data-ttu-id="9b4ea-341">(`=` 演算子と `==` 演算子の違いに注意してください)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-341">(Notice the distinction between the `=` operator and the `==` operator.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-342">非等値。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-342">Inequality.</span></span> <span data-ttu-id="9b4ea-343">値が等しくない場合は `true` を返します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-343">Returns `true` if the values are not equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-344">小なり、大なり、小なり、または等しい、より大きい、または等しい。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-344">Less-than, greater-than, less-than-or-equal, and greater-than-or-equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-345">連結。文字列を結合するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-345">Concatenation, which is used to join strings.</span></span> <span data-ttu-id="9b4ea-346">ASP.NET は、式のデータ型に基づいて、この演算子と加算演算子の違いを認識します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-346">ASP.NET knows the difference between this operator and the addition operator based on the data type of the expression.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="9b4ea-347">`+=` `-=`</span><span class="sxs-lookup"><span data-stu-id="9b4ea-347">`+=` `-=`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-348">インクリメント演算子とデクリメント演算子。変数から 1 (それぞれ) を加算して減算します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-348">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-349">.Dot.</span><span class="sxs-lookup"><span data-stu-id="9b4ea-349">Dot.</span></span> <span data-ttu-id="9b4ea-350">オブジェクトとそのプロパティおよびメソッドを区別するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-350">Used to distinguish objects and their properties and methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-351">内側.</span><span class="sxs-lookup"><span data-stu-id="9b4ea-351">Parentheses.</span></span> <span data-ttu-id="9b4ea-352">式をグループ化し、パラメーターをメソッドに渡すために使用されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-352">Used to group expressions and to pass parameters to methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-353">カッコ.</span><span class="sxs-lookup"><span data-stu-id="9b4ea-353">Brackets.</span></span> <span data-ttu-id="9b4ea-354">配列またはコレクションの値にアクセスするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-354">Used for accessing values in arrays or collections.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-355">じゃない。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-355">Not.</span></span> <span data-ttu-id="9b4ea-356">`true` 値を `false` に戻します。逆も同様です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-356">Reverses a `true` value to `false` and vice versa.</span></span> <span data-ttu-id="9b4ea-357">通常、`false` をテストするための簡単な方法として使用されます (つまり、`true`ではありません)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-357">Typically used as a shorthand way to test for `false` (that is, for not `true`).</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="9b4ea-358">`&&` `||`</span><span class="sxs-lookup"><span data-stu-id="9b4ea-358">`&&` `||`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="9b4ea-359">論理 AND および OR。条件を相互にリンクするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-359">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="9b4ea-360">コードでのファイルとフォルダーのパスの操作</span><span class="sxs-lookup"><span data-stu-id="9b4ea-360">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="9b4ea-361">多くの場合、コードでファイルとフォルダーのパスを操作します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-361">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="9b4ea-362">開発用コンピューターに表示される web サイトの物理フォルダー構造の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-362">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="9b4ea-363">Url とパスに関する重要な詳細情報を次に示します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-363">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="9b4ea-364">URL は、ドメイン名 (`http://www.example.com`) またはサーバー名 (`http://localhost`、`http://mycomputer`) のいずれかで始まります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-364">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="9b4ea-365">URL は、ホストコンピューターの物理パスに対応します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-365">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="9b4ea-366">たとえば、`http://myserver` は、サーバー上の*C:\websites\mywebsite*フォルダーに対応している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-366">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="9b4ea-367">仮想パスは、完全パスを指定しなくてもコード内のパスを表す短縮形です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-367">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="9b4ea-368">これには、ドメイン名またはサーバー名の後の URL の部分が含まれます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-368">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="9b4ea-369">仮想パスを使用すると、パスを更新しなくてもコードを別のドメインまたはサーバーに移動できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-369">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="9b4ea-370">相違点を理解するための例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-370">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="9b4ea-371">完全な URL</span><span class="sxs-lookup"><span data-stu-id="9b4ea-371">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="9b4ea-372">サーバー名</span><span class="sxs-lookup"><span data-stu-id="9b4ea-372">Server name</span></span> | <span data-ttu-id="9b4ea-373">*my企業サーバー*</span><span class="sxs-lookup"><span data-stu-id="9b4ea-373">*mycompanyserver*</span></span> |
| <span data-ttu-id="9b4ea-374">[仮想パス]</span><span class="sxs-lookup"><span data-stu-id="9b4ea-374">Virtual path</span></span> | <span data-ttu-id="9b4ea-375">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="9b4ea-375">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="9b4ea-376">物理パス</span><span class="sxs-lookup"><span data-stu-id="9b4ea-376">Physical path</span></span> | <span data-ttu-id="9b4ea-377">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="9b4ea-377">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="9b4ea-378">仮想ルートは/です。 C: ドライブのルートと同じです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-378">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="9b4ea-379">(仮想フォルダーパスは常にスラッシュを使用します)。フォルダーの仮想パスは、物理フォルダーと同じ名前である必要はありません。エイリアスにすることができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-379">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="9b4ea-380">(実稼働サーバーでは、仮想パスが正確な物理パスと一致することはほとんどありません)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-380">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="9b4ea-381">コード内でファイルやフォルダーを操作するときに、使用しているオブジェクトに応じて、物理パスと仮想パスを参照することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-381">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="9b4ea-382">ASP.NET には、コード内のファイルとフォルダーのパスを操作するためのツールが用意されています。 `Server.MapPath` メソッド、`~` 演算子、および `Href` メソッドです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-382">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="9b4ea-383">仮想パスから物理パスへの変換: サーバーの MapPath メソッド</span><span class="sxs-lookup"><span data-stu-id="9b4ea-383">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="9b4ea-384">`Server.MapPath` メソッドは、仮想パス (C:\WebSites\MyWebSiteFolder\default.cshtml など *)* を絶対物理パス (たとえば、) に変換します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-384">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="9b4ea-385">この方法は、完全な物理パスが必要な場合にいつでも使用できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-385">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="9b4ea-386">一般的な例として、web サーバー上のテキストファイルまたはイメージファイルを読み取ったり書き込んだりする場合があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-386">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="9b4ea-387">通常、ホストサイトのサーバー上にあるサイトの絶対物理パスがわからないため、この方法では、既知のパス (仮想パス) をサーバー上の対応するパスに変換できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-387">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="9b4ea-388">ファイルまたはフォルダーへの仮想パスをメソッドに渡し、物理パスを返します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-388">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="9b4ea-389">仮想ルートの参照: ~ 演算子と Href メソッド</span><span class="sxs-lookup"><span data-stu-id="9b4ea-389">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="9b4ea-390">*Cshtml*ファイルまたは*vbhtml*ファイルでは、`~` 演算子を使用して仮想ルートパスを参照できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-390">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="9b4ea-391">これは、サイト内でページを移動することができ、他のページに含まれているすべてのリンクが破損しないため、非常に便利です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-391">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="9b4ea-392">また、web サイトを別の場所に移動した場合にも便利です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-392">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="9b4ea-393">次にいくつかの例を示します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-393">Here are some examples:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

<span data-ttu-id="9b4ea-394">Web サイトが `http://myserver/myapp`場合は、ページの実行時に ASP.NET がこれらのパスを処理する方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-394">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="9b4ea-395">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="9b4ea-395">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="9b4ea-396">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="9b4ea-396">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="9b4ea-397">(実際には、これらのパスは変数の値としては表示されませんが、ASP.NET はそのようなパスを扱います)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-397">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="9b4ea-398">次のように、サーバーコード (上記) とマークアップの両方で `~` 演算子を使用できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-398">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

<span data-ttu-id="9b4ea-399">マークアップでは、`~` 演算子を使用して、イメージファイル、その他の web ページ、CSS ファイルなどのリソースへのパスを作成します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-399">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="9b4ea-400">ページが実行されると、ASP.NET はページ (コードとマークアップの両方) を参照し、適切なパスへのすべての `~` 参照を解決します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-400">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="9b4ea-401">条件付きロジックとループ</span><span class="sxs-lookup"><span data-stu-id="9b4ea-401">Conditional Logic and Loops</span></span>

<span data-ttu-id="9b4ea-402">ASP.NET server code を使用すると、条件に基づいてタスクを実行し、ステートメントを特定の回数 (ループを実行するコード) に繰り返すコードを記述することができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-402">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times (that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="9b4ea-403">テスト条件</span><span class="sxs-lookup"><span data-stu-id="9b4ea-403">Testing Conditions</span></span>

<span data-ttu-id="9b4ea-404">単純な条件をテストするには、`if` ステートメントを使用します。これは、指定したテストに基づいて true または false を返します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-404">To test a simple condition you use the `if` statement, which returns true or false based on a test you specify:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

<span data-ttu-id="9b4ea-405">`if` キーワードはブロックを開始します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-405">The `if` keyword starts a block.</span></span> <span data-ttu-id="9b4ea-406">実際のテスト (条件) はかっこ内にあり、true または false を返します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-406">The actual test (condition) is in parentheses and returns true or false.</span></span> <span data-ttu-id="9b4ea-407">テストが true の場合に実行されるステートメントは、中かっこで囲まれます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-407">The statements that run if the test is true are enclosed in braces.</span></span> <span data-ttu-id="9b4ea-408">`if` ステートメントには、条件が false の場合に実行するステートメントを指定する `else` ブロックを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-408">An `if` statement can include an `else` block that specifies statements to run if the condition is false:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

<span data-ttu-id="9b4ea-409">`else if` ブロックを使用して複数の条件を追加できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-409">You can add multiple conditions using an `else if` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

<span data-ttu-id="9b4ea-410">この例では、if ブロックの最初の条件が true でない場合、`else if` 条件がチェックされます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-410">In this example, if the first condition in the if block is not true, the `else if` condition is checked.</span></span> <span data-ttu-id="9b4ea-411">この条件が満たされると、`else if` ブロック内のステートメントが実行されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-411">If that condition is met, the statements in the `else if` block are executed.</span></span> <span data-ttu-id="9b4ea-412">条件が満たされていない場合は、`else` ブロック内のステートメントが実行されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-412">If none of the conditions are met, the statements in the `else` block are executed.</span></span> <span data-ttu-id="9b4ea-413">任意の数の else if ブロックを追加して、他のすべての&quot; 条件 &quot;として `else` ブロックで閉じることができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-413">You can add any number of else if blocks, and then close with an `else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="9b4ea-414">多数の条件をテストするには、`switch` ブロックを使用します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-414">To test a large number of conditions, use a `switch` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

<span data-ttu-id="9b4ea-415">テストする値は、かっこで囲まれています (例では `weekday` 変数)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-415">The value to test is in parentheses (in the example, the `weekday` variable).</span></span> <span data-ttu-id="9b4ea-416">個々のテストでは、コロン (:) で終わる `case` ステートメントが使用されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-416">Each individual test uses a `case` statement that ends with a colon (:).</span></span> <span data-ttu-id="9b4ea-417">`case` ステートメントの値がテスト値と一致する場合は、そのケースブロック内のコードが実行されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-417">If the value of a `case` statement matches the test value, the code in that case block is executed.</span></span> <span data-ttu-id="9b4ea-418">各 case ステートメントを終了するには、`break` ステートメントを使用します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-418">You close each case statement with a `break` statement.</span></span> <span data-ttu-id="9b4ea-419">(各 `case` ブロックに break を含め忘れた場合、次の `case` ステートメントのコードも実行されます)。`switch` ブロックには、多くの場合、&quot; &quot;の最後のケースとして `default` ステートメントが含まれています。それ以外の場合は、他のいずれのケースも true ではありません。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-419">(If you forget to include break in each `case` block, the code from the next `case` statement will run also.) A `switch` block often has a `default` statement as the last case for an &quot;everything else&quot; option that runs if none of the other cases are true.</span></span>

<span data-ttu-id="9b4ea-420">ブラウザーに表示された最後の2つの条件ブロックの結果:</span><span class="sxs-lookup"><span data-stu-id="9b4ea-420">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="9b4ea-422">ループコード</span><span class="sxs-lookup"><span data-stu-id="9b4ea-422">Looping Code</span></span>

<span data-ttu-id="9b4ea-423">多くの場合、同じステートメントを繰り返し実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-423">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="9b4ea-424">これを行うには、ループを使用します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-424">You do this by looping.</span></span> <span data-ttu-id="9b4ea-425">たとえば、多くの場合、データのコレクション内の各項目に対して同じステートメントを実行します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-425">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="9b4ea-426">ループする回数が正確にわかっている場合は、`for` ループを使用できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-426">If you know exactly how many times you want to loop, you can use a `for` loop.</span></span> <span data-ttu-id="9b4ea-427">この種類のループは、カウントアップまたはカウントする場合に特に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-427">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

<span data-ttu-id="9b4ea-428">ループは `for` キーワードで始まり、その後に3つのステートメントがかっこで囲まれ、それぞれがセミコロンで終了します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-428">The loop begins with the `for` keyword, followed by three statements in parentheses, each terminated with a semicolon.</span></span>

- <span data-ttu-id="9b4ea-429">かっこ内では、最初のステートメント (`var i=10;`) によってカウンターが作成され、10に初期化されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-429">Inside the parentheses, the first statement (`var i=10;`) creates a counter and initializes it to 10.</span></span> <span data-ttu-id="9b4ea-430">カウンターに名前を付ける必要はあり&#8212;ません `i` 任意の変数を使用できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-430">You don't have to name the counter `i` &#8212; you can use any variable.</span></span> <span data-ttu-id="9b4ea-431">`for` ループが実行されると、カウンターが自動的にインクリメントされます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-431">When the `for` loop runs, the counter is automatically incremented.</span></span>
- <span data-ttu-id="9b4ea-432">2番目のステートメント (`i < 21;`) では、カウントする条件を設定します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-432">The second statement (`i < 21;`) sets the condition for how far you want to count.</span></span> <span data-ttu-id="9b4ea-433">このケースでは、最大20にまで移動します (つまり、カウンターが21未満である間は継続します)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-433">In this case, you want it to go to a maximum of 20 (that is, keep going while the counter is less than 21).</span></span>
- <span data-ttu-id="9b4ea-434">3番目のステートメント (`i++`) では、インクリメント演算子を使用します。これは、ループが実行されるたびにカウンターに1が追加されることを指定するだけです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-434">The third statement (`i++` ) uses an increment operator, which simply specifies that the counter should have 1 added to it each time the loop runs.</span></span>

<span data-ttu-id="9b4ea-435">中かっこ内には、ループの反復ごとに実行されるコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-435">Inside the braces is the code that will run for each iteration of the loop.</span></span> <span data-ttu-id="9b4ea-436">マークアップは、毎回新しい段落 (`<p>` 要素) を作成し、出力に行を追加して `i` (カウンター) の値を表示します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-436">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of `i` (the counter).</span></span> <span data-ttu-id="9b4ea-437">このページを実行すると、この例では、出力を表示する11行を作成し、アイテム番号を示す各行にテキストを入力します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-437">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

<span data-ttu-id="9b4ea-439">コレクションまたは配列を使用して作業している場合は、多くの場合、`foreach` ループを使用します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-439">If you're working with a collection or array, you often use a `foreach` loop.</span></span> <span data-ttu-id="9b4ea-440">コレクションは、類似したオブジェクトのグループであり、`foreach` ループを使用すると、コレクション内の各項目に対してタスクを実行できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-440">A collection is a group of similar objects, and the `foreach` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="9b4ea-441">この種類のループは、`for` ループとは異なり、カウンターをインクリメントしたり制限を設定したりする必要がないため、コレクションに便利です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-441">This type of loop is convenient for collections, because unlike a `for` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="9b4ea-442">代わりに、`foreach` ループコードは、完了するまでコレクションを処理します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-442">Instead, the `foreach` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="9b4ea-443">たとえば、次のコードは、`Request.ServerVariables` コレクション内の項目を返します。これは、web サーバーに関する情報を格納するオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-443">For example, the following code returns the items in the `Request.ServerVariables` collection, which is an object that contains information about your web server.</span></span> <span data-ttu-id="9b4ea-444">`foreac` h ループを使用して、HTML の箇条書きに新しい `<li>` 要素を作成することによって各項目の名前を表示します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-444">It uses a `foreac` h loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

<span data-ttu-id="9b4ea-445">`foreach` キーワードの後に、コレクション内の1つの項目 (例では `var item`) を表す変数を宣言し、続いて `in` キーワードを入力した後、ループするコレクションを指定します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-445">The `foreach` keyword is followed by parentheses where you declare a variable that represents a single item in the collection (in the example, `var item`), followed by the `in` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="9b4ea-446">`foreach` ループの本体では、前に宣言した変数を使用して現在の項目にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-446">In the body of the `foreach` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

<span data-ttu-id="9b4ea-448">より汎用的なループを作成するには、`while` ステートメントを使用します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-448">To create a more general-purpose loop, use the `while` statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

<span data-ttu-id="9b4ea-449">`while` ループは、`while` キーワードで始まり、その後に、ループの継続時間 (ここでは `countNum` が50未満である限り) を指定します。次に、繰り返します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-449">A `while` loop begins with the `while` keyword, followed by parentheses where you specify how long the loop continues (here, for as long as `countNum` is less than 50), then the block to repeat.</span></span> <span data-ttu-id="9b4ea-450">ループは通常、カウントに使用される変数またはオブジェクトをインクリメント (加算) またはデクリメント (減算) します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-450">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="9b4ea-451">この例では、`+=` 演算子は、ループが実行されるたびに `countNum` に1を加算します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-451">In the example, the `+=` operator adds 1 to `countNum` each time the loop runs.</span></span> <span data-ttu-id="9b4ea-452">(カウントダウンするループ内で変数をデクリメントするには、デクリメント演算子 `-=`) を使用します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-452">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`).</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="9b4ea-453">オブジェクトとコレクション</span><span class="sxs-lookup"><span data-stu-id="9b4ea-453">Objects and Collections</span></span>

<span data-ttu-id="9b4ea-454">ASP.NET web サイトのほぼすべてのものは、web ページ自体を含むオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-454">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="9b4ea-455">このセクションでは、コード内で頻繁に使用するいくつかの重要なオブジェクトについて説明します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-455">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="9b4ea-456">Page オブジェクト</span><span class="sxs-lookup"><span data-stu-id="9b4ea-456">Page Objects</span></span>

<span data-ttu-id="9b4ea-457">ASP.NET の最も基本的なオブジェクトはページです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-457">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="9b4ea-458">ページオブジェクトのプロパティには、修飾されたオブジェクトを使用せずに直接アクセスできます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-458">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="9b4ea-459">次のコードは、ページの `Request` オブジェクトを使用して、ページのファイルパスを取得します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-459">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

<span data-ttu-id="9b4ea-460">現在の page オブジェクトのプロパティとメソッドを参照していることを明確にするために、必要に応じて `this` キーワードを使用して、コード内のページオブジェクトを表すことができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-460">To make it clear that you're referencing properties and methods on the current page object, you can optionally use the keyword `this` to represent the page object in your code.</span></span> <span data-ttu-id="9b4ea-461">次に示すのは、上記のコード例です。ページを表すために `this` が追加されています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-461">Here is the previous code example, with `this` added to represent the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

<span data-ttu-id="9b4ea-462">`Page` オブジェクトのプロパティを使用して、次のような大量の情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-462">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="9b4ea-463">`Request`.</span><span class="sxs-lookup"><span data-stu-id="9b4ea-463">`Request`.</span></span> <span data-ttu-id="9b4ea-464">既に説明したように、これは現在の要求に関する情報のコレクションです。要求を行ったブラウザーの種類、ページの URL、ユーザー id などが含まれます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-464">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="9b4ea-465">`Response`.</span><span class="sxs-lookup"><span data-stu-id="9b4ea-465">`Response`.</span></span> <span data-ttu-id="9b4ea-466">これは、サーバーコードの実行が終了したときにブラウザーに送信される応答 (ページ) に関する情報のコレクションです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-466">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="9b4ea-467">たとえば、このプロパティを使用して、応答に情報を書き込むことができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-467">For example, you can use this property to write information into the response.</span></span> 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="9b4ea-468">コレクションオブジェクト (配列とディクショナリ)</span><span class="sxs-lookup"><span data-stu-id="9b4ea-468">Collection Objects (Arrays and Dictionaries)</span></span>

<span data-ttu-id="9b4ea-469">*コレクション*は、データベースの `Customer` オブジェクトのコレクションなど、同じ種類のオブジェクトのグループです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-469">A *collection* is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="9b4ea-470">ASP.NET には、`Request.Files` コレクションのような多くの組み込みコレクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-470">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="9b4ea-471">多くの場合、コレクション内のデータを操作します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-471">You'll often work with data in collections.</span></span> <span data-ttu-id="9b4ea-472">2つの一般的なコレクション型は、*配列*と*ディクショナリ*です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-472">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="9b4ea-473">配列は、類似した項目のコレクションを格納するが、各項目を保持するための個別の変数を作成しない場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-473">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

<span data-ttu-id="9b4ea-474">配列を使用して、`string`、`int`、`DateTime`などの特定のデータ型を宣言します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-474">With arrays, you declare a specific data type, such as `string`, `int`, or `DateTime`.</span></span> <span data-ttu-id="9b4ea-475">変数に配列を含めることができることを示すには、宣言に角かっこを追加します (`string[]` や `int[]`など)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-475">To indicate that the variable can contain an array, you add brackets to the declaration (such as `string[]` or `int[]`).</span></span> <span data-ttu-id="9b4ea-476">配列内の項目には、その位置 (インデックス) を使用するか、`foreach` ステートメントを使用してアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-476">You can access items in an array using their position (index) or by using the `foreach` statement.</span></span> <span data-ttu-id="9b4ea-477">配列インデックスは 0 &#8212;から始まります。つまり、最初の項目の位置は0、2番目の項目は1の位置にあります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-477">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

<span data-ttu-id="9b4ea-478">配列内の項目の数を確認するには、その `Length` プロパティを取得します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-478">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="9b4ea-479">配列内の特定の項目の位置を取得するには (配列を検索する場合)、`Array.IndexOf` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-479">To get the position of a specific item in the array (to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="9b4ea-480">また、配列の内容 (`Array.Reverse` メソッド) の反転やコンテンツ (`Array.Sort` メソッド) の並べ替えなどを行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-480">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="9b4ea-481">ブラウザーに表示される文字列配列コードの出力を次に示します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-481">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

<span data-ttu-id="9b4ea-483">ディクショナリはキーと値のペアのコレクションであり、キー (または名前) を指定して、対応する値を設定または取得します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-483">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

<span data-ttu-id="9b4ea-484">ディクショナリを作成するには、`new` キーワードを使用して、新しい辞書オブジェクトを作成していることを示します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-484">To create a dictionary, you use the `new` keyword to indicate that you're creating a new dictionary object.</span></span> <span data-ttu-id="9b4ea-485">`var` キーワードを使用して、変数に辞書を割り当てることができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-485">You can assign a dictionary to a variable using the `var` keyword.</span></span> <span data-ttu-id="9b4ea-486">ディクショナリ内の項目のデータ型は、山かっこ (`< >`) を使用して指定します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-486">You indicate the data types of the items in the dictionary using angle brackets ( `< >` ).</span></span> <span data-ttu-id="9b4ea-487">宣言の最後に、かっこのペアを追加する必要があります。これは、実際には新しいディクショナリを作成するメソッドであるためです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-487">At the end of the declaration, you must add a pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="9b4ea-488">ディクショナリに項目を追加するには、ディクショナリ変数 (この場合は`myScores`) の `Add` メソッドを呼び出して、キーと値を指定します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-488">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="9b4ea-489">また、次の例のように、角かっこを使用してキーを指定し、単純な割り当てを行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-489">Alternatively, you can use square brackets to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

<span data-ttu-id="9b4ea-490">ディクショナリから値を取得するには、キーを角かっこで囲んで指定します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-490">To get a value from the dictionary, you specify the key in brackets:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="9b4ea-491">パラメーターを使用したメソッドの呼び出し</span><span class="sxs-lookup"><span data-stu-id="9b4ea-491">Calling Methods with Parameters</span></span>

<span data-ttu-id="9b4ea-492">この記事の前半で説明したように、を使用してプログラミングするオブジェクトには、メソッドを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-492">As you read earlier in this article, the objects that you program with can have methods.</span></span> <span data-ttu-id="9b4ea-493">たとえば、`Database` オブジェクトには、`Database.Connect` メソッドがある場合があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-493">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="9b4ea-494">多くのメソッドには、1つまたは複数のパラメーターもあります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-494">Many methods also have one or more parameters.</span></span> <span data-ttu-id="9b4ea-495">*パラメーター*は、メソッドがタスクを完了できるようにメソッドに渡す値です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-495">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="9b4ea-496">たとえば、`Request.MapPath` メソッドの宣言を見て、次の3つのパラメーターを取得します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-496">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

<span data-ttu-id="9b4ea-497">(行は、読みやすくするために折り返されています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-497">(The line has been wrapped to make it more readable.</span></span> <span data-ttu-id="9b4ea-498">改行は、引用符で囲まれた文字列内を除き、ほぼすべての場所に配置することができます)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-498">Remember that you can put line breaks almost any place except inside strings that are enclosed in quotation marks.)</span></span>

<span data-ttu-id="9b4ea-499">このメソッドは、指定された仮想パスに対応するサーバー上の物理パスを返します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-499">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="9b4ea-500">メソッドの3つのパラメーターは、`virtualPath`、`baseVirtualDir`、および `allowCrossAppMapping`です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-500">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="9b4ea-501">(宣言では、パラメーターが、受け入れられるデータのデータ型と共に一覧表示されていることに注意してください)。このメソッドを呼び出す場合は、3つのすべてのパラメーターの値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-501">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="9b4ea-502">Razor 構文には、メソッドにパラメーターを渡す方法として、*位置指定*パラメーターと*名前付きパラメーター*の2つのオプションが用意されています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-502">The Razor syntax gives you two options for passing parameters to a method: *positional parameters* and *named parameters*.</span></span> <span data-ttu-id="9b4ea-503">位置指定パラメーターを使用してメソッドを呼び出すには、メソッド宣言で指定された厳密な順序でパラメーターを渡します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-503">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="9b4ea-504">(通常、この順序については、メソッドのドキュメントを参照してください)。順序に従う必要があります。また、必要に応じて&#8212;パラメーターを省略することはできません。値のない位置指定パラメーターには、空の文字列 (`""`) または `null` を渡します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-504">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or `null` for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="9b4ea-505">次の例では、web サイトに*scripts*という名前のフォルダーがあることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-505">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="9b4ea-506">このコードは `Request.MapPath` メソッドを呼び出し、3つのパラメーターの値を正しい順序で渡します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-506">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="9b4ea-507">次に、結果としてマップされたパスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-507">It then displays the resulting mapped path.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

<span data-ttu-id="9b4ea-508">メソッドに多数のパラメーターがある場合は、名前付きパラメーターを使用してコードを読みやすくすることができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-508">When a method has many parameters, you can keep your code more readable by using named parameters.</span></span> <span data-ttu-id="9b4ea-509">名前付きパラメーターを使用してメソッドを呼び出すには、パラメーター名の後にコロン (:) を指定し、その後に値を指定します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-509">To call a method using named parameters, you specify the parameter name followed by a colon (:), and then the value.</span></span> <span data-ttu-id="9b4ea-510">名前付きパラメーターの利点は、任意の順序で渡すことができることです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-510">The advantage of named parameters is that you can pass them in any order you want.</span></span> <span data-ttu-id="9b4ea-511">(欠点は、メソッドの呼び出しがコンパクトではないことです)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-511">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="9b4ea-512">次の例では、上記と同じメソッドを呼び出しますが、名前付きパラメーターを使用して値を指定します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-512">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

<span data-ttu-id="9b4ea-513">ご覧のように、パラメーターは異なる順序で渡されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-513">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="9b4ea-514">ただし、前の例とこの例を実行すると、同じ値が返されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-514">However, if you run the previous example and this example, they'll return the same value.</span></span>

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a><span data-ttu-id="9b4ea-515">エラーの処理</span><span class="sxs-lookup"><span data-stu-id="9b4ea-515">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="9b4ea-516">Try-catch ステートメント</span><span class="sxs-lookup"><span data-stu-id="9b4ea-516">Try-Catch Statements</span></span>

<span data-ttu-id="9b4ea-517">多くの場合、コントロール以外の理由で失敗する可能性のあるステートメントがコードに含まれています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-517">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="9b4ea-518">例:</span><span class="sxs-lookup"><span data-stu-id="9b4ea-518">For example:</span></span>

- <span data-ttu-id="9b4ea-519">コードでファイルを作成またはアクセスしようとすると、すべてのエラーが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-519">If your code tries to create or access a file, all sorts of errors might occur.</span></span> <span data-ttu-id="9b4ea-520">必要なファイルが存在しない可能性があります。ロックされているか、コードにアクセス許可がない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-520">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="9b4ea-521">同様に、コードがデータベース内のレコードを更新しようとすると、アクセス許可の問題が発生し、データベースへの接続が切断され、保存するデータが無効になっている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-521">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="9b4ea-522">プログラミング用語では、これらの状況は*例外*と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-522">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="9b4ea-523">コードで例外が発生した場合、ユーザーにとって非常に面倒なエラーメッセージが生成されます (スローされます)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-523">If your code encounters an exception, it generates (throws) an error message that's, at best, annoying to users:</span></span>

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

<span data-ttu-id="9b4ea-525">コードで例外が発生する可能性があり、この種類のエラーメッセージが表示されないようにするには、`try/catch` ステートメントを使用します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-525">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `try/catch` statements.</span></span> <span data-ttu-id="9b4ea-526">`try` ステートメントでは、チェックしているコードを実行します。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-526">In the `try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="9b4ea-527">1つ以上の `catch` ステートメントでは、発生した可能性のある特定のエラー (特定の種類の例外) を検索できます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-527">In one or more `catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="9b4ea-528">予測しているエラーを検索するために必要な数の `catch` ステートメントを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-528">You can include as many `catch` statements as you need to look for errors that you are anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="9b4ea-529">`try/catch` ステートメントでは `Response.Redirect` メソッドを使用しないことをお勧めします。これは、ページで例外が発生する可能性があるためです。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-529">We recommend that you avoid using the `Response.Redirect` method in `try/catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="9b4ea-530">次の例は、最初の要求でテキストファイルを作成し、ユーザーがファイルを開くためのボタンを表示するページを示しています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-530">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="9b4ea-531">この例では、例外が発生するように、不適切なファイル名を意図的に使用しています。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-531">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="9b4ea-532">このコードには `catch` 2 つの例外のステートメントが含まれています。 `FileNotFoundException`は、ファイル名が正しくない場合に発生します。また、ASP.NET がフォルダーを検索できない場合に発生する `DirectoryNotFoundException`です。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-532">The code includes `catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="9b4ea-533">(例では、すべてが正常に動作するときに実行方法を確認するために、ステートメントのコメントを解除できます)。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-533">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="9b4ea-534">コードで例外が処理されなかった場合は、前のスクリーンショットのようなエラーページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-534">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="9b4ea-535">ただし、`try/catch` セクションは、ユーザーがこれらの種類のエラーを表示できないようにするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="9b4ea-535">However, the `try/catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="9b4ea-536">その他の資料</span><span class="sxs-lookup"><span data-stu-id="9b4ea-536">Additional Resources</span></span>

<span data-ttu-id="9b4ea-537">**Visual Basic を使用したプログラミング**</span><span class="sxs-lookup"><span data-stu-id="9b4ea-537">**Programming with Visual Basic**</span></span>

[<span data-ttu-id="9b4ea-538">付録: Visual Basic の言語と構文</span><span class="sxs-lookup"><span data-stu-id="9b4ea-538">Appendix: Visual Basic Language and Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkId=202908)

<span data-ttu-id="9b4ea-539">**リファレンスドキュメント**</span><span class="sxs-lookup"><span data-stu-id="9b4ea-539">**Reference Documentation**</span></span>

[<span data-ttu-id="9b4ea-540">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9b4ea-540">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)

[<span data-ttu-id="9b4ea-541">C#言語</span><span class="sxs-lookup"><span data-stu-id="9b4ea-541">C# Language</span></span>](https://msdn.microsoft.com/library/kx37x362.aspx)
