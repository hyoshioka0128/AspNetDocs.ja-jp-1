---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: 動的に型指定されたビューと 厳密に型指定されたビュー |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 30b84c71c86e455f15a659abf566750f1c6eea90
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702947"
---
# <a name="dynamic-v-strongly-typed-views"></a>動的に型指定されたビューと 厳密に型指定されたビュー

[Rick Anderson](https://twitter.com/RickAndMSFT)

コントローラーから ASP.NET MVC 3 のビューに情報を渡すには、次の3つの方法があります。

1. 厳密に型指定されたモデルオブジェクトとして。
2. 動的な型として (動的に使用 @model )
3. ViewBag を使用する

ここでは、動的および厳密に型指定されたビューを比較対照する、簡単な MVC 3 のブログアプリケーションを作成しました。 コントローラーは、ブログの単純なリストから開始します。

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

IndexNotStonglyTyped () メソッドを右クリックし、Razor ビューを追加します。

[![8475 NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

[厳密に **型指定されたビューを作成する** ] チェックボックスがオフになっていることを確認します。 結果のビューには、あまり多くのものが含まれていません。

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

厳密に型指定されたビューではなく、動的なを使用しているので、intellisense は役に立ちません。 完成したコードを次に示します。

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![NotStronglyTypedView_5F00_IE 6646 [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

次に、厳密に型指定されたビューを追加します。 コントローラーに次のコードを追加します。

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

まったく同じ戻り値のビュー (topBlogs) であることに注意してください。厳密に型指定されていないビューとしてを呼び出します。 *StonglyTypedIndex ()* の内側を右クリックし、[**ビューの追加**] を選択します。 今度は、 **ブログ** モデルクラスを選択し、スキャフォールディングテンプレートとして [ **List** ] を選択します。

[![5658 StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

新しいビューテンプレート内では、intellisense がサポートされています。

[![7002 [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)
