---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: ビジネス ルール検証を使用してモデルを構築する |マイクロソフトドキュメント
author: rick-anderson
description: 手順 3 では、NerdDinner アプリケーションのデータベースのクエリと更新の両方に使用できるモデルを作成する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 1a316e9051cf56cd4f1546336b334ace991c05b3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541638"
---
# <a name="build-a-model-with-business-rule-validations"></a>ビジネス ルール検証でモデルをビルドする

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、mvc 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)ASP.NETの手順 3 です。
> 
> 手順 3 では、NerdDinner アプリケーションのデータベースのクエリと更新の両方に使用できるモデルを作成する方法を示します。
> 
> mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。

## <a name="nerddinner-step-3-building-the-model"></a>NerdDinner ステップ 3: モデルの構築

モデル ビュー コント ローラー フレームワークでは、"モデル" という用語は、アプリケーションのデータを表すオブジェクトと、検証とビジネス ルールを統合する対応するドメイン ロジックを指します。 モデルは多くの点でMVCベースのアプリケーションの「心」であり、後で見るように根本的にそれの動作を駆動します。

ASP.NET MVC フレームワークは、任意のデータ アクセス テクノロジを使用してサポートし、開発者は、さまざまな豊富な .NET データ オプションからモデルを実装する選択できます: LINQ to Entities、LINQ to SQL、NHibernate、LLBLGen プロ、サブソニック、ウィルソンソーム、または単に生ADO.NETデータリーダーまたはデータセット。

NerdDinner アプリケーションでは、LINQ to SQL を使用して、データベース設計にかなり密接に対応する単純なモデルを作成し、カスタム検証ロジックとビジネス ルールを追加します。 次に、アプリケーションの残りの部分からデータ永続化の実装を抽象化するのに役立つリポジトリ クラスを実装し、簡単に単体テストを実行できるようにします。

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ to SQL は、.NET 3.5 の一部として出荷される ORM (オブジェクト リレーショナル マッパー) です。

LINQ to SQL は、コーディング対象の .NET クラスにデータベース テーブルを簡単にマップする方法を提供します。 NerdDinnerアプリケーションでは、データベース内のディナーとRSVPテーブルをディナークラスとRSVPクラスにマッピングするために使用します。 ディナーと RSVP テーブルの列は、ディナー クラスと RSVP クラスのプロパティに対応します。 各 Dinner オブジェクトと RSVP オブジェクトは、データベース内のディナーテーブルまたは RSVP テーブル内の個別の行を表します。

LINQ to SQL では、データベース データを使用して Dinner オブジェクトと RSVP オブジェクトを取得および更新するために SQL ステートメントを手動で構築する必要がなくなります。 代わりに、Dinner クラスと RSVP クラス、データベースとの間のマッピング方法、およびそれらの間の関係を定義します。 LINQ to SQL は、対話して使用するときに実行時に使用する適切な SQL 実行ロジックの生成を処理します。

VB および C# の LINQ 言語サポートを使用して、データベースから Dinner オブジェクトと RSVP オブジェクトを取得する表現力豊かなクエリを記述できます。 これにより、記述する必要があるデータ コードの量が最小限に抑え、本当にクリーンなアプリケーションを構築できます。

### <a name="adding-linq-to-sql-classes-to-our-project"></a>LINQ を SQL クラスに追加するプロジェクト

まず、プロジェクト内の [モデル] フォルダーを右クリックし、[**&gt;新しい項目の追加**] メニュー コマンドを選択します。

![](build-a-model-with-business-rule-validations/_static/image1.png)

これにより、[新しい項目の追加] ダイアログが表示されます。 "データ" カテゴリでフィルター処理し、その中の "LINQ to SQL クラス" テンプレートを選択します。

![](build-a-model-with-business-rule-validations/_static/image2.png)

「NerdDinner」という項目に名前を付け、[追加]ボタンをクリックします。 \Models ディレクトリの下に NerdDinner.dbml ファイルを追加し、LINQ to SQL オブジェクト リレーショナル デザイナーを開きます。

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>LINQ to SQL を使用したデータ モデル クラスの作成

LINQ to SQL を使用すると、既存のデータベース スキーマからデータ モデル クラスをすばやく作成できます。 これを行うには、サーバー エクスプ ローラーで NerdDinner データベースを開き、モデル化するテーブルを選択します。

![](build-a-model-with-business-rule-validations/_static/image4.png)

その後、テーブルを LINQ to SQL デザイナ画面にドラッグできます。 この場合、LINQ to SQL はテーブルのスキーマを使用して Dinner クラスと RSVP クラスを自動的に作成します (データベース テーブル列にマップするクラス プロパティを使用)。

![](build-a-model-with-business-rule-validations/_static/image5.png)

既定では、LINQ to SQL デザイナは、データベース スキーマに基づいてクラスを作成するときに、テーブル名と列名を自動的に "多元化" します。 たとえば、上記の例の "Dinners" テーブルは "Dinner" クラスになります。 このクラスの名前付けは、モデルを .NET の名前付け規則と一致させるのに役立ちます。 ただし、デザイナーが生成するクラスまたはプロパティの名前が気に入らない場合は、いつでもオーバーライドして任意の名前に変更できます。 これは、デザイナー内でエンティティ名/プロパティ名をインラインで編集するか、プロパティ グリッドを使用して変更することで行うことができます。

既定では、LINQ to SQL デザイナーはテーブルの主キー/外部キーリレーションシップも検査し、テーブルに基づいて、作成するさまざまなモデル クラス間で既定の "リレーションシップ関連付け" が自動的に作成されます。 たとえば、DINNER テーブルと RSVP テーブルを LINQ to SQL デザイナにドラッグすると、RSVP テーブルに Dinners テーブルへの外部キーが含まれているという事実に基づいて、2 つの間の一対多リレーションシップの関連付けが推定されます (これはデザイナーの矢印で示されます)。

![](build-a-model-with-business-rule-validations/_static/image6.png)

上記の関連付けにより、LINQ to SQL は、指定された RSVP に関連付けられたディナーに開発者がアクセスするために使用できる RSVP クラスに厳密に型指定された "Dinner" プロパティを追加します。 また、開発者が特定の Dinner に関連付けられている RSVP オブジェクトを取得および更新できるようにする "RSVP" コレクション プロパティを、Dinner クラスに含めるようになります。

以下に、新しい RSVP オブジェクトを作成し、それを Dinner の RSVP コレクションに追加する場合の Visual Studio 内のインテリセンスの例を示します。 LINQ to SQL が Dinner オブジェクトに "RSRAP" コレクションを自動的に追加する方法に注目してください。

![](build-a-model-with-business-rule-validations/_static/image7.png)

ディナーの RSVP コレクションに RSVP オブジェクトを追加することで、データベース内のディナーと RSVP 行の間の外部キー関係を関連付ける LINQ to SQL を指示します。

![](build-a-model-with-business-rule-validations/_static/image8.png)

デザイナーがテーブル関連付けをモデル化または名前付けする方法が気に入らない場合は、それをオーバーライドできます。 デザイナー内の関連付け矢印をクリックし、プロパティ グリッドを使用してプロパティにアクセスして、名前の変更、削除、または変更を行います。 ただし、NerdDinner アプリケーションでは、既定の関連付けルールは、構築するデータ モデル クラスに適しており、既定の動作を使用できます。

### <a name="nerddinnerdatacontext-class"></a>クラス

Visual Studio では、LINQ to SQL デザイナを使用して定義されたモデルとデータベースリレーションシップを表す .NET クラスが自動的に作成されます。 LINQ to SQL DataContext クラスは、ソリューションに追加された各 LINQ to SQL デザイナー ファイルに対しても生成されます。 LINQ to SQL クラスアイテムを "NerdDinner" と名付けたため、作成されたデータコンテキスト クラスは "NerdDinnerDataContext" と呼ばれます。 この NerdDinnerDataContext クラスは、データベースと対話する主な方法です。

NerdDinnerDataContext クラスは、データベース内でモデル化した 2 つのテーブルを表す 2 つのプロパティである "ディナー" と "RSVM" を公開します。 C# を使用して、これらのプロパティに対する LINQ クエリを記述して、データベースから Dinner オブジェクトと RSVP オブジェクトをクエリして取得できます。

次のコードは、NerdDinnerDataContext オブジェクトをインスタンス化し、それに対して LINQ クエリを実行して、将来発生する一連のディナーを取得する方法を示しています。 Visual Studio では、LINQ クエリを記述するときに完全なインテリセンスが提供され、そこから返されるオブジェクトは厳密に型指定され、インテリセンスもサポートします。

![](build-a-model-with-business-rule-validations/_static/image9.png)

Dinner オブジェクトと RSVP オブジェクトのクエリを実行できるだけでなく、NerdDinnerDataContext は、その後、Dinner オブジェクトと RSVP オブジェクトに対して行った変更を自動的に追跡します。 この機能を使用すると、明示的な SQL 更新コードを記述しなくても、簡単に変更内容をデータベースに保存できます。

たとえば、次のコードは、LINQ クエリを使用してデータベースから 1 つの Dinner オブジェクトを取得し、2 つの Dinner プロパティを更新してから、変更内容をデータベースに保存する方法を示しています。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

上記のコードの NerdDinnerDataContext オブジェクトは、取得した Dinner オブジェクトに対して行われたプロパティの変更を自動的に追跡しました。 "SubmitChanges()" メソッドを呼び出すと、データベースに対して適切な SQL "UPDATE" ステートメントが実行され、更新された値が永続化されます。

### <a name="creating-a-dinnerrepository-class"></a>ディナーリポジトリクラスの作成

小規模なアプリケーションでは、コントローラが LINQ to SQL DataContext クラスに対して直接動作し、コントローラ内に LINQ クエリを埋め込むことで問題ない場合があります。 しかし、アプリケーションが大きくなるにつれて、このアプローチは保守とテストが面倒になります。 また、複数の場所で同じ LINQ クエリを複製する可能性もあります。

アプリケーションの保守とテストを容易にする方法の 1 つは、「リポジトリ」パターンを使用することです。 リポジトリ クラスは、データ クエリと永続化ロジックをカプセル化し、アプリケーションからデータ永続化の実装の詳細を抽象化するのに役立ちます。 アプリケーション コードをクリーンにするだけでなく、リポジトリ パターンを使用すると、将来データ ストレージの実装を変更しやすくなるようになることができ、実際のデータベースを必要とせずにアプリケーションの単体テストを容易にできます。

NerdDinner アプリケーションでは、以下のシグネチャを持つ DinnerRepository クラスを定義します。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*注: この章の後半で、このクラスから IDinnerRepository インターフェイスを抽出し、コントローラーでの依存関係の注入を有効にします。まず、簡単に始め、DinnerRepository クラスを直接使用します。*

このクラスを実装するには、「モデル」フォルダーを右クリックし、**追加 -&gt;新しい項目メニュー**コマンドを選択します。 [新しい項目の追加] ダイアログで、"クラス" テンプレートを選択し、ファイルに "DinnerRepository.cs" という名前を付けます。

![](build-a-model-with-business-rule-validations/_static/image10.png)

次のコードを使用して DinnerRepository クラスを実装できます。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>DinnerRepository クラスを使用した取得、更新、挿入、および削除

DinnerRepository クラスを作成したので、次のコード例を使用して実行できる一般的なタスクを示します。

#### <a name="querying-examples"></a>クエリの例

次のコードは、DinnerID 値を使用して 1 つのディナーを取得します。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

以下のコードは、今後のすべての夕食を取得し、それらの上にループします。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>挿入と更新の例

次のコードは、2 つの新しいディナーを追加する方法を示しています。 リポジトリへの追加/変更は、"Save()" メソッドが呼び出されるまでデータベースにコミットされません。 LINQ to SQL はデータベース トランザクション内のすべての変更を自動的にラップするので、リポジトリが保存されたときにすべての変更が発生するか、変更が行われないかのどちらかになります。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

次のコードは、既存の Dinner オブジェクトを取得し、その 2 つのプロパティを変更します。 リポジトリで "Save()" メソッドが呼び出されると、変更内容がデータベースにコミットされます。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

次のコードは、ディナーを取得し、それに RSVP を追加します。 これは、LINQ to SQL が作成した Dinner オブジェクトの RSVPs コレクションを使用して行われます (データベース内の 2 つのキー間に主キー/外部キーのリレーションシップがあるため)。 この変更は、リポジトリで "Save()" メソッドが呼び出されると、新しい RSVP テーブル行としてデータベースに保存されます。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>例を削除する

次のコードは、既存の Dinner オブジェクトを取得し、削除するマークを付けます。 リポジトリで "Save()" メソッドが呼び出されると、データベースに削除がコミットされます。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>検証とビジネス ルール ロジックをモデル クラスと統合する

検証とビジネス ルール ロジックの統合は、データを処理するアプリケーションの重要な部分です。

#### <a name="schema-validation"></a>スキーマ検証

LINQ to SQL デザイナを使用してモデル クラスを定義する場合、データ モデル クラスのプロパティのデータ型は、データベース テーブルのデータ型に対応します。 たとえば、Dinners テーブルの "EventDate" 列が "datetime" の場合、LINQ to SQL で作成されるデータ モデル クラスは "DateTime" (組み込みの .NET データ型) になります。 つまり、コードから整数またはブール値を割り当てようとするとコンパイル エラーが発生し、実行時に無効な文字列型を暗黙的に変換しようとすると自動的にエラーが発生します。

LINQ to SQL は、文字列を使用する場合に SQL 値のエスケープを自動的に処理します。

#### <a name="validation-and-business-rule-logic"></a>検証とビジネス ルール ロジック

スキーマの検証は最初の手順として役立ちますが、十分なことはほとんどありません。 ほとんどの実際のシナリオでは、複数のプロパティにまたがる、コードを実行できる、多くの場合、モデルの状態を認識できる、より豊富な検証ロジックを指定する機能が必要です (たとえば、作成/更新/削除されているか、"archived" のようなドメイン固有の状態内で作成されています)。 モデル クラスに検証規則を定義して適用するために使用できるさまざまなパターンとフレームワークがあり、これに役立つ .NET ベースのフレームワークがいくつか存在します。 MVC アプリケーション内でほとんどすべてASP.NET使用できます。

NerdDinner アプリケーションの目的のために、比較的単純で単純なパターンを使用して、夕食モデル オブジェクトで IsValid プロパティと GetRuleの違反() メソッドを公開します。 IsValid プロパティは、検証とビジネス ルールがすべて有効かどうかに応じて、true または false を返します。 メソッドは、ルール エラーの一覧を返します。

プロジェクトに「部分クラス」を追加することで、ディナーモデルに IsValid と GetRule違反() を実装します。 部分クラスを使用すると、VS デザイナが管理するクラス (LINQ to SQL デザイナによって生成された Dinner クラスなど) にメソッド/プロパティ/イベントを追加し、ツールによるコードの混乱を回避できます。 プロジェクトに新しい部分クラスを追加するには、\Models フォルダーを右クリックし、[新しい項目の追加] メニュー コマンドを選択します。 その後、「新しい項目の追加」ダイアログで「クラス」テンプレートを選択し、Dinner.cs名前を付けることができます。

![](build-a-model-with-business-rule-validations/_static/image11.png)

[追加] ボタンをクリックすると、Dinner.csファイルがプロジェクトに追加され、IDE 内で開きます。 次のコードを使用して、基本的なルール/検証の実施フレームワークを実装できます。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

上記のコードに関するいくつかの注意事項:

- Dinner クラスの先頭には"partial" キーワードが付いています。
- RuleViolation クラスは、ルール違反に関する詳細を提供できる、プロジェクトに追加するヘルパー クラスです。
- Dinner.GetRule違反() メソッドを使用すると、検証とビジネス ルールが評価されます (後で実装します)。 その後、ルール エラーに関する詳細を提供する RuleViolation オブジェクトのシーケンスを返します。
- Dinner.IsValid プロパティは、Dinner オブジェクトにアクティブなルール違反があるかどうかを示す便利なヘルパー プロパティを提供します。 いつでも Dinner オブジェクトを使用して開発者が事前にチェックできます (例外は発生しません)。
- Dinner.OnValidate() 部分メソッドは、データベース内で Dinner オブジェクトが永続化される場合にいつでも通知を受け取ることができる LINQ to SQL が提供するフックです。 上記の OnValidate() 実装により、保存前にディナーにルール違反が存在しないようになります。 無効な状態の場合は例外が発生し、LINQ to SQL はトランザクションを中止します。

このアプローチは、検証とビジネス ルールを統合できる単純なフレームワークを提供します。 ここでは、以下のルールを GetRule違反() メソッドに追加してみましょう。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

C# の "利回り戻し" 機能を使用して、Rule違反のシーケンスを返します。 上記の最初の 6 つのルール チェックでは、Dinner の文字列プロパティを null または空にすることはできません。 最後のルールはもう少し興味深く、プロジェクトに追加できる PhoneValidator.IsValidNumber() ヘルパー メソッドを呼び出して、ContactPhone 番号の形式がディナーの国と一致することを確認します。

私たちは使用することができます.この電話検証サポートを実装するための NET の正規表現サポート。 以下は、国固有のRegexパターンチェックを追加することを可能にする私たちのプロジェクトに追加できる簡単なPhoneValidator実装です。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>検証およびビジネス ロジック違反の処理

以上の検証とビジネス ルール コードを追加したので、Dinner を作成または更新しようとすると、検証ロジックルールが評価され、適用されます。

開発者は、次のようなコードを記述して、Dinner オブジェクトが有効かどうかを事前に判断し、例外を発生させることなく、その中のすべての違反の一覧を取得できます。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

無効な状態で Dinner を保存しようとすると、Dinner リポジトリで Save() メソッドを呼び出したときに例外が発生します。 これは、LINQ to SQL が Dinner.OnValidate() の変更を保存する前に、自動的に Dinner.OnValidate() 部分メソッドを呼び出し、Dinner.OnValidate() にコードを追加して、ルール違反がディナーに存在する場合に例外を発生させるためです。 この例外をキャッチし、修正する違反のリストをリアクティブに取得できます。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

検証とビジネス ルールは、UI レイヤー内ではなくモデルレイヤー内に実装されるため、アプリケーション内のすべてのシナリオに適用され、使用されます。 後でビジネスルールを変更または追加し、Dinnerオブジェクトで動作するすべてのコードを尊重することができます。

アプリケーションと UI ロジック全体にこれらの変更を適用することなく、ビジネス ルールを 1 か所で柔軟に変更できる機能を持つことは、アプリケーションの適切な記述の兆候であり、MVC フレームワークが役立つ利点です。

### <a name="next-step"></a>次の手順

これで、データベースのクエリと更新の両方に使用できるモデルが作成されました。

ここでは、プロジェクトにコントローラーとビューをいくつか追加し、HTML UI エクスペリエンスを構築します。

> [!div class="step-by-step"]
> [前へ](create-a-database.md)
> [次へ](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
