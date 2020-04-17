---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
title: データ注釈検証コントロールを使用した検証 (C#) |マイクロソフトドキュメント
author: rick-anderson
description: データ注釈モデル バインダーを利用して、ASP.NET MVC アプリケーション内で検証を実行します。 さまざまな種類の検証コントロールの使用方法を説明します。
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 7ca8013e-9dfc-4e33-8336-cdccfd5f9414
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
msc.type: authoredcontent
ms.openlocfilehash: 28ea52b9b412431d59d7afdd1c7cce93a50a7e2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542678"
---
# <a name="validation-with-the-data-annotation-validators-c"></a>データ検証注釈コントロールの検証 (C#)

[マイクロソフト](https://github.com/microsoft)

> データ注釈モデル バインダーを利用して、ASP.NET MVC アプリケーション内で検証を実行します。 さまざまな種類の検証コントロール属性を使用し、Microsoft エンティティ フレームワークで使用する方法について説明します。

このチュートリアルでは、データ注釈検証を使用して、ASP.NET MVC アプリケーションで検証を実行する方法について説明します。 データ注釈検証コントロールを使用する利点は、クラス プロパティに 1 つ以上の属性 (Required 属性や StringLength 属性など) を追加するだけで、検証を実行できる点です。

データ注釈検証コントロールを使用する前に、データ注釈モデル バインダーをダウンロードする必要があります。 [CodePlex](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)Web サイトからデータ注釈モデル バインダーのサンプルをダウンロードするには、 ここをクリックしてください。

データ注釈モデル バインダーは Microsoft ASP.NET MVC フレームワークの公式部分ではないことを理解することが重要です。 データ注釈モデル バインダーは Microsoft ASP.NET MVC チームによって作成されましたが、Microsoft では、このチュートリアルで説明し、使用するデータ注釈モデル バインダーの公式製品サポートを提供していません。

## <a name="using-the-data-annotation-model-binder"></a>データ注釈モデル バインダーの使用

ASP.NET MVC アプリケーションでデータ注釈モデル バインダーを使用するには、まず、Microsoft.Web.Mvc.DataAnnotations.dll アセンブリと System.ComponentModel.DataAnnotations.dll アセンブリへの参照を追加する必要があります。 メニュー オプションの **[プロジェクト]、[参照の追加]** を選択します。 次に、[**参照**] タブをクリックし、データ注釈モデル バインダーのサンプルをダウンロード (および解凍) した場所を参照します (**図 1**を参照)。

[![](validation-with-the-data-annotation-validators-cs/_static/image2.png)](validation-with-the-data-annotation-validators-cs/_static/image1.png)

**図 1**: データ注釈モデル バインダーへの参照の追加 ([フルサイズの画像を表示する をクリック](validation-with-the-data-annotation-validators-cs/_static/image3.png))

アセンブリとシステム.コンポーネントモデル.データアノテーション.dll アセンブリの両方を選択し **、[OK]** ボタンをクリックします。

データ注釈モデル バインダーでは、.NET Framework サービス パック 1 に含まれる System.ComponentModel.DataAnnotations.dll アセンブリを使用することはできません。 データ注釈モデル バインダーサンプルに含まれるバージョンの System.ComponentModel.DataAnnotations.dll アセンブリを使用する必要があります。

最後に、データ注釈モデル バインダーを Global.asax ファイルに登録する必要があります。 アプリケーション Start() イベント\_ハンドラに次のコード行を追加して、\_アプリケーション Start() メソッドを次のようにします。

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample1.cs)]

このコード行は、mvc アプリケーション全体の既定のモデル バインダーとして ataAnnotationsModelBinder ASP.NET登録します。

## <a name="using-the-data-annotation-validator-attributes"></a>データ注釈検証コントロール属性の使用

データ注釈モデル バインダーを使用する場合は、検証を実行するためにバリデータ属性を使用します。 名前空間には、次の検証属性が含まれています。

- Range – プロパティの値が指定した範囲の値の間に収まっているかどうかを検証できます。
- 正規表現 – プロパティの値が指定した正規表現パターンと一致するかどうかを検証できます。
- [必須] – 必要に応じてプロパティをマークできます。
- StringLength – 文字列プロパティの最大長を指定できます。
- 検証 – すべての検証コントロール属性の基本クラス。

> [!NOTE] 
> 
> 標準の検証コントロールのいずれでも検証のニーズが満たされない場合は、基本検証属性から新しい検証属性を継承してカスタム検証属性を作成するオプションが常にあります。

**リスト 1**の Product クラスは、これらのバリデータ属性の使用方法を示しています。 [名前]、[説明]、および [単価] プロパティは必須としてマークされます。 Name プロパティには、10 文字未満の文字列長を指定する必要があります。 最後に、UnitPrice プロパティは、通貨金額を表す正規表現パターンと一致する必要があります。

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample2.cs)]

**リスト 1**: モデル\製品.cs

Product クラスは、1 つの追加属性を使用する方法を示しています。 DisplayName 属性を使用すると、プロパティがエラー メッセージに表示されるときに、プロパティの名前を変更できます。 "単価フィールドが必要です" というエラー メッセージを表示する代わりに、エラー メッセージ "価格フィールドが必要です" を表示できます。

> [!NOTE] 
> 
> 検証コントロールによって表示されるエラー メッセージを完全にカスタマイズする場合は、次のように、検証コントロールの ErrorMessage プロパティにカスタム エラー メッセージを割り当てることができます。`<Required(ErrorMessage:="This field needs a value!")>`

リスト 1 の Product クラスは **、リスト** **2**の Create() コントローラ アクションで使用できます。 このコントローラアクションは、モデルの状態にエラーが含まれる場合に[作成]ビューを再表示します。

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample3.cs)]

**リスト 2**: コントローラー\製品コントローラー.vb

最後に、**リスト 3**でビューを作成するには、Create() アクションを右クリックし、メニューオプションの **[ビューの追加]** を選択します。 Product クラスをモデル クラスとして使用して、厳密に型指定されたビューを作成します。 [ビュー コンテンツ] ドロップダウン リストから [**作成**] を選択します (**図 2**を参照)。

[![](validation-with-the-data-annotation-validators-cs/_static/image5.png)](validation-with-the-data-annotation-validators-cs/_static/image4.png)

**図2**: 作成ビューの追加

[!code-aspx[Main](validation-with-the-data-annotation-validators-cs/samples/sample4.aspx)]

**リスト 3**: ビュー\製品\作成.aspx

> [!NOTE] 
> 
> [**ビューの追加**] メニュー オプションで生成された [作成] フォームから [ID] フィールドを削除します。 Id フィールドは ID 列に対応するため、ユーザーがこのフィールドに値を入力できないようにします。

製品を作成するフォームを送信し、必須フィールドの値を入力しない場合は、**図 3**の検証エラー メッセージが表示されます。

[![](validation-with-the-data-annotation-validators-cs/_static/image7.png)](validation-with-the-data-annotation-validators-cs/_static/image6.png)

**図 3**: 必須フィールドが見つからない

無効な通貨金額を入力すると、**図 4**のエラー メッセージが表示されます。

[![](validation-with-the-data-annotation-validators-cs/_static/image9.png)](validation-with-the-data-annotation-validators-cs/_static/image8.png)

**図4**: 無効な通貨金額

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>エンティティ フレームワークでのデータ注釈検証コントロールの使用

Microsoft Entity Framework を使用してデータ モデル クラスを生成する場合は、検証コントロール属性をクラスに直接適用することはできません。 Entity Framework デザイナーはモデル クラスを生成するため、モデル クラスに加えた変更は、次にデザイナーで変更を加えた時点で上書きされます。

Entity Framework によって生成されたクラスで検証コントロールを使用する場合は、メタ データ クラスを作成する必要があります。 検証コントロールを実際のクラスに適用する代わりに、メタ データ クラスに検証コントロールを適用します。

たとえば、Entity Framework を使用して Movie クラスを作成したとします (**図 5**を参照)。 さらに、ムービータイトルとディレクターのプロパティを必要なプロパティにしたいと考えてください。 この場合は、**リスト 4**で部分クラスとメタ データ クラスを作成できます。

[![](validation-with-the-data-annotation-validators-cs/_static/image11.png)](validation-with-the-data-annotation-validators-cs/_static/image10.png)

**図 5**: エンティティ フレームワークによって生成されたムービー クラス

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample5.cs)]

**リスト4**: モデル\Movie.cs

**リスト 4**のファイルには、ムービーとムービーメタデータという名前の 2 つのクラスが含まれています。 Movie クラスは部分クラスです。 これは、DataModel.Designer.vb ファイルに含まれるエンティティ フレームワークによって生成された部分クラスに対応します。

現在、.NET フレームワークは部分的なプロパティをサポートしていません。 したがって、**リスト 4**で定義されているムービー クラスのプロパティにバリデータ属性を適用することによって、DataModel.Designer.vb ファイルで定義されているムービー クラスのプロパティに検証コントロール属性を適用する方法はありません。

ムービー部分クラスは、MovieMetaData クラスを指すメタデータ型属性で修飾されていることに注意してください。 クラスには、ムービー クラスのプロパティのプロキシ プロパティが含まれています。

検証コントロール属性は、MovieMetaData クラスのプロパティに適用されます。 タイトル、ディレクター、および日付リリースのプロパティはすべて必須プロパティとしてマークされます。 Director プロパティには、5 文字未満の文字列を割り当てる必要があります。 最後に、"日付解放日フィールドが必要です" などのエラー メッセージを表示するには、"DateReleased/日付のリリース" プロパティに "DisplayName/ 表示名" 属性が適用されます。 エラーの代わりに"日付がリリースされました" フィールドが必要です。

> [!NOTE] 
> 
> MovieMetaData クラスのプロキシ プロパティは、ムービー クラスの対応するプロパティと同じ型を表す必要はありません。 たとえば、Director プロパティは、Movie クラスの文字列プロパティと MovieMetaData クラスのオブジェクト プロパティです。

**図 6**のページは、ムービーのプロパティに無効な値を入力したときに返されるエラー メッセージを示しています。

[![](validation-with-the-data-annotation-validators-cs/_static/image13.png)](validation-with-the-data-annotation-validators-cs/_static/image12.png)

**図 6**: エンティティ フレームワークで検証コントロールを使用する ([フルサイズの画像を表示する をクリック](validation-with-the-data-annotation-validators-cs/_static/image14.png))

## <a name="summary"></a>まとめ

このチュートリアルでは、データ注釈モデル バインダーを利用して、ASP.NET MVC アプリケーション内で検証を実行する方法を学習しました。 次の手順では、Required 属性や StringLength 属性など、さまざまな種類のバリデータ属性の使用方法について説明しました。 また、Microsoft エンティティ フレームワークを使用する際にこれらの属性を使用する方法についても説明しました。

> [!div class="step-by-step"]
> [前へ](validating-with-a-service-layer-cs.md)
> [次へ](creating-model-classes-with-the-entity-framework-vb.md)
