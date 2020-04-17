---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: アクション (VB) を作成する |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NET MVC コントローラーに新しいアクションを追加する方法について説明します。 メソッドをアクションにするための要件について説明します。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: dd651155bdb931cb8358d369b3c0c2c98abb86b2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542249"
---
# <a name="creating-an-action-vb"></a>アクションを作成する (VB)

[マイクロソフト](https://github.com/microsoft)

> ASP.NET MVC コントローラーに新しいアクションを追加する方法について説明します。 メソッドをアクションにするための要件について説明します。

このチュートリアルの目的は、新しいコントローラー アクションを作成する方法を説明することです。 アクション メソッドの要件について学習します。 また、メソッドがアクションとして公開されないようにする方法についても学習します。

## <a name="adding-an-action-to-a-controller"></a>コントローラへのアクションの追加

新しいアクションをコントローラーに追加するには、新しいメソッドをコントローラーに追加します。 たとえば、リスト 1 のコントローラには、Index() という名前のアクションと、SayHello() という名前のアクションが含まれています。 どちらのメソッドもアクションとして公開されます。

**リスト 1 - コントローラー\ホームコントローラー.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

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

コントローラ クラスでパブリック メソッドを作成する必要があり、そのメソッドをコントローラ アクションとして公開しない場合は&lt;、NonAction&gt;属性を使用してメソッドが呼び出されないようにできます。 たとえば、リスト 2 のコントローラには、NonAction&lt;&gt;属性で修飾された CompanySecrets() という名前のパブリック メソッドが含まれています。

**リスト 2 - コントローラー\ワークコントローラー.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

ブラウザーのアドレス バーに /Work/CompanySecrets と入力して CompanySecrets() コントローラー アクションを呼び出そうとすると、図 1 のエラー メッセージが表示されます。

[![非アクション メソッドの呼び出し](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)

**図 01**: NonAction メソッドの呼び出し ([フルサイズの画像を表示する をクリック](creating-an-action-vb/_static/image2.png)して)

> [!div class="step-by-step"]
> [前へ](creating-a-controller-vb.md)
> [次へ](aspnet-mvc-controllers-overview-cs.md)
