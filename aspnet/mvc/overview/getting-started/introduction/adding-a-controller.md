---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: コントローラーの追加 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: ae3258872df798f52d8e031dc8ebf01b4f0a7358
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045131"
---
# <a name="adding-a-controller"></a>コントローラーを追加する

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

MVC は、 *モデルビューコントローラー*を表します。 MVC は、適切な設計、テスト、保守が容易なアプリケーションを開発するためのパターンです。 MVC ベースのアプリケーションには次のものが含まれます。

- **M** odels: アプリケーションのデータを表し、検証ロジックを使用してそのデータにビジネスルールを適用するクラス。
- **V** iews: アプリケーションが HTML 応答を動的に生成するために使用するテンプレートファイル。
- **C** ontrollers: 入力方向のブラウザー要求を処理し、モデルデータを取得し、ブラウザーに応答を返すビューテンプレートを指定するクラス。

このチュートリアルシリーズでは、これらのすべての概念について説明し、それらを使用してアプリケーションを構築する方法について説明します。

まず、コントローラークラスを作成してみましょう。 **ソリューションエクスプローラー**で、 *Controllers*フォルダーを右クリックし、[**追加**]、[**コントローラー**] の順にクリックします。

![](adding-a-controller/_static/image1.png)

[ **スキャフォールディングの追加** ] ダイアログボックスで、[ **MVC 5 コントローラー-空**] をクリックし、[ **追加**] をクリックします。

![](adding-a-controller/_static/image2.png)  

新しいコントローラーに "HelloWorldController" という名前を指定し、[ **追加**] をクリックします。

![コントローラーの追加](adding-a-controller/_static/image3.png)

*HelloWorldController.cs*という名前の新しいファイルと新しいフォルダー *Views\HelloWorld*が作成されたことを**ソリューションエクスプローラー**に注意してください。 コントローラーは IDE で開かれています。

![](adding-a-controller/_static/image4.png)

このファイルの内容を次のコードに置き換えます。

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

コントローラーメソッドは HTML の文字列を例として返します。 コントローラーにはという名前が付けられ、 `HelloWorldController` 最初のメソッドにはという名前が付けられ `Index` ます。 ブラウザーから呼び出してみましょう。 アプリケーションを実行します (F5 キーを押すか、Ctrl キーを押しながら F5 キーを押します)。 ブラウザーで、HelloWorld を &quot; &quot; アドレスバーのパスに追加します。 (たとえば、次の図のようになります `http://localhost:1234/HelloWorld.` )。ブラウザーのページは次のスクリーンショットのようになります。 上記のメソッドでは、コードによって文字列が直接返されました。 HTML を返すだけでシステムに指示しました。

![](adding-a-controller/_static/image5.png)

ASP.NET MVC は、受信 URL に応じて、さまざまなコントローラークラス (およびその中のさまざまなアクションメソッド) を呼び出します。 ASP.NET MVC で使用される既定の URL ルーティングロジックでは、次のような形式を使用して、呼び出すコードを決定します。

`/[Controller]/[ActionName]/[Parameters]`

ルーティングの形式は、 *アプリの \_ Start/RouteConfig* ファイルで設定します。

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

アプリケーションを実行するときに、URL セグメントを指定しない場合、既定では、上記のコードの [既定] セクションで指定されている "Home" コントローラーと "Index" アクションメソッドが既定値になります。

URL の最初の部分では、実行するコントローラークラスを指定します。 そのため、 *HelloWorld* はクラスにマップし `HelloWorldController` ます。 URL の2番目の部分では、実行するクラスのアクションメソッドを決定します。 したがって、 */HelloWorld/Index* では、 `Index` クラスのメソッドが `HelloWorldController` 実行されます。 また、 *HelloWorld* を参照しなければならないことに注意して `Index` ください。既定では、メソッドが使用されていました。 これは、という名前のメソッド `Index` が、明示的に指定されていない場合にコントローラーで呼び出される既定のメソッドであるためです。 URL セグメントの 3 番目の部分 (`Parameters`) はルート データ用です。 ルートデータについては、このチュートリアルで後ほど説明します。

`http://localhost:xxxx/HelloWorld/Welcome` を参照します。 `Welcome`メソッドが実行され、文字列が返されます。 &quot; これはウェルカムアクションメソッドです... &quot; . 既定の MVC マッピングは `/[Controller]/[ActionName]/[Parameters]` です。 この URL では、コントローラーは `HelloWorld` で、`Welcome` がアクション メソッドです。 URL の `[Parameters]` の部分はまだ使っていません。

![](adding-a-controller/_static/image6.png)

例を少し変更して、URL からコントローラーにパラメーター情報を渡すことができるようにします (たとえば、 */HelloWorld/Welcome? name = Scott &amp; numtimes = 4*)。 `Welcome`次に示すように、2つのパラメーターを含めるようにメソッドを変更します。 このコードでは、C# の省略可能なパラメーター機能を使用して、パラメーターに値が渡されない場合に既定で1に設定する必要があることを示して `numTimes` います。

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> セキュリティに関する注意: 上記のコードでは [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) を使用して、悪意のある入力 (つまり JavaScript) からアプリケーションを保護します。 詳細については [、「方法: HTML エンコーディングを文字列に適用](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)する」を参照してください。

 アプリケーションを実行し、URL の例 () に移動し `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4` ます。 URL の `name` と `numtimes` に違う値を指定してみてください。 [ASP.NET MVC モデルバインドシステム](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)では、アドレスバーのクエリ文字列の名前付きパラメーターが、メソッドのパラメーターに自動的にマップされます。

![](adding-a-controller/_static/image7.png)

上のサンプルでは、URL セグメント ( `Parameters` ) は使用されず `name` 、 `numTimes` パラメーターとパラメーターは [クエリ文字列](http://en.wikipedia.org/wiki/Query_string)として渡されます。 ? 上記の URL の (疑問符) は区切り記号であり、クエリ文字列は次のようになります。 &amp; 文字は、クエリ文字列を区切ります。

Welcome メソッドを次のコードに置き換えます。

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

アプリケーションを実行し、次の URL を入力します。 `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`

![](adding-a-controller/_static/image8.png)

この時点で、3番目の URL セグメントがルートパラメーターと一致した場合、アクションメソッドには、 `ID.` `Welcome` `ID` メソッド内の url 指定に一致するパラメーター () が含まれ `RegisterRoutes` ます。

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

ASP.NET MVC アプリケーションでは、パラメーターをクエリ文字列として渡すよりも、ルートデータとしてパラメーターを渡す方が一般的です (上記の ID を使用した場合など)。 ルートを追加して、との両方の `name` `numtimes` パラメーターを URL のルートデータとして渡すこともできます。 *App \_ Start\RouteConfig.cs*ファイルで、"Hello" ルートを追加します。

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

アプリケーションを実行し、に移動し `/localhost:XXX/HelloWorld/Welcome/Scott/3` ます。

![](adding-a-controller/_static/image9.png)

多くの MVC アプリケーションでは、既定のルートは正常に機能します。 このチュートリアルの後半では、モデルバインダーを使用してデータを渡す方法について学習します。そのための既定のルートを変更する必要もありません。

これらの例では、コントローラーが &quot; &quot; MVC の VC 部分 (ビューとコントローラーが動作) を実行しています。 コントローラーは HTML を直接返しています。 通常、コントローラーが HTML を直接返すことはありません。これは、コードが非常に煩雑になるためです。 代わりに、通常は別のビューテンプレートファイルを使用して、HTML 応答を生成します。 次に、その方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](getting-started.md)
> [次へ](adding-a-view.md)
