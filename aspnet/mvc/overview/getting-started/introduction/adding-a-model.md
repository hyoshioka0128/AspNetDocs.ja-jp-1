---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: モデルの追加 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 453a55bd9f16c7b33525de18bc49493d22776f47
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045118"
---
# <a name="adding-a-model"></a>モデルの追加

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

このセクションでは、データベースのムービーを管理するためのクラスをいくつか追加します。 これらのクラスは、 &quot; &quot; ASP.NET MVC アプリのモデル部分です。

[Entity Framework](https://docs.microsoft.com/ef/)と呼ばれる .NET Framework のデータアクセステクノロジを使用して、これらのモデルクラスを定義および操作します。 Entity Framework (EF と呼ばれることもあります) では、 *Code First*と呼ばれる開発パラダイムがサポートされています。 Code First を使用すると、単純なクラスを記述することによってモデルオブジェクトを作成できます。 (これらは、plain old CLR オブジェクトの POCO クラスとも呼ばれ &quot; ます &quot; )。その後、データベースをクラスからすぐに作成することができます。これにより、非常にクリーンで迅速な開発ワークフローが可能になります。 データベースを最初に作成する必要がある場合でも、このチュートリアルに従って MVC と EF アプリの開発について学習することができます。 その後、Tom Fizmakens [ASP.NET スキャフォールディング](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) チュートリアルに従うことができます。このチュートリアルでは、データベースの最初のアプローチについて説明します。

## <a name="adding-model-classes"></a>モデルクラスの追加

**ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、[**追加**]、[**クラス**] の順に選択します。

![](adding-a-model/_static/image1.png)

*クラス*名として「Movie」と入力し &quot; &quot; ます。

次の5つのプロパティをクラスに追加し `Movie` ます。

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

クラスを使用して、 `Movie` データベースのムービーを表します。 オブジェクトの各インスタンス `Movie` は、データベーステーブル内の行に対応し、クラスの各プロパティ `Movie` はテーブル内の列にマップされます。

注: system.object と関連クラスを使用するには、 [Entity Framework NuGet パッケージ](https://www.nuget.org/packages/EntityFramework/)をインストールする必要があります。 詳細な手順については、リンク先を参照してください。

同じファイルで、次のクラスを追加し `MovieDBContext` ます。

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

クラスは、 `MovieDBContext` `Movie` データベース内のクラスインスタンスのフェッチ、格納、および更新を処理する Entity Framework ムービーデータベースコンテキストを表します。 は、 `MovieDBContext` `DbContext` Entity Framework によって提供される基本クラスから派生します。

およびを参照できるようにするには、 `DbContext` `DbSet` ファイルの先頭に次のステートメントを追加する必要があり `using` ます。

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

これを行うには、using ステートメントを手動で追加するか、赤色の波線の上にマウスポインターを移動し、クリックしてクリックします。 `Show potential fixes``using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

注: 使用されていない `using` ステートメントがいくつか削除されました。 Visual Studio では、未使用の依存関係が灰色で表示されます。 灰色の依存関係をポイントし、[未使用の Using の削除] をクリックして、未使用の依存関係を削除でき `Show potential fixes` **ます。**

![](adding-a-model/_static/image3.png)

最後にモデル (MVC では M) を追加しました。 次のセクションでは、データベース接続文字列を操作します。

> [!div class="step-by-step"]
> [前へ](adding-a-view.md)
> [次へ](creating-a-connection-string.md)
