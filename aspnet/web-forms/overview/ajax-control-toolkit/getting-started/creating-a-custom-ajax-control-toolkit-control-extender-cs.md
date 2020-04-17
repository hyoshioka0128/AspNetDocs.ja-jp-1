---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: カスタム AJAX コントロール ツールキット コントロール エクステンダの作成 (C#) |マイクロソフトドキュメント
author: rick-anderson
description: カスタム エクステンダを使用すると、新しいクラスを作成しなくても、ASP.NET コントロールの機能をカスタマイズおよび拡張できます。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ac7bf71227459ab4b1e87489e1faab6dc41545b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543029"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a>カスタム AJAX Control Toolkit コントロール エクステンダーを作成する (C#)

[マイクロソフト](https://github.com/microsoft)

> カスタム エクステンダを使用すると、新しいクラスを作成しなくても、ASP.NET コントロールの機能をカスタマイズおよび拡張できます。

このチュートリアルでは、カスタム AJAX コントロール ツールキット コントロール エクステンダーを作成する方法について説明します。 TextBox にテキストを入力するときにボタンの状態を無効から有効にする、シンプルで便利な新しいエクステンダを作成します。 このチュートリアルを読んだ後、独自のコントロール エクステンダを使用して ASP.NET AJAX ツールキットを拡張できるようになります。

カスタム コントロール エクステンダは、Visual Studio または Visual Web 開発者を使用して作成できます (Visual Web 開発者の最新バージョンを使用していることを確認してください)。

## <a name="overview-of-the-disabledbutton-extender"></a>無効ボタン エクステンダーの概要

新しいコントロール エクステンダは、DisabledButton エクステンダーという名前です。 このエクステンダには、次の 3 つのプロパティがあります。

- ターゲット コントロール ID - コントロールが拡張するテキスト ボックス。
- ターゲットボタンIID - 無効または有効になっているボタン。
- 無効テキスト - ボタンに最初に表示されるテキスト。 入力を開始すると、ボタンにはボタンテキストプロパティの値が表示されます。

テキスト ボックスとボタン コントロールに無効ボタン エクステンダーをフックします。 テキストを入力する前に、ボタンは無効になっており、テキスト ボックスとボタンは次のようになります。

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

([フルサイズの画像を表示するには クリック](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png))

テキストの入力を開始すると、ボタンが有効になり、テキスト ボックスとボタンは次のようになります。

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

([フルサイズの画像を表示するには クリック](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png))

コントロール エクステンダを作成するには、次の 3 つのファイルを作成する必要があります。

- DisabledButtonExtender.cs - このファイルは、エクステンダの作成を管理し、デザイン時にプロパティを設定できるようにするサーバー側のコントロール クラスです。 また、エクステンダに設定できるプロパティも定義します。 これらのプロパティには、コードを使用して、デザイン時にアクセスし、DisableButtonBehavior.js ファイルで定義されているプロパティと一致するプロパティを一致させます。
- 無効なボタン動作.js -- このファイルは、すべてのクライアント スクリプト ロジックを追加する場所です。
- DisabledButtonDesigner.cs - このクラスは、デザイン時の機能を有効にします。 コントロール エクステンダーが Visual Studio/Visual Web 開発者デザイナーで正しく動作するようにするには、このクラスが必要です。

そのため、コントロール エクステンダは、サーバー側コントロール、クライアント側の動作、およびサーバー側のデザイナー クラスで構成されます。 これらの 3 つのファイルをすべて作成する方法については、以下のセクションで説明します。

## <a name="creating-the-custom-extender-website-and-project"></a>カスタム エクステンダ Web サイトとプロジェクトの作成

最初の手順は、Visual Studio/Visual Web 開発者でクラス ライブラリ プロジェクトと Web サイトを作成することです。 クラス ライブラリ プロジェクトでカスタム エクステンダーを作成し、Web サイトでカスタム エクステンダーをテストします。

ウェブサイトから始めましょう。 Web サイトを作成するには、次の手順に従います。

1. メニュー オプションの **[ファイル]、[ 新しい Web サイト**] を選択します。
2. **[ASP.NET Web サイト]** テンプレートを選択します。
3. 新しいウェブサイトに*名前を付ける Web サイト1.*
4. **[OK]** をクリックします。

次に、コントロール エクステンダのコードを含むクラス ライブラリ プロジェクトを作成する必要があります。

1. メニュー オプションの **[ファイル]、[追加]、[新しいプロジェクト**] の順に選択します。
2. クラス**ライブラリ**テンプレートを選択します。
3. 新しいクラス ライブラリに**CustomExtenders**という名前を付けます。
4. **[OK]** をクリックします。

これらの手順を完了すると、ソリューション エクスプローラーウィンドウは図 1 のようになります。

[![Web サイトおよびクラス ライブラリ プロジェクトを使用したソリューション](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)

**図 01**: Web サイトとクラス ライブラリ プロジェクトを含むソリューション ([フルサイズの画像を表示するには クリック](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png))

次に、必要なすべてのアセンブリ参照をクラス ライブラリ プロジェクトに追加する必要があります。

1. CustomExtenders プロジェクトを右クリックし、メニュー オプションの **[参照の追加]** を選択します。
2. [.NET] タブを選択します。
3. 次のアセンブリへの参照を追加します。

    1. System.Web.dll
    2. System.Web.Extensions.dll
    3. System.Design.dll
    4. システム.Web.エクステンション.デザイン.dll
4. [参照] タブを選択します。
5. アセンブリへの参照を追加します。 このアセンブリは、AJAX コントロール ツールキットをダウンロードしたフォルダーにあります。

これらの手順を完了すると、クラス ライブラリ プロジェクトの References フォルダーは図 2 のようになります。

[![必要な参照を含む参照フォルダ](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)

**図 02**: 参照が必須のフォルダ ([フルサイズの画像を表示する をクリック](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png))

## <a name="creating-the-custom-control-extender"></a>カスタム コントロール エクステンダの作成

クラス ライブラリができたので、エクステンダー コントロールの構築を開始できます。 カスタム エクステンダー コントロール クラスの裸のボーンから始めましょう (リスト 1 を参照)。

**リスト 1 - MyCustomExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

リスト 1 のコントロール エクステンダー クラスについて、いくつかの点が分かります。 まず、クラスが基本の ExtenderControlBase クラスから継承していることに注意してください。 すべての AJAX コントロール ツールキットエクステンダー コントロールは、この基本クラスから派生します。 たとえば、基本クラスには、各コントロール エクステンダの必須プロパティである TargetID プロパティが含まれます。

次に、このクラスには、クライアント スクリプトに関連する次の 2 つの属性が含まれていることに注意してください。

- WebResource - ファイルをアセンブリに埋め込みリソースとして含めます。
- クライアント スクリプト リソース - アセンブリからスクリプト リソースを取得します。

属性は、カスタム エクステンダーがコンパイルされるときに、アセンブリに MyControlBehavior.js JavaScript ファイルを埋め込むために使用されます。 属性は、カスタム エクステンダーが Web ページで使用されている場合にアセンブリから MyControlBehavior.js スクリプトを取得するために使用されます。

Web リソース属性とクライアントスクリプトリソース属性が機能するには、埋め込みリソースとして JavaScript ファイルをコンパイルする必要があります。 [ソリューション エクスプローラー] ウィンドウでファイルを選択し、プロパティ シートを開き、"**ビルド アクション**" プロパティに値*埋め込みリソース*を割り当てます。

コントロール エクステンダにも、ターゲット コントロールタイプ属性が含まれていることに注意してください。 この属性は、コントロール エクステンダーによって拡張されるコントロールの種類を指定するために使用されます。 リスト 1 の場合、コントロール エクステンダを使用して TextBox を拡張します。

最後に、カスタム エクステンダに MyProperty という名前のプロパティが含まれていることに注意してください。 プロパティは、エクステンダー コントロールプロパティ属性でマークされています。 GetPropertyValue() メソッドと SetPropertyValue() メソッドは、サーバー側のコントロール エクステンダーからクライアント側の動作にプロパティ値を渡すために使用されます。

先に進んで、私たちのDisabledボタンエクステンダーのコードを実装しましょう。 このエクステンダーのコードは、リスト 2 にあります。

**リスト 2 - DisabledButtonExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

リスト 2 の DisabledButton エクステンダーには、ターゲット ボタン ID と無効テキストという名前の 2 つのプロパティがあります。 プロパティに適用される ID 参照プロパティは、ボタン コントロールの ID 以外のこのプロパティを割り当てることを防ぎます。

属性は、このエクステンダーに DisabledButtonBehavior.js という名前のファイルにあるクライアント側の動作を関連付けます。 この JavaScript ファイルについては、次のセクションで説明します。

## <a name="creating-the-custom-extender-behavior"></a>カスタム エクステンダー動作の作成

コントロール エクステンダのクライアント側コンポーネントは動作と呼ばれます。 ボタンを無効にして有効にするための実際のロジックは、DisabledButton 動作に含まれています。 この動作の JavaScript コードは、リスト 3 に含まれています。

**リスト 3 - 無効なボタン.js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

リスト 3 の JavaScript ファイルには、無効なボタン動作という名前のクライアント側クラスが含まれています。 このクラスには、サーバー側のツインと同様に、ターゲット ボタン ID と無効テキストという名前の 2\_つのプロパティが含\_まれており、ターゲット ボタン\_ID/セット\_ターゲット ボタン ID を使用してアクセスし、無効なテキスト/設定無効テキストを取得できます。

initialize() メソッドは、キーアップ イベント ハンドラを動作のターゲット要素に関連付けます。 この動作に関連付けられたテキスト ボックスに文字を入力するたびに、keyup ハンドラーが実行されます。 keyup ハンドラは、動作に関連付けられた TextBox にテキストが含まれているかどうかに応じて、Button を有効または無効にします。

リスト 3 の JavaScript ファイルは、埋め込みリソースとしてコンパイルする必要があります。 [ソリューション エクスプローラー] ウィンドウでファイルを選択し、プロパティ シートを開き、"*埋め込みリソース*" プロパティを **[ビルド アクション**] プロパティに割り当てます (図 3 参照)。 このオプションは、Visual Studio と Visual Web 開発者の両方で使用できます。

[![埋め込みリソースとしての JavaScript ファイルの追加](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)

**図 03**: JavaScript ファイルを埋め込みリソースとして追加する ([フルサイズの画像を表示する をクリック](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png))

## <a name="creating-the-custom-extender-designer"></a>カスタム エクステンダー デザイナーの作成

エクステンダーを完成させるために作成する必要がある最後のクラスが 1 つあります。 リスト 4 でデザイナー クラスを作成する必要があります。 このクラスは、Visual Studio/Visual Web 開発者デザイナーでエクステンダーが正しく動作するようにするために必要です。

**リスト 4 - DisabledButtonDesigner.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

リスト 4 のデザイナーを、無効ボタン エクステンダーとデザイナー属性に関連付けます。次のように、デザイナー属性を DisabledExtender クラスに適用する必要があります。

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a>カスタム エクステンダの使用

DisabledButton コントロール エクステンダーの作成が完了したので、ASP.NETの Web サイトで使用する時間です。 まず、カスタム エクステンダをツールボックスに追加する必要があります。 次の手順に従います。

1. ソリューション エクスプローラー ウィンドウでページをダブルクリックして、ASP.NET ページを開きます。
2. ツールボックスを右クリックし、メニュー オプションの [**アイテムの選択]** を選択します。
3. [ツールボックス項目の選択] ダイアログで、CustomExtenders.dll アセンブリを参照します。
4. **[OK]ボタン**をクリックしてダイアログを閉じます。

これらの手順を完了すると、DisabledButton コントロール エクステンダーがツールボックスに表示されます (図 4 参照)。

[![ツールボックスの [無効にする] ボタン](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)

**図 04**: ツールボックス内の [無効] ボタン ([フルサイズの画像を表示する をクリック](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png)します)

次に、新しいASP.NETページを作成する必要があります。 次の手順に従います。

1. という名前の新しいASP.NET ページを作成します。
2. スクリプト マネージャーをページにドラッグします。
3. TextBox コントロールをページ上にドラッグします。
4. ボタン コントロールをページにドラッグします。
5. [プロパティ] ウィンドウで、"ボタン ID" プロパティを値<em>btnSave</em>に変更し、Text プロパティを値 [*\*保存 ]* に変更します。

標準のテキスト ボックス コントロールとボタン コントロールASP.NETページを作成しました。

次に、無効ボタン エクステンダーを使用してテキスト ボックス コントロールを拡張する必要があります。

1. エクステンダー ウィザード ダイアログを開くには、[**エクステンダーの追加**] タスク オプションを選択します (図 5 参照)。 ダイアログには、カスタムの DisabledButton エクステンダーが含まれていることに注意してください。
2. 無効ボタン エクステンダを選択し **、[OK] ボタン**をクリックします。

[![エクステンダー ウィザード ダイアログ](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)

**図 05**: エクステンダ ウィザード ダイアログ ([フルサイズの画像を表示する をクリック](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png))

最後に、無効ボタン エクステンダーのプロパティを設定できます。 TextBox コントロールのプロパティを変更することで、DisabledButton エクステンダーのプロパティを変更できます。

1. デザイナーでテキスト ボックスを選択します。
2. [プロパティ] ウィンドウで、[エクステンダー] ノードを展開します (図 6 を参照)。
3. 値を*割*り当てるに保存する、無効テキストプロパティと*値 btn保存*にプロパティに保存します。

[![エクステンダー プロパティの設定](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)

**図 06**: エクステンダープロパティの設定 ([フルサイズの画像を表示する をクリック](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png))

ページを (F5 キーを押して) 実行すると、Button コントロールは最初は無効になります。 TextBox にテキストを入力し始めるとすぐに、Button コントロールが有効になります (図 7 参照)。

[![無効ボタン エクステンダーの動作](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)

**図 07**: DisabledButton エクステンダーの動作 ([フルサイズの画像を表示する をクリック](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png))

## <a name="summary"></a>まとめ

このチュートリアルの目的は、カスタム エクステンダー コントロールを使用して AJAX コントロール ツールキットを拡張する方法を説明することです。 このチュートリアルでは、単純な DisabledButton コントロール エクステンダーを作成しました。 このエクステンダーを実装するには、無効なボタンエクステンダー クラス、無効なボタン動作の JavaScript 動作、および無効なボタンデザイナー クラスを作成します。 カスタム コントロール エクステンダを作成するときは、常に同様の手順を実行します。

> [!div class="step-by-step"]
> [前へ](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
> [次へ](get-started-with-the-ajax-control-toolkit-vb.md)
