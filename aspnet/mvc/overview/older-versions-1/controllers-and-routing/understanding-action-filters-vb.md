---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
title: アクション フィルタ (VB) について |マイクロソフトドキュメント
author: rick-anderson
description: このチュートリアルの目的は、アクション フィルターについて説明することです。 アクション フィルターは、コントローラー アクションまたはコントローラー全体に適用できる属性です。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: e83812f2-c53e-4a43-a7c1-d64c59ecf694
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
msc.type: authoredcontent
ms.openlocfilehash: 70ab564bc1217f67874090d2ae6899d9bcd743a1
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542106"
---
# <a name="understanding-action-filters-vb"></a>アクション フィルターについて理解する (VB)

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_VB.pdf)

> このチュートリアルの目的は、アクション フィルターについて説明することです。 アクション フィルターは、コントローラー アクション (またはコントローラー全体) に適用できる属性で、アクションの実行方法を変更します。

## <a name="understanding-action-filters"></a>アクション フィルタについて

このチュートリアルの目的は、アクション フィルターについて説明することです。 アクション フィルターは、コントローラー アクション (またはコントローラー全体) に適用できる属性で、アクションの実行方法を変更します。 ASP.NET MVC フレームワークには、いくつかのアクション フィルターが含まれています。

- OutputCache – このアクション フィルターは、指定された時間だけコントローラー アクションの出力をキャッシュします。
- HandleError – このアクション フィルターは、コント ローラー アクションの実行時に発生したエラーを処理します。
- [承認] – このアクション フィルターを使用すると、特定のユーザーまたはロールへのアクセスを制限できます。

独自のカスタム アクション フィルターを作成することもできます。 たとえば、カスタム認証システムを実装するためにカスタム アクション フィルターを作成する場合があります。 または、コントローラー アクションによって返されるビュー データを変更するアクション フィルターを作成する場合もあります。

このチュートリアルでは、アクション フィルターを最初から作成する方法について説明します。 アクションの処理のさまざまな段階をログに記録するログ アクション フィルターを作成、 Visual Studio の出力ウィンドウ。

### <a name="using-an-action-filter"></a>アクション フィルタの使用

アクション フィルターは属性です。 ほとんどのアクションフィルタは、個々のコントローラアクションまたはコントローラ全体に適用できます。

たとえば、リスト 1 のデータ コント ローラーは、`Index()`現在の時刻を返すという名前のアクションを公開します。 このアクションは、アクション フィルター`OutputCache`で装飾されます。 このフィルターは、アクションによって返される値を 10 秒間キャッシュします。

**リスト1 –`Controllers\DataController.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample1.vb)]

URL /Data/Index`Index()`をブラウザのアドレスバーに入力し、更新ボタンを複数回押してアクションを繰り返し呼び出すと、同じ時間が10秒間表示されます。 アクションの`Index()`出力は 10 秒間キャッシュされます (図 1 を参照)。

[![キャッシュ時間](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)

**図 01**: キャッシュタイム ([フルサイズの画像を表示する をクリック](understanding-action-filters-vb/_static/image3.png)します )

リスト 1 では、単一のアクション`OutputCache`フィルター (アクション フィルター `Index()` ) がメソッドに適用されます。 必要に応じて、同じアクションに複数のアクション フィルターを適用できます。 たとえば、 と`OutputCache``HandleError`アクション フィルターの両方を同じアクションに適用できます。

リスト 1 では`OutputCache`、アクション フィルターがアクション`Index()`に適用されます。 この属性をクラス自体に`DataController`適用することもできます。 その場合、コントローラによって公開されたアクションによって返される結果は、10 秒間キャッシュされます。

### <a name="the-different-types-of-filters"></a>さまざまな種類のフィルター

ASP.NET MVC フレームワークは、4 種類のフィルターをサポートします。

1. 承認フィルター – 属性`IAuthorizationFilter`を実装します。
2. アクション フィルター –`IActionFilter`属性を実装します。
3. 結果フィルター – 属性`IResultFilter`を実装します。
4. 例外フィルター – 属性`IExceptionFilter`を実装します。

フィルタは上記の順序で実行されます。 たとえば、承認フィルターは、アクション フィルターと例外フィルターが他のすべての種類のフィルターの後に常に実行される前に常に実行されます。

承認フィルタは、コントローラアクションの認証と承認を実装するために使用されます。 たとえば、承認フィルターは承認フィルターの例です。

アクション フィルターには、コントローラー アクションの実行前後に実行されるロジックが含まれます。 たとえば、アクション フィルターを使用して、コントローラー アクションが返すビュー データを変更できます。

結果フィルターには、ビュー結果の実行前後に実行されるロジックが含まれます。 たとえば、ビューがブラウザにレンダリングされる直前にビューの結果を変更する場合があります。

例外フィルターは、最後に実行するフィルターの種類です。 例外フィルターを使用して、コントローラーアクションまたはコントローラーアクションの結果によって発生したエラーを処理できます。 例外フィルターを使用してエラーをログに記録することもできます。

フィルタの種類ごとに、特定の順序で実行されます。 同じ種類のフィルターを実行する順序を制御する場合は、フィルターの Order プロパティを設定できます。

すべてのアクション フィルターの基本クラスは`System.Web.Mvc.FilterAttribute`クラスです。 特定の種類のフィルターを実装する場合は、基本フィルター クラスから継承し、1 つ以上の IAuthorization フィルター、IActionFilter、IResultFilter、または例外フィルター インターフェイスを実装するクラスを作成する必要があります。

### <a name="the-base-actionfilterattribute-class"></a>基本アクションフィルター属性クラス

カスタム アクション フィルターを簡単に実装できるようにするために、ASP.NET MVC フレームワークには基本`ActionFilterAttribute`クラスが含まれています。 このクラスは、 および`IActionFilter``IResultFilter`インターフェイスの両方を実装し`Filter`、クラスから継承します。

ここでの用語は完全に一貫していません。 技術的には、ActionFilterAttribute クラスから継承するクラスは、アクション フィルターと結果フィルターの両方です。 しかし、緩い意味では、単語アクションフィルターは、ASP.NETMVCフレームワーク内の任意の種類のフィルターを参照するために使用されます。

基本の ActionFilterAttribute クラスには、オーバーライドできる次のメソッドがあります。

- OnActionExecuting – このメソッドは、コントローラー アクションが実行される前に呼び出されます。
- OnActionExecuted – このメソッドは、コント ローラー アクションが実行された後に呼び出されます。
- OnResultExecuting – このメソッドは、コントローラーアクションの結果が実行される前に呼び出されます。
- OnResultExecuted – このメソッドは、コント ローラー アクションの結果が実行された後に呼び出されます。

次のセクションでは、これらの各メソッドを実装する方法を説明します。

### <a name="creating-a-log-action-filter"></a>ログ アクション フィルタの作成

カスタム アクション フィルターを作成する方法を説明するために、コントローラー アクションの処理のステージを Visual Studio の [出力] ウィンドウに記録するカスタム アクション フィルターを作成します。 リスト`LogActionFilter`2に含まれています。

**リスト2 –`ActionFilters\LogActionFilter.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample2.vb)]

リスト 2 では`OnActionExecuting()`、 `OnActionExecuted()` `OnResultExecuting()`、 `OnResultExecuted()` 、および メソッド`Log()`はすべてメソッドを呼び出します。 メソッドの名前と現在のルート データがメソッドに`Log()`渡されます。 この`Log()`メソッドは、Visual Studio の出力ウィンドウにメッセージを書き込みます (図 2 参照)。

[![[Visual Studio の出力] ウィンドウへの書き込み](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)

**図 02**: Visual Studio の出力ウィンドウへの書き込み ([フルサイズの画像を表示する をクリック](understanding-action-filters-vb/_static/image6.png)します )

リスト 3 のホーム コントローラーは、Log アクション フィルターをコントローラー クラス全体に適用する方法を示しています。 ホーム コントローラーによって公開されるアクションのいずれかが呼び出されるたびに (`Index()`メソッドまたは`About()`メソッドのいずれか)、アクションの処理のステージが Visual Studio の出力ウィンドウに記録されます。

**リスト3 –`Controllers\HomeController.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample3.vb)]

### <a name="summary"></a>まとめ

このチュートリアルでは、MVC アクション フィルターのASP.NETについて説明しました。 4 種類のフィルターについて学習しました: 承認フィルター、アクション フィルター、結果フィルター、例外フィルター。 また、基本`ActionFilterAttribute`クラスについても学習しました。

最後に、単純なアクション フィルターを実装する方法を学習しました。 コントローラー アクションの処理のステージをログに記録するログ アクション フィルターを作成、 Visual Studio の出力ウィンドウ。

> [!div class="step-by-step"]
> [前へ](asp-net-mvc-routing-overview-vb.md)
> [次へ](improving-performance-with-output-caching-vb.md)
