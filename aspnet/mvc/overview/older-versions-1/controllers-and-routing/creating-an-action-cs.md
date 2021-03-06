---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: アクションの作成 (C#) |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NET MVC コントローラーに新しいアクションを追加する方法について説明します。 メソッドをアクションにするための要件について説明します。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: 1c1edfbab41afa58c7cb2c0d306995e9fe491c90
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542275"
---
# <a name="creating-an-action-c"></a>アクションを作成する (C#)

[マイクロソフト](https://github.com/microsoft)

> ASP.NET MVC コントローラーに新しいアクションを追加する方法について説明します。 メソッドをアクションにするための要件について説明します。

このチュートリアルの目的は、新しいコントローラー アクションを作成する方法を説明することです。 アクション メソッドの要件について学習します。 また、メソッドがアクションとして公開されないようにする方法についても学習します。

## <a name="adding-an-action-to-a-controller"></a>コントローラへのアクションの追加

新しいアクションをコントローラーに追加するには、新しいメソッドをコントローラーに追加します。 たとえば、リスト 1 のコントローラには、Index() という名前のアクションと、SayHello() という名前のアクションが含まれています。 どちらのメソッドもアクションとして公開されます。

**リスト 1 - コントローラ\ホームコントローラ.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

アクションとして宇宙に公開されるためには、メソッドは特定の要件を満たす必要があります。

- メソッドはパブリックである必要があります。
- メソッドを静的メソッドにすることはできません。
- メソッドを拡張メソッドにすることはできません。
- メソッドをコンストラクター、取得、またはセッターにすることはできません。
- メソッドにオープン ジェネリック型を指定することはできません。
- メソッドは、コントローラーの基本クラスのメソッドではありません。
- メソッドに**ref**パラメーターまたは out パラメーター**を**含めることはできません。

コントローラ アクションの戻り値の型に制限はありません。 コントローラーアクションは、文字列、DateTime、Random クラスのインスタンス、または void を返すことができます。 ASP.NET MVC フレームワークは、アクションの結果ではない戻り値の型を文字列に変換し、ブラウザーに文字列をレンダリングします。

これらの要件に違反しないメソッドをコントローラに追加すると、そのメソッドはコントローラ アクションとして公開されます。 ここで注意してください。 コントローラアクションは、インターネットに接続しているすべてのユーザーが呼び出すことができます。 たとえば、DeleteMyWebsite() コントローラ アクションを作成しないでください。

## <a name="preventing-a-public-method-from-being-invoked"></a>パブリック メソッドが呼び出されないようにする

コントローラ クラスでパブリック メソッドを作成する必要があり、そのメソッドをコントローラ アクションとして公開しない場合は、[NonAction] 属性を使用してメソッドが呼び出されないようにできます。 たとえば、リスト 2 のコントローラには、[NonAction] 属性で修飾された CompanySecrets() という名前のパブリック メソッドが含まれています。

**リスト 2 - コントローラー\ワークコントローラー.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

ブラウザーのアドレス バーに /Work/CompanySecrets と入力して CompanySecrets() コントローラー アクションを呼び出そうとすると、図 1 のエラー メッセージが表示されます。

[![非アクション メソッドの呼び出し](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)

**図 01**: NonAction メソッドの呼び出し ([フルサイズの画像を表示する をクリック](creating-an-action-cs/_static/image2.png)して)

> [!div class="step-by-step"]
> [前へ](creating-a-controller-cs.md)
> [次へ](asp-net-mvc-routing-overview-vb.md)
