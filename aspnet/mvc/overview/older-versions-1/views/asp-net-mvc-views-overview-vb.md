---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: ASP.NET MVC ビューの概要 (VB) |Microsoft Docs
author: StephenWalther
description: ASP.NET MVC ビューとは何ですか。また、HTML ページとどのような違いがありますか。 このチュートリアルでは、Stephen Walther がビューを紹介し、その方法を示します。
ms.author: riande
ms.date: 02/16/2008
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: a07d15cb14e9ef90b62c5a8702dee53f1a0a6032
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044667"
---
# <a name="aspnet-mvc-views-overview-vb"></a>ASP.NET MVC ビュー概要 (VB)

[Stephen Walther](https://github.com/StephenWalther)

> ASP.NET MVC ビューとは何ですか。また、HTML ページとどのような違いがありますか。 このチュートリアルでは、Stephen Walther を使用してビューを作成し、ビュー内でビューデータと HTML ヘルパーを活用する方法を紹介します。

このチュートリアルの目的は、MVC ビューの ASP.NET、データの表示、および HTML ヘルパーの概要を説明することです。 このチュートリアルの最後に、新しいビューを作成する方法、コントローラーからビューにデータを渡す方法、HTML ヘルパーを使用してビューのコンテンツを生成する方法について理解しておく必要があります。

## <a name="understanding-views"></a>ビューについて

ASP.NET または Active Server ページとは異なり、ASP.NET MVC には、ページに直接対応するものは含まれません。 ASP.NET MVC アプリケーションでは、ブラウザーのアドレスバーに入力する URL 内のパスに対応するページがディスク上にありません。 ASP.NET MVC アプリケーションのページに最も近いのは、 *ビュー*と呼ばれるものです。

ASP.NET MVC アプリケーションでは、入力方向のブラウザー要求がコントローラーアクションにマップされます。 コントローラーアクションはビューを返すことがあります。 ただし、コントローラーアクションでは、他の種類のアクション (別のコントローラーアクションへのリダイレクトなど) が実行される場合があります。

リスト1には、HomeController という名前のシンプルなコントローラーが含まれています。 HomeController は、Index () と Details () という2つのコントローラーアクションを公開します。

**リスト 1-HomeController**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

ブラウザーのアドレスバーに次の URL を入力して、最初のアクション (Index () アクション) を呼び出すことができます。

/Home/Index

このアドレスをブラウザーに入力することで、2番目のアクションである Details () アクションを呼び出すことができます。

/Home/Details

Index () アクションを実行すると、ビューが返されます。 作成するほとんどの操作では、ビューが返されます。 ただし、アクションは他の種類のアクション結果を返すことができます。 たとえば、Details () アクションは、着信要求を Index () アクションにリダイレクトする RedirectToActionResult を返します。

Index () アクションには、次の1行のコードが含まれています。

View ()

次のコード行では、web サーバー上の次のパスにあるビューが返されます。

\Views\Home\Index.aspx

ビューへのパスは、コントローラーの名前とコントローラーアクションの名前から推測されます。

必要に応じて、ビューを明示的に指定することもできます。 次のコード行では、Fred という名前のビューが返されます。

ビュー (Fred)

このコード行を実行すると、次のパスからビューが返されます。

\Views\Home\Fred.aspx

> [!NOTE] 
> 
> ASP.NET MVC アプリケーションの単体テストを作成する予定の場合は、ビュー名について明示することをお勧めします。 これにより、単体テストを作成して、必要なビューがコントローラーアクションによって返されたことを確認できます。

## <a name="adding-content-to-a-view"></a>ビューへのコンテンツの追加

ビューは、スクリプトを含めることができる標準 (X) の HTML ドキュメントです。 スクリプトを使用して、動的なコンテンツをビューに追加します。

たとえば、リスト2のビューには、現在の日付と時刻が表示されます。

**リスト 2-\Views\Home\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

リスト2の HTML ページの本文には、次のスクリプトが含まれていることに注意してください。

&lt;% Response. 書き込み (DateTime. Now)%&gt;

スクリプト &lt; &gt; の先頭と末尾を示すには、スクリプトの区切り記号% と% を使用します。 このスクリプトは、Visual basic で記述されています。 ブラウザーにコンテンツを表示するために、Write () メソッドを呼び出して現在の日付と時刻を表示します。 スクリプトの区切り記号 &lt; % と% を使用して、 &gt; 1 つまたは複数のステートメントを実行できます。

Response. Write () を呼び出すと、Microsoft から、Response () メソッドを呼び出すためのショートカットが提供されます。 リスト3のビューでは、 &lt; &gt; 応答の呼び出し () のショートカットとして区切り記号% = と% を使用します。

**リスト 3-Views\Home\Index2.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

任意の .NET 言語を使用して、動的なコンテンツをビューに生成できます。 通常は、Visual Basic .NET または C# のいずれかを使用して、コントローラーとビューを記述します。

## <a name="using-html-helpers-to-generate-view-content"></a>HTML ヘルパーを使用したビューコンテンツの生成

ビューにコンテンツを簡単に追加できるようにするために、 *HTML ヘルパー*と呼ばれるものを利用できます。 通常、HTML ヘルパーは、文字列を生成するメソッドです。 HTML ヘルパーを使用すると、テキストボックス、リンク、ドロップダウンリスト、リストボックスなどの標準の HTML 要素を生成できます。

たとえば、リスト4のビューでは、3つの HTML ヘルパー (BeginForm ()、TextBox ()、および Password () ヘルパー) を利用して、ログインフォームを生成します (図1を参照)。

**リスト 4--\Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)

**図 01**: 標準のログインフォーム ([クリックすると、フルサイズの画像が表示](asp-net-mvc-views-overview-vb/_static/image2.png)される)

すべての HTML ヘルパーメソッドは、ビューの Html プロパティで呼び出されます。 たとえば、TextBox () メソッドを呼び出すことによってテキストボックスをレンダリングします。

&lt; &gt; Html の TextBox () ヘルパーと .html () ヘルパーの両方を呼び出すときは、スクリプトの区切り記号% = と% を使用することに注意してください。 これらのヘルパーは単に文字列を返します。 文字列をブラウザーに表示するには、Response. Write () を呼び出す必要があります。

HTML ヘルパーメソッドの使用は省略可能です。 記述する必要のある HTML およびスクリプトの量を減らすことで、作業が簡単になります。 リスト5のビューでは、HTML ヘルパーを使用せずに、リスト4のビューとまったく同じ形式がレンダリングされます。

**リスト 5--\Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

独自の HTML ヘルパーを作成することもできます。 たとえば、データベースレコードのセットを HTML テーブルに自動的に表示する GridView () ヘルパーメソッドを作成できます。 このトピックでは、 **カスタム HTML ヘルパーの作成**について説明します。

## <a name="using-view-data-to-pass-data-to-a-view"></a>ビューデータを使用してビューにデータを渡す

ビューデータを使用して、コントローラーからビューにデータを渡します。 メールを通じて送信するパッケージのようなデータを表示してみてください。 コントローラーからビューに渡されるすべてのデータは、このパッケージを使用して送信する必要があります。 たとえば、リスト6のコントローラーは、データを表示するメッセージを追加します。

**リスト 6-ProductController .vb**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

Controller ViewData プロパティは、名前と値のペアのコレクションを表します。 リスト6では、Index () メソッドは、Hello World! という値を持つメッセージという名前のビューデータコレクションに項目を追加します。 Index () メソッドによってビューが返されると、ビューデータは自動的にビューに渡されます。

リスト7のビューでは、ビューデータからメッセージが取得され、ブラウザーに表示されます。

**リスト 7--\Views\Product\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

このビューでは、メッセージを表示するときに html. Encode () HTML ヘルパーメソッドが利用されていることに注意してください。 Html の Encode () HTML ヘルパーは、やなどの特殊文字を、 &lt; &gt; web ページに安全に表示できる文字にエンコードします。 ユーザーが web サイトに送信するコンテンツをレンダリングするときは常に、JavaScript インジェクション攻撃を防ぐためにコンテンツをエンコードする必要があります。

(ProductController に自分でメッセージを作成したので、実際にはメッセージをエンコードする必要はありません。 ただし、ビュー内のビューデータから取得したコンテンツを表示するときは、常に Html の Encode () メソッドを呼び出すことをお勧めします。

リスト7では、ビューデータを利用して、コントローラーからビューに単純な文字列メッセージを渡していました。 また、ビューデータを使用して、データベースレコードのコレクションなど、他の種類のデータをコントローラーからビューに渡すこともできます。 たとえば、Products データベーステーブルの内容をビューに表示する場合は、データベースレコードのコレクションをビューデータに渡すことになります。

また、厳密に型指定されたビューデータをコントローラーからビューに渡すこともできます。 このトピックでは、厳密に **型指定されたビューのデータとビューについ**て説明します。

## <a name="summary"></a>まとめ

このチュートリアルでは、MVC ビューの ASP.NET、データの表示、および HTML ヘルパーについて簡単に説明しました。 最初のセクションでは、新しいビューをプロジェクトに追加する方法について学習しました。 特定のコントローラーからビューを呼び出すには、適切なフォルダーにビューを追加する必要があることを学びました。 次に、HTML ヘルパーのトピックについて説明しました。 HTML ヘルパーを使用して、標準の HTML コンテンツを簡単に生成する方法について学習しました。 最後に、ビューデータを利用して、コントローラーからビューにデータを渡す方法について学習しました。

> [!div class="step-by-step"]
> [前へ](passing-data-to-view-master-pages-cs.md)
> [次へ](creating-custom-html-helpers-vb.md)
