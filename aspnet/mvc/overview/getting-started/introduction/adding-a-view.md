---
title: MVC アプリへのビューの追加
author: Rick-Anderson
description: MVC アプリへのビューの追加
ms.author: riande
ms.date: 01/23/2019
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: b8400036cc689d3cd2fec54b3191252d296ade41
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045014"
---
# <a name="adding-a-view"></a>ビューの追加

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

このセクションでは、 `HelloWorldController` ビューテンプレートファイルを使用して、クライアントへの HTML 応答を生成するプロセスを完全にカプセル化するようにクラスを変更します。 

[Razor ビューエンジン](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md)を使用して、ビューテンプレートファイルを作成します。 Razor ベースのビューテンプレートには *、1つ* のファイル拡張子が付いており、C# を使用して HTML 出力を作成するための洗練された方法を提供します。 Razor では、ビューテンプレートを記述するときに必要な文字数とキーストロークの数が最小限に抑えられ、滑らかなコーディングワークフローが可能になります。

現在、`Index` メソッドは、コントローラー クラスでハード コーディングされるメッセージを含む文字列を返します。 次の `Index` コードに示すように、Controllers [ビュー](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View) メソッドを呼び出すようにメソッドを変更します。

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

上記のメソッドは、 `Index` ビューテンプレートを使用してブラウザーへの HTML 応答を生成します。 上記のメソッドなどのコントローラーメソッド ( [アクションメソッド](http://rachelappel.com/asp.net-mvc-actionresults-explained)とも呼ばれます) は、 `Index` 通常、文字列のようなプリミティブ型ではなく、 [actionresult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (または [actionresult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)から派生したクラス) を返します。

*Views\HelloWorld*フォルダーを右クリックして [**追加**] をクリックし、[ **MVC 5 ビューページ (レイアウト (Razor))**] をクリックします。
  
![](adding-a-view/_static/image1.png)   
  
[ **項目の名前の指定** ] ダイアログボックスで、「 *Index*」と入力し、[ **OK**] をクリックします。  
  
![](adding-a-view/_static/image2.png)  
  
[**レイアウトページの選択**] ダイアログで、既定の** \_ レイアウト**をそのまま使用し、[ **OK]** をクリックします。  
  
![](adding-a-view/_static/image3.png)  
  
上のダイアログボックスの左側のウィンドウで、 *Views\Shared* フォルダーが選択されています。 カスタムレイアウトファイルが別のフォルダーにある場合は、それを選択できます。 このチュートリアルでは、後でレイアウトファイルについて説明します。

*MvcMovie\Views\HelloWorld\Index.cshtml*ファイルが作成されます。

![](adding-a-view/_static/image4.png)

次の強調表示されたマークアップを追加します。

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

*Index. cshtml*ファイルを右クリックし、[**ブラウザーで表示**] を選択します。

![PI](adding-a-view/_static/image5.png)

また、*インデックスの cshtml*ファイルを右クリックし、[ **Page Inspector で表示**] を選択することもできます。 詳細については、 [Page Inspector チュートリアル](../../views/using-page-inspector-in-aspnet-mvc.md) を参照してください。

または、アプリケーションを実行し、 `HelloWorld` コントローラー () を参照し `http://localhost:xxxx/HelloWorld` ます。 `Index`コントローラーのメソッドは多くの作業を行いませんでした。ステートメントを実行するだけです。これにより、 `return View()` メソッドがビューテンプレートファイルを使用してブラウザーに応答を表示するように指定されています。 使用するビューテンプレートファイルの名前を明示的に指定していないので、ASP.NET MVC では、\Views\HelloWorld フォルダー内の*\Views\HelloWorld*ファイルを使用するように既定で設定されてい*ます。* 下の画像は、ビューテンプレートの Hello という文字列を示して &quot; &quot; います。ビューにハードコーディングされています。

![](adding-a-view/_static/image6.png)

すばらしいですね。 ただし、ブラウザーのタイトルバーに "Index-My ASP.NET Application" と表示され、ページの上部にある大きなリンクに "アプリケーション名" と表示されていることに注意してください。 ブラウザーウィンドウのサイズによっては、右上にある3つのバーをクリックして、[ **ホーム**]、[ **バージョン情報**]、 **[連絡先**]、[ **登録** ]、[ **ログイン** ] のリンクを表示することが必要になる場合があります。

## <a name="changing-views-and-layout-pages"></a>ビューおよびレイアウトページの変更

最初に、 &quot; &quot; ページの上部にある [アプリケーション名] リンクを変更します。 このテキストは、すべてのページに共通です。 実際には、アプリケーション内のすべてのページに表示される場合でも、プロジェクト内の1つの場所にのみ実装されます。 **ソリューションエクスプローラー**の [ */* ]/[共有] フォルダーにアクセスし、[ * \_ Layout* ] ファイルを開きます。 このファイルは *レイアウトページ* と呼ばれ、他のすべてのページで使用される共有フォルダーにあります。

![_LayoutCshtml](adding-a-view/_static/image7.png)

[レイアウト] テンプレートでは、1 か所でサイトの HTML コンテナー レイアウトを指定し、それをサイト内の複数のページに適用できます。 `@RenderBody()` という行を見つけます。 `RenderBody` は、作成したビュー固有のページがすべて表示されるプレースホルダーで、レイアウト ページに&quot;ラップ&quot;されます。 たとえば、 **About** リンクを選択すると、 *Views\Home\About.cshtml* ビューがメソッド内に表示され `RenderBody` ます。

タイトル要素の内容を変更します。 レイアウトテンプレートの [html.actionlink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) を [ &quot; アプリケーション名] から &quot; [MVC ムービー] に変更し、 &quot; コントローラーをからに変更し &quot; `Home` `Movies` ます。 完全なレイアウトファイルを次に示します。

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

アプリケーションを実行し、[MVC Movie] と表示されていることを確認し &quot; &quot; ます。 [ **About** ] リンクをクリックすると、そのページに MVC ムービーが表示されていること &quot; がわかり &quot; ます。 レイアウトテンプレートで変更を1回行って、サイトのすべてのページに新しいタイトルを反映させることができました。

![](adding-a-view/_static/image8.png)

最初に *Views\HelloWorld\Index.cshtml* ファイルを作成したときに、次のコードが含まれていました。

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

上記の Razor コードでは、レイアウトページが明示的に設定されています。 *ビュー \\ _ViewStart*を調べます。このファイルには、まったく同じ Razor マークアップが含まれています。 *[ビュー \\ _ViewStart](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* は、すべてのビューで使用される共通レイアウトを定義します。したがって、 *Views\HelloWorld\Index.cshtml*ファイルからコメントアウトまたは削除することができます。

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

`Layout` プロパティを使用すれば、別のレイアウト ビューを設定することができます。また、`null` に設定して、レイアウト ファイルが使用されないようにすることができます。

次に、インデックスビューのタイトルを変更してみましょう。

*MvcMovie\Views\HelloWorld\Index.cshtml*を開きます。 2つの場所で変更を行うことができます。最初に、ブラウザーのタイトルに表示されるテキスト、次にセカンダリヘッダー ( `<h2>` 要素) で構成します。 これを少し変えれば、コードのどの部分でアプリのどの部分が変更されるかを確認することができます。

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

表示する HTML タイトルを指定するために、上記のコードではオブジェクトのプロパティを設定してい `Title` `ViewBag` ます (これは、 *インデックスの cshtml* ビューテンプレートに含まれています)。 レイアウトテンプレート ( *Views\Shared \\ _Layout* ) は、 `<title>` 以前に変更した HTML のセクションの一部として、要素内のこの値を使用することに注意して `<head>` ください。

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

この方法を使用 `ViewBag` すると、ビューテンプレートとレイアウトファイルの間で、他のパラメーターを簡単に渡すことができます。

アプリケーションを実行します。 ブラウザーのタイトル、プライマリ見出し、およびセカンダリ見出しが変更されていることに注意してください (ブラウザーに変更内容が表示されない場合は、キャッシュされたコンテンツを表示している可能性があります。 ブラウザーで Ctrl キーを押しながら F5 キーを押して、サーバーからの応答を強制的に読み込みます。)ブラウザーのタイトルは、 `ViewBag.Title` *Index. cshtml* view テンプレートで設定したと、 &quot; &quot; レイアウトファイルに追加されたムービーアプリで作成されます。

また、*インデックスの cshtml*ビューテンプレートの内容が、 * \_ Layout*ビューテンプレートにマージされ、1つの HTML 応答がブラウザーに送信されたことにも注目してください。 レイアウト テンプレートを使用すれば、アプリケーションのすべてのページに適用される変更をとても簡単に行うことができます。

![](adding-a-view/_static/image9.png)

しかし、このような少しの &quot; データ &quot; (この例では、 &quot; ビューテンプレート! message から Hello &quot; ) はハードコーディングされています。 MVC アプリケーションには &quot; V &quot; (ビュー) がありますが、 &quot; C &quot; (コントローラー) はありますが、 &quot; M &quot; (モデル) はまだありません。 ここでは、データベースを作成し、そこからモデルデータを取得する方法について説明します。

## <a name="passing-data-from-the-controller-to-the-view"></a>コントローラーからビューへのデータの受け渡し

データベースにアクセスしてモデルについて説明する前に、まずコントローラーからビューに情報を渡す方法について説明します。 コントローラークラスは、受信 URL 要求に応答して呼び出されます。 コントローラークラスは、入力方向のブラウザー要求を処理し、データベースからデータを取得し、最終的にブラウザーに返す応答の種類を決定するコードを記述します。 これで、ビューテンプレートをコントローラーから使用して、ブラウザーに HTML 応答を生成して書式設定することができます。

コントローラーは、ビューテンプレートがブラウザーに応答を表示するために必要なすべてのデータまたはオブジェクトを提供する役割を担います。 ベストプラクティス: **ビューテンプレートでは、ビジネスロジックを実行したり、データベースを直接操作したりしないで**ください。 代わりに、ビューテンプレートは、コントローラーによって提供されるデータでのみ機能します。 この &quot; 問題の分離 &quot; を維持することで、コードをクリーンで、テストしやすく、保守しやすくなります。

現在、 `Welcome` クラスのアクションメソッドは、パラメーターとパラメーターを受け取り、 `HelloWorldController` `name` `numTimes` ブラウザーに直接値を出力します。 コントローラーがこの応答を文字列として表示するのではなく、ビューテンプレートを使用するようにコントローラーを変更してみましょう。 このビュー テンプレートでは動的応答が生成されます。これは、応答を生成するために、コントローラーからビューに適量のデータを渡す必要があることを意味します。 これを行うには、ビューテンプレートに必要な動的データ (パラメーター) を、ビューテンプレートで `ViewBag` アクセスできるオブジェクトに配置します。

*HelloWorldController.cs*ファイルに戻り、メソッドを変更し `Welcome` て、 `Message` オブジェクトにとの値を追加し `NumTimes` `ViewBag` ます。 `ViewBag` は動的オブジェクトであるため、任意のものを自由に配置できます。 `ViewBag` オブジェクトには、その中に何かを配置するまで定義されたプロパティはありません。 [ASP.NET MVC モデルバインドシステム](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)は、 `name` `numTimes` アドレスバーのクエリ文字列からメソッドのパラメーターに、名前付きパラメーター (と) を自動的にマップします。 完全な *HelloWorldController.cs* ファイルは次のようになります。

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

これで、オブジェクトには `ViewBag` 、自動的にビューに渡されるデータが含まれるようになりました。 次に、ウェルカムビューテンプレートが必要です。 [ **ビルド** ] メニューの [ **ソリューションのビルド** ] (または Ctrl + Shift + B) を選択して、プロジェクトがコンパイルされていることを確認します。 *Views\HelloWorld*フォルダーを右クリックして [**追加**] をクリックし、[ **MVC 5 ビューページ (レイアウト (Razor))**] をクリックします。
  
![](adding-a-view/_static/image10.png)   
  
[ **項目の名前の指定** ] ダイアログボックスで、「 *ようこそ*」と入力し、[ **OK**] をクリックします。   
  
[**レイアウトページの選択**] ダイアログで、既定の** \_ レイアウト**をそのまま使用し、[ **OK]** をクリックします。  
  
![](adding-a-view/_static/image11.png)   

*MvcMovie\Views\HelloWorld\Welcome.cshtml*ファイルが作成されます。

*Welcome*ファイル内のマークアップを置き換えます。 ここでは、ユーザーが必要としている &quot; 回数だけ Hello というループを作成し &quot; ます。 次に、完全な *Welcome* ファイルを示します。

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

アプリケーションを実行し、次の URL を参照します。

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

これで、データは URL から取得され、 [モデルバインダー](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)を使用してコントローラーに渡されます。 コントローラーは、データをオブジェクトにパッケージ化 `ViewBag` し、そのオブジェクトをビューに渡します。 ビューには、データが HTML としてユーザーに表示されます。

![](adding-a-view/_static/image12.png)

上記のサンプルでは、オブジェクトを使用し `ViewBag` て、コントローラーからビューにデータを渡していました。 チュートリアルの後半で、ビュー モデルを使用して、コントローラーからビューにデータを渡します。 データを渡すビューモデルのアプローチは、一般にビューバッグアプローチよりもはるかに優先されます。 詳細については、「 [Dynamic V 厳密に型指定](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) されたビュー」のブログエントリを参照してください。 

それは、 &quot; モデルの M の一種で &quot; あり、データベースの種類ではありませんでした。 学習したことを確認し、ムービーのデータベースを作成してみましょう。

> [!div class="step-by-step"]
> [前へ](adding-a-controller.md)
> [次へ](adding-a-model.md)
