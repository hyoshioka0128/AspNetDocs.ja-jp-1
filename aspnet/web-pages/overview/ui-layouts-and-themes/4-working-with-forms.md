---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: ASP.NET Web ページ (Razor) サイトでの HTML フォームの操作 |Microsoft Docs
author: Rick-Anderson
description: フォームは、テキストボックス、チェックボックス、オプションボタン、プルダウンリストなどのユーザー入力コントロールを配置する HTML ドキュメントのセクションです。 フォーム wh を使用します。
ms.author: riande
ms.date: 02/10/2014
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: c7d4802063c8610a246afe67bd15eea429f7304a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519604"
---
# <a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a>ASP.NET Web ページ (Razor) サイトでの HTML フォームの操作

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、ASP.NET Web ページ (Razor) web サイトで作業しているときに HTML フォーム (テキストボックスとボタン) を処理する方法について説明します。
> 
> **学習内容:** 
> 
> - HTML フォームを作成する方法。
> - フォームからユーザー入力を読み取る方法。
> - ユーザー入力を検証する方法。
> - ページの送信後にフォーム値を復元する方法。
> 
> この記事で紹介する ASP.NET プログラミングの概念は次のとおりです。
> 
> - `Request` オブジェクトです。
> - 入力の検証。
> - HTML エンコード。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 3
>   
> 
> このチュートリアルは ASP.NET Web ページ2でも動作します。

## <a name="creating-a-simple-html-form"></a>単純な HTML フォームの作成

1. 新しい web サイトを作成します。
2. ルートフォルダーで、*フォーム cshtml*という名前の web ページを作成し、次のマークアップを入力します。

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. ブラウザーでページを起動します。 (WebMatrix の **[ファイル]** ワークスペースで、ファイルを右クリックし、 **[ブラウザーで起動]** を選択します)。3つの入力フィールドと **[送信]** ボタンを含む単純なフォームが表示されます。

    ![3つのテキストボックスがあるフォームのスクリーンショット。](4-working-with-forms/_static/image1.png)

    この時点で、 **[送信]** ボタンをクリックしても何も起こりません。 フォームを使いやすくするには、サーバーで実行するコードを追加する必要があります。

## <a name="reading-user-input-from-the-form"></a>フォームからのユーザー入力の読み取り

フォームを処理するには、送信されたフィールド値を読み取り、それらの値を処理するコードを追加します。 この手順では、フィールドを読み取り、ユーザー入力をページに表示する方法について説明します。 (実稼働アプリケーションでは、通常、ユーザー入力を使用してより興味深いものを実行します。 これは、データベースの操作に関する記事で説明されています。)

1. *フォームの cshtml*ファイルの先頭に、次のコードを入力します。

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    ユーザーが最初にページを要求すると、空のフォームのみが表示されます。 フォームにユーザーが入力し、 **[送信]** をクリックします。 これにより、ユーザー入力がサーバーに送信 (投稿) されます。 既定では、要求は同じページ (つまり、 *cshtml*) に送られます。

    この時点でページを送信すると、入力した値がフォームのすぐ上に表示されます。

    ![入力した値がページに表示されるスクリーンショット。](4-working-with-forms/_static/image2.png)

    ページのコードを確認します。 まず、`IsPost` メソッドを使用して、ページがポスト&#8212;されているかどうかを確認します。これは、ユーザーが **[送信]** ボタンをクリックしたかどうかによって決まります。 これが post の場合、`IsPost` は true を返します。 これは、初期要求 (GET 要求) とポストバック (POST 要求) のどちらを使用しているかを判断するために ASP.NET Web ページでの標準的な方法です。 (GET と POST の詳細については、「 [Razor 構文を使用した ASP.NET Web ページプログラミングの概要](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost)」の「HTTP GET and post」と「IsPost プロパティ」を参照してください)。

    次に、ユーザーが `Request.Form` オブジェクトから入力した値を取得し、後で変数に格納します。 `Request.Form` オブジェクトには、ページで送信されたすべての値が含まれます。各値はキーによって識別されます。 キーは、読み取るフォームフィールドの `name` 属性に相当します。 たとえば、`companyname` フィールド (テキストボックス) を読み取るには、`Request.Form["companyname"]`を使用します。

    フォーム値は、`Request.Form` オブジェクトに文字列として格納されます。 したがって、数値、日付、またはその他の型として値を操作する必要がある場合は、文字列からその型に変換する必要があります。 この例では、`Request.Form` の `AsInt` メソッドを使用して、employees フィールド (従業員数を含む) の値を整数に変換します。
2. ブラウザーでページを起動し、フォームのフィールドに入力して、 **[送信]** をクリックします。 このページには、入力した値が表示されます。

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a>外観とセキュリティのための HTML エンコード
> 
> HTML には、`<`、`>`、`&`などの文字が特別に使用されています。 これらの特殊文字が想定されていない場所に出現すると、web ページの外観と機能が無駄になる可能性があります。 たとえば、ブラウザーは、`<b>` または `<input ...>`のように、HTML 要素の先頭として `<` 文字 (後にスペースがある場合を除く) を解釈します。 ブラウザーが要素を認識しない場合は、`<` で始まる文字列を破棄するだけで、再度認識されるようになります。 当然ながら、これによってページに外観が変わってしまう可能性があります。
> 
> HTML エンコーディングでは、これらの予約文字は、ブラウザーが正しいシンボルとして解釈するコードに置き換えられます。 たとえば、`<` 文字は `&lt;` に置き換えられ、`>` 文字は `&gt;`に置き換えられます。 ブラウザーでは、表示する文字としてこれらの置換文字列がレンダリングされます。
> 
> ユーザーから返された文字列 (入力) を表示するときは常に HTML エンコーディングを使用することをお勧めします。 そうしないと、ユーザーは、悪意のあるスクリプトを実行したり、サイトのセキュリティを侵害したり、意図したものではないものを実行したりするために web ページを取得しようとすることができます。 (これは、ユーザーの入力を取得し、その場所を保存した後、ブログ&#8212;コメントやユーザーのレビューなどのように後で表示する場合に特に重要です)。
> 
> これらの問題を回避するために、ASP.NET Web ページは、コードから出力されたテキストコンテンツを自動的に HTML エンコードします。 たとえば、`@MyVar`などのコードを使用して変数または式の内容を表示すると、ASP.NET Web ページによって出力が自動的にエンコードされます。

## <a name="validating-user-input"></a>ユーザー入力の検証

ユーザーは間違いを犯してしまいます。 フィールドに入力するように要求したときに、忘れた場合、または従業員の数を入力するように依頼した場合は、代わりに名前を入力します。 フォームを処理する前に正しく入力されていることを確認するには、ユーザーの入力を検証します。

この手順では、3つのフォームフィールドをすべて検証して、ユーザーがそれらを空白のままにしていないことを確認する方法を示します。 また、employee count の値が数値であることも確認します。 エラーが発生した場合は、検証に合格しなかった値をユーザーに通知するエラーメッセージが表示されます。

1. フォームの*cshtml*ファイルで、最初のコードブロックを次のコードに置き換えます。 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    ユーザー入力を検証するには、`Validation` ヘルパーを使用します。 `Validation.RequireField`を呼び出すことによって、必要なフィールドを登録します。 `Validation.Add` を呼び出し、検証するフィールドと実行する検証の種類を指定することによって、他の種類の検証を登録します。

    ページを実行すると、ASP.NET によってすべての検証が行われます。 結果を確認するには、`Validation.IsValid`を呼び出します。これにより、すべての値が渡された場合は true が返され、検証に失敗した場合は false が返されます。 通常は、ユーザー入力に対して処理を実行する前に `Validation.IsValid` を呼び出します。
2. 次のように、`Html.ValidationMessage` メソッドに3つの呼び出しを追加して、`<body>` 要素を更新します。

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    検証エラーメッセージを表示するには、Html.`ValidationMessage` を呼び出すことができます。 メッセージに必要なフィールドの名前を渡します。
3. ページを実行します。 フィールドを空白のままにして、 **[送信]** をクリックします。 エラーメッセージが表示できます。

    ![ユーザー入力が検証に合格しない場合に表示されるエラーメッセージを示すスクリーンショット。](4-working-with-forms/_static/image3.jpg)
4. "ABC" などの文字列を " **Employee Count** " フィールドに追加し、もう一度 **[Submit]** をクリックします。 今回は、文字列が正しい形式ではないことを示すエラーが表示されます。つまり、整数です。

    ![ユーザーが従業員フィールドに文字列を入力した場合に表示されるエラーメッセージを示すスクリーンショット。](4-working-with-forms/_static/image4.jpg)

ASP.NET Web ページには、ユーザーの入力を検証するためのオプションが多数用意されています。たとえば、クライアントスクリプトを使用して自動的に検証を実行し、ユーザーがブラウザーですぐにフィードバックを取得できるようにします。 詳細については、後の「[その他のリソース](#Additional_Resources)」を参照してください。

## <a name="restoring-form-values-after-postbacks"></a>ポストバック後のフォーム値の復元

前のセクションのページをテストしたときに、検証エラーが発生した場合は (無効なデータだけでなく) 入力したものがすべて削除され、すべてのフィールドの値を再入力する必要があることがわかります。 これは重要な点を示しています。ページを送信し、処理した後、再度ページを表示すると、ページがゼロから再作成されます。 ご覧のとおり、これは、送信時にページ内にあったすべての値が失われることを意味します。

ただし、これは簡単に修正できます。 送信された値 (`Request.Form` オブジェクト内) にアクセスできるため、ページを表示するときにこれらの値をフォームフィールドに戻すことができます。

1. フォームの*cshtml*ファイルで、`value` 属性を使用して、`<input>` 要素の `value` 属性を置き換えます。 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    `<input>` 要素の `value` 属性は、`Request.Form` オブジェクトからフィールド値を動的に読み取るように設定されています。 ページが初めて要求されたときは、`Request.Form` オブジェクトの値がすべて空になります。 これは、フォームが空白であるため、問題ありません。
2. ブラウザーでページを起動し、フォームフィールドに入力するか、空白のままにして、 **[送信]** をクリックします。 送信された値を表示するページが表示されます。

    ![フォーム-5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>その他のリソース

- [1001 Web ユーザーから入力を取得する方法](https://msdn.microsoft.com/library/ms971057.aspx)
- [フォームを使用してユーザー入力を処理する](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)
- [ASP.NET Web ページにおけるユーザー入力の検証](https://go.microsoft.com/fwlink/?LinkId=253002)
- [HTML フォームでのオートコンプリートの使用](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)
