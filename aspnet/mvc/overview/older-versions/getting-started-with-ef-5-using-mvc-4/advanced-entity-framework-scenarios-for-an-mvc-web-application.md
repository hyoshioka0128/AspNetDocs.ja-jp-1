---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: MVC Web アプリケーションの高度な Entity Framework シナリオ (10/10) |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: f8f079f6d8ea663c6888456be422a2bae93a4b87
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "86163582"
---
# <a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a>MVC Web アプリケーションの高度な Entity Framework シナリオ (10/10)

[Tom Dykstra](https://github.com/tdykstra)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。 チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)をご覧ください。 チュートリアルシリーズは、最初から開始するか、[この章のスタートプロジェクトをダウンロード](building-the-ef5-mvc4-chapter-downloads.md)して開始することができます。
> 
> > [!NOTE] 
> > 
> > 解決できない問題が発生した場合は、完成した[章をダウンロード](building-the-ef5-mvc4-chapter-downloads.md)し、問題の再現を試みてください。 一般に、コードと完成したコードを比較することで、問題の解決策を見つけることができます。 一般的なエラーとその解決方法については、「[エラーと回避策](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)」を参照してください。

前のチュートリアルでは、リポジトリと作業単位パターンを実装しています。 このチュートリアルでは、次のトピックについて説明します。

- 生の SQL クエリを実行しています。
- 追跡なしのクエリを実行しています。
- データベースに送信されたクエリを検証しています。
- プロキシクラスを使用した作業
- 変更の自動検出を無効にしています。
- 変更を保存するときに検証を無効にします。
- [エラーと回避策](#errors)

これらのトピックのほとんどでは、既に作成したページを操作します。 生の SQL を使用して一括更新を行うには、データベース内のすべてのコースのクレジット数を更新する新しいページを作成します。

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

また、追跡なしのクエリを使用するには、新しい検証ロジックを Department Edit ページに追加します。

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a>生の SQL クエリの実行

Entity Framework Code First API には、SQL コマンドをデータベースに直接渡すことができるようにするメソッドが含まれています。 次のようなオプションがあります。

- エンティティ型を返すクエリに対して `DbSet.SqlQuery` メソッドを使用します。 返されるオブジェクトは、オブジェクトによって予期される型である必要があり `DbSet` ます。また、追跡をオフにしない限り、データベースコンテキストによって自動的に追跡されます。 (メソッドの詳細については、次のセクションを参照してください `AsNoTracking` )。
- エンティティでは `Database.SqlQuery` ない型を返すクエリには、メソッドを使用します。 このメソッドを使用してエンティティ型を取得する場合でも、返されるデータはデータベース コンテキストによって追跡されません。
- クエリ以外のコマンドには、 [Database.Exeのコマンド](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx)を使用します。

Entity Framework を使用する利点の 1 つは、データを格納する特定のメソッドにコードを過度に接近させなくてもよい点です。 SQL クエリとコマンドが生成されるため、自分でこれらを記述する必要がなくなります。 ただし、手動で作成した特定の SQL クエリを実行する必要がある場合は、例外的なシナリオがあります。これらのメソッドを使用すると、このような例外を処理できます。

Web アプリケーションで SQL コマンドを実行する場合は常に、SQL インジェクション攻撃から自身のサイトを保護する対策を講じる必要があります。 これを行う 1 つの方法として、パラメーター化されたクエリを使用して、Web ページによって送信された文字列が SQL コマンドとして解釈できないことを確認します。 このチュートリアルでは、ユーザー入力をクエリに統合するときに、パラメーター化されたクエリを使用します。

### <a name="calling-a-query-that-returns-entities"></a>エンティティを返すクエリの呼び出し

`GenericRepository`追加のメソッドを使用して派生クラスを作成しなくても、追加のフィルター処理と並べ替えの柔軟性をクラスに提供するとします。 これを実現する方法の1つとして、SQL クエリを受け取るメソッドを追加する方法があります。 その後、 `Where` 結合またはサブクエリに依存する句など、コントローラーで任意の種類のフィルター処理や並べ替えを指定できます。 このセクションでは、このようなメソッドを実装する方法について説明します。

`GetWithRawSql` *GenericRepository.cs*に次のコードを追加して、メソッドを作成します。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

*CourseController.cs*で、 `Details` 次の例に示すように、メソッドから新しいメソッドを呼び出します。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

この場合は、メソッドを使用することもできますが、メソッドを使用して `GetByID` メソッドが動作することを確認してい `GetWithRawSql` `GetWithRawSQL` ます。

[詳細] ページを実行して、選択クエリが機能することを確認します ([**コース**] タブを選択し、1つのコースの**詳細**を選択します)。

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>他の種類のオブジェクトを返すクエリの呼び出し

以前に、登録日ごとの学生数を示す About ページ用に、学生の統計グリッドを作成しました。 *HomeController.cs*でこれを実行するコードは、LINQ を使用します。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

LINQ を使用するのではなく、このデータを直接 SQL で取得するコードを記述するとします。 そのためには、エンティティオブジェクト以外のものを返すクエリを実行する必要があります。これは、メソッドを使用する必要があることを意味し `Database.SqlQuery` ます。

*HomeController.cs*で、メソッドの LINQ ステートメントを `About` 次のコードに置き換えます。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

[バージョン情報] ページを実行します。 以前に行ったのと同じデータが表示されます。

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a>更新クエリの呼び出し

Contoso 大学の管理者が、すべてのコースのクレジットの数を変更するなど、データベースで一括変更を実行できるようにするとします。 大学に多くのコースがある場合は、それらすべてをエンティティとして取得し、それらを個別に変更するのは非効率的です。 このセクションでは、すべてのコースのクレジット数を変更する要素をユーザーが指定できるようにする web ページを実装します。これにより、SQL ステートメントを実行して変更を行うことができ `UPDATE` ます。 Web ページは次の図のようになります。

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

前のチュートリアルでは、汎用リポジトリを使用してコントローラーのエンティティを読み取り、更新して `Course` `Course` います。 この一括更新操作では、汎用リポジトリに含まれていない新しいリポジトリメソッドを作成する必要があります。 そのためには、 `CourseRepository` クラスから派生した専用クラスを作成し `GenericRepository` ます。

*DAL*フォルダーで、 *CourseRepository.cs*を作成し、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

*UnitOfWork.cs*で、リポジトリの `Course` 種類をからに変更します。 `GenericRepository<Course>``CourseRepository:`

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

*CourseController.cs*で、メソッドを追加し `UpdateCourseCredits` ます。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

このメソッドは、との両方に使用され `HttpGet` `HttpPost` ます。 メソッドが実行されると、変数は null になり、 `HttpGet` `UpdateCourseCredits` `multiplier` 前の図に示すように、空のテキストボックスと [送信] ボタンが表示されます。

[**更新**] ボタンがクリックされ、 `HttpPost` メソッドが実行されると、 `multiplier` はテキストボックスに入力された値を持ちます。 次に、 `UpdateCourseCredits` 影響を受ける行の数を返すリポジトリメソッドを呼び出し、その値をオブジェクトに格納し `ViewBag` ます。 ビューがオブジェクトの影響を受ける行の数を受け取ると `ViewBag` 、次の図に示すように、テキストボックスと送信ボタンの代わりにその数値が表示されます。

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

[更新コースのクレジット] ページで、 *Views\Course*フォルダーにビューを作成します。

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

*Views\Course\UpdateCourseCredits.cshtml*で、テンプレートコードを次のコードに置き換えます。

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

**[Courses]\(コース\)** タブを選択してから、ブラウザーのアドレス バーで URL の末尾に "/UpdateCourseCredits" を追加して (例: `http://localhost:50205/Course/UpdateCourseCredits`)、`UpdateCourseCredits` メソッドを実行します。 テキスト ボックスに数値を入力します。

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

**[更新]** をクリックします。 影響を受けた行の数が表示されます。

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

**[リストに戻る]** をクリックして、単位数が変更されたコースの一覧を表示します。

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

未加工の SQL クエリの詳細については、Entity Framework チームのブログの「[生の Sql クエリ](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx)」を参照してください。

## <a name="no-tracking-queries"></a>追跡なしのクエリ

データベースコンテキストは、データベース行を取得し、それらを表すエンティティオブジェクトを作成するときに、既定では、メモリ内のエンティティがデータベース内のデータと同期されているかどうかを追跡します。 メモリ内のデータはキャッシュとして機能し、エンティティを更新するときに使われます。 Web アプリケーションでは、一般にコンテキスト インスタンスの存続期間は短く (要求ごとに新しいインスタンスが作成されて破棄されます)、通常、エンティティを読み取るコンテキストはエンティティが再び使われる前に破棄されるので、多くの場合、このようなキャッシュは必要ありません。

コンテキストで、メソッドを使用してクエリのエンティティオブジェクトを追跡するかどうかを指定でき `AsNoTracking` ます。 追跡を無効にした方がよい一般的なシナリオを以下に示します。

- このクエリでは、追跡を無効にする大量のデータを取得すると、パフォーマンスが著しく向上する可能性があります。
- エンティティを更新するためにアタッチする必要があるが、以前に別の目的で同じエンティティを取得した場合。 エンティティはデータベース コンテキストによって既に追跡されているため、変更するエンティティをアタッチできません。 この問題を回避する方法の1つは、 `AsNoTracking` 前のクエリでオプションを使用することです。

このセクションでは、これらのシナリオの2番目のシナリオを示すビジネスロジックを実装します。 具体的には、インストラクターが複数の部門の管理者になることができないというビジネスルールを適用します。

*DepartmentController.cs*で、メソッドとメソッドから呼び出すことができる新しいメソッドを追加し、 `Edit` `Create` 同じ管理者を持つ2つの部門がいないことを確認します。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

`try` `HttpPost` `Edit` 検証エラーがない場合に、この新しいメソッドを呼び出すために、メソッドのブロックにコードを追加します。 `try`ブロックは次の例のようになります。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

Department Edit ページを実行して、部門の管理者を、既に別の部門の管理者になっているインストラクターに変更してみてください。 次のようなエラーメッセージが表示されます。

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

ここで、Department Edit ページをもう一度実行し、今度は**予算**の金額を変更します。 [**保存**] をクリックすると、次のエラーページが表示します。

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

例外エラーメッセージは " `An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.` " です。これは、次の一連のイベントが原因で発生します。

- メソッドは、 `Edit` `ValidateOneAdministratorAssignmentPerInstructor` Kim Abercrombie を管理者として持つすべての部門を取得するメソッドを呼び出します。 これにより、英語部門が読み取られます。 この部門は編集されているので、エラーは報告されません。 ただし、この読み取り操作の結果として、データベースから読み取られた English department エンティティがデータベースコンテキストによって追跡されるようになります。
- メソッドは、 `Edit` `Modified` MVC モデルバインダーによって作成された english department エンティティにフラグを設定しようとしますが、これは失敗します。これは、コンテキストが既に英語部門のエンティティを追跡しているためです。

この問題の解決策の1つは、検証クエリによって取得されたインメモリ department エンティティをコンテキストが追跡しないようにすることです。 このような欠点はありません。これは、このエンティティを更新したり、メモリにキャッシュすることでメリットが得られるような方法でもう一度読み取ったりすることはないからです。

次に示すように、 *DepartmentController.cs*のメソッドで、 `ValidateOneAdministratorAssignmentPerInstructor` 追跡を指定しません。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

部署の**予算**額の編集を繰り返します。 この時点で操作は成功し、サイトは [学科] インデックスページに期待どおりに戻り、変更された予算値が表示されます。

## <a name="examining-queries-sent-to-the-database"></a>データベースに送信されたクエリの調査

データベースに送信される実際の SQL クエリを確認できると役立つ場合があります。 これを行うには、デバッガーでクエリ変数を確認するか、クエリのメソッドを呼び出します `ToString` 。 これを試すには、単純なクエリを見て、一括読み込み、フィルター処理、並べ替えなどのオプションを追加したときに何が起こるかを見てみましょう。

*Controllers/CourseController*で、メソッドを `Index` 次のコードに置き換えます。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

ここで、メソッドのおよびステートメントの*GenericRepository.cs*にブレークポイントを設定し `return query.ToList();` `return orderBy(query).ToList();` `Get` ます。 プロジェクトをデバッグモードで実行し、[コースのインデックス] ページを選択します。 コードがブレークポイントに到達したら、 `query` 変数を調べます。 SQL Server に送信されるクエリが表示されます。 これは単純な `Select` ステートメントです。

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.json)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

クエリが長すぎると、Visual Studio のデバッグウィンドウに表示されない場合があります。 クエリ全体を表示するには、変数の値をコピーしてテキストエディターに貼り付けます。

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

次に、ユーザーが特定の部門をフィルター処理できるように、[コースのインデックス] ページにドロップダウンリストを追加します。 コースはタイトルで並べ替えることができ、ナビゲーションプロパティの一括読み込みを指定し `Department` ます。 *CourseController.cs*で、メソッドを `Index` 次のコードに置き換えます。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

メソッドは、パラメーターのドロップダウンリストの選択された値を受け取り `SelectedDepartment` ます。 何も選択されていない場合、このパラメーターは null になります。

`SelectList`すべての部門を含むコレクションがドロップダウンリストのビューに渡されます。 コンストラクターに渡されるパラメーターは、 `SelectList` 値フィールド名、テキストフィールド名、および選択された項目を指定します。

このコードでは、リポジトリのメソッドに対して、 `Get` `Course` ナビゲーションプロパティのフィルター式、並べ替え順序、および一括読み込みを指定して `Department` います。 `true`ドロップダウンリストで何も選択されていない場合 (つまり、が null の場合)、フィルター式は常にを返し `SelectedDepartment` ます。

*Views\Course\Index.cshtml*の開始タグの直前に、 `table` ドロップダウンリストと [送信] ボタンを作成する次のコードを追加します。

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

クラスにブレークポイントを設定したまま、 `GenericRepository` Course Index ページを実行します。 最初の2回は、コードがブレークポイントにヒットして、ページがブラウザーに表示されるようにします。 ドロップダウンリストから部門を選択し、[**フィルター**] をクリックします。

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

今回は、ドロップダウンリストの部門クエリの最初のブレークポイントになります。 これをスキップし、 `query` 次にコードがブレークポイントに到達したときに変数を表示して、クエリがどのように見えるかを確認し `Course` ます。 次のような内容が表示されます。

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.json)]

クエリが `JOIN` `Department` データと共にデータを読み込み `Course` 、句を含むクエリであることがわかります `WHERE` 。

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a>プロキシクラスの使用

Entity Framework がエンティティインスタンスを作成するとき (たとえば、クエリの実行時)、エンティティのプロキシとして機能する動的に生成された派生型のインスタンスとして作成されることがよくあります。 このプロキシは、プロパティにアクセスしたときにアクションを自動的に実行するフックを挿入するために、エンティティの一部の仮想プロパティをオーバーライドします。 たとえば、このメカニズムは、リレーションシップの遅延読み込みをサポートするために使用されます。

ほとんどの場合、このプロキシの使用を意識する必要はありませんが、例外があります。

- 場合によっては、Entity Framework がプロキシインスタンスを作成できないようにする必要があります。 たとえば、プロキシインスタンスをシリアル化するよりも、プロキシ以外のインスタンスをシリアル化する方が効率的な場合があります。
- 演算子を使用してエンティティクラスをインスタンス化する場合 `new` 、プロキシインスタンスは取得されません。 これは、遅延読み込みや自動変更追跡などの機能を利用できないことを意味します。 これは通常は問題ありません。通常、遅延読み込みは必要ありません。これは、データベースに存在しない新しいエンティティを作成しているためです。また、エンティティをとして明示的にマークしている場合は、通常、変更の追跡は必要ありません `Added` 。 ただし、遅延読み込みが必要で、変更の追跡が必要な場合は、クラスのメソッドを使用して、プロキシを使用して新しいエンティティインスタンスを作成でき `Create` `DbSet` ます。
- プロキシ型から実際のエンティティ型を取得することもできます。 クラスのメソッドを使用して、 `GetObjectType` `ObjectContext` プロキシ型のインスタンスの実際のエンティティ型を取得できます。

詳細については、Entity Framework チームのブログの「[プロキシの操作](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx)」を参照してください。

## <a name="disabling-automatic-detection-of-changes"></a>変更の自動検出を無効にする

Entity Framework では、エンティティの現在の値と元の値を比較して、エンティティがどのように変更されたか (およびそれによって、どの更新プログラムをデータベースに送信する必要があるか) を判断します。 元の値は、エンティティが照会またはアタッチされたときに格納されます。 変更の自動検出を行うメソッドには、次のようなものがあります。

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

多数のエンティティを追跡していて、これらのメソッドのいずれかをループ内で何度も呼び出す場合、 [autodetection の有効な](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx)プロパティを使用して自動変更検出を一時的に無効にすると、パフォーマンスが大幅に向上する可能性があります。 詳細については、「[変更を自動的に検出](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx)する」を参照してください。

## <a name="disabling-validation-when-saving-changes"></a>変更を保存するときに検証を無効にする

メソッドを呼び出すと、 `SaveChanges` 既定では、Entity Framework は、データベースを更新する前に、変更されたすべてのエンティティのすべてのプロパティのデータを検証します。 多数のエンティティを更新していて、既にデータを検証している場合、この作業は不要であり、変更の保存プロセスを一時的に無効にすることによって時間を短縮することができます。 これは、 [Validateonsaveenabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx)プロパティを使用して行うことができます。 詳細については、「[検証](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx)」を参照してください。

## <a name="summary"></a>まとめ

これで、ASP.NET MVC アプリケーションでの Entity Framework の使用に関するこの一連のチュートリアルは完了です。 その他の Entity Framework リソースへのリンクについては、「 [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。

Web アプリケーションを構築した後にデプロイする方法の詳細については、MSDN ライブラリの「 [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx) 」を参照してください。

認証や承認など、MVC に関連するその他のトピックについては、 [mvc の推奨リソース](../../getting-started/recommended-resources-for-mvc.md)を参照してください。

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a>謝辞

- Tom Dykstra は、このチュートリアルの元のバージョンを記述し、Microsoft Web Platform and Tools コンテンツチームのシニアプログラミングライターです。
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT) ) はこのチュートリアルを共同で作成し、ほとんどの作業を EF 5 および MVC 4 用に更新しました。 Rick は、Microsoft が Azure と MVC に注力するシニアプログラミングライターです。
- [Rowan](http://www.romiller.com) Entity Framework チームの他のメンバーがコードレビューを支援し、EF 5 のチュートリアルを更新している間に発生した移行に関する多くの問題のデバッグを支援しました。

## <a name="vb"></a>VB

このチュートリアルを最初に作成したときに、完成したダウンロードプロジェクトの C# バージョンと VB バージョンの両方を提供しました。 この更新により、各章の C# ダウンロード可能なプロジェクトを提供して、シリーズのどこからでも簡単に開始できるようになりますが、時間制限やその他の優先順位により、VB では実行されませんでした。 これらのチュートリアルを使用して VB プロジェクトをビルドし、他のユーザーと共有したい場合は、お知らせください。

<a id="errors"></a>

## <a name="errors-and-workarounds"></a>エラーと回避策

### <a name="cannot-createshadow-copy"></a>作成/シャドウコピーできません

エラー メッセージ:

*このファイルが既に存在する場合は、' DotNetOpenAuth ' を作成/シャドウコピーできません。*

解決方法 :

数秒待ってから、ページを更新してください。

### <a name="update-database-not-recognized"></a>更新-データベースを認識できません

エラー メッセージ:

*"データベースの更新" という用語は、コマンドレット、関数、スクリプトファイル、または操作可能なプログラムの名前として認識されません。名前の綴りを確認するか、パスが含まれている場合は、パスが正しいことを確認してから、もう一度やり直してください。*(PMC の *`Update-Database`* コマンドから)

解決方法 :

Visual Studio を終了します。 プロジェクトを再度開き、もう一度やり直してください。

### <a name="validation-failed"></a>検証に失敗しました

エラー メッセージ:

*1つ以上のエンティティの検証に失敗しました。詳細については、' EntityValidationErrors ' プロパティを参照してください。* (PMC の *`Update-Database`* コマンドから)

解決方法 :

この問題の原因の1つは、メソッドの実行時の検証エラーです `Seed` 。 メソッドのデバッグに関するヒントについては、「 [Entity Framework (EF) db のシード処理とデバッグ](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)」を参照してください `Seed` 。

### <a name="http-50019-error"></a>HTTP 500.19 エラー

エラー メッセージ:

*HTTP エラー 500.19-内部サーバーエラーページの関連する構成データが無効なため、要求されたページにアクセスできません。*

解決方法 :

このエラーを発生させる1つの方法は、ソリューションの複数のコピーを保持し、それぞれが同じポート番号を使用することです。 通常、この問題を解決するには、Visual Studio のすべてのインスタンスを終了し、作業中のプロジェクトを再起動します。 それでもうまくいかない場合は、ポート番号を変更してみてください。 プロジェクトファイルを右クリックし、[プロパティ] をクリックします。 [ **Web** ] タブを選択し、[**プロジェクトの Url** ] テキストボックスでポート番号を変更します。

### <a name="error-locating-sql-server-instance"></a>SQL Server インスタンスの位置を特定しているときのエラー

エラー メッセージ:

*SQL Server への接続の確立中に、ネットワーク関連またはインスタンス固有のエラーが発生しました。サーバーが見つからなかったか、アクセスできませんでした。インスタンス名が正しいこと、および SQL Server がリモート接続を許可するように構成されていることを確認してください。(プロバイダー: SQL ネットワークインターフェイス、エラー:26-指定されたサーバー/インスタンスの検索でエラーが発生しました)*

解決方法 :

接続文字列を確認してください。 データベースを手動で削除した場合は、構築文字列内のデータベースの名前を変更します。

> [!div class="step-by-step"]
> [前へ](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
> [次へ](building-the-ef5-mvc4-chapter-downloads.md)
