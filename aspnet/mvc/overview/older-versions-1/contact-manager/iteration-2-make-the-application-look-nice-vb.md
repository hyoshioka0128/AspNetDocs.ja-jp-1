---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
title: 'イテレーション #2 – アプリケーションを見栄え良くする (VB) |マイクロソフトドキュメント'
author: rick-anderson
description: このイテレーションでは、既定の ASP.NET MVC ビュー マスター ページとカスケード スタイル シートを変更することで、アプリケーションの外観を向上させます。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f65cb436-e493-46fd-9608-384b27385aa1
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
msc.type: authoredcontent
ms.openlocfilehash: 5a97958db442c48bd696f6414f7226127984bc34
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542431"
---
# <a name="iteration-2--make-the-application-look-nice-vb"></a>繰り返し #2 – アプリケーションの外観を良くする (VB)

[マイクロソフト](https://github.com/microsoft)

[コードをダウンロード](iteration-2-make-the-application-look-nice-vb/_static/contactmanager_2_vb1.zip)

> このイテレーションでは、既定の ASP.NET MVC ビュー マスター ページとカスケード スタイル シートを変更することで、アプリケーションの外観を向上させます。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>MVC アプリケーション (VB) ASP.NET連絡先管理の構築

この一連のチュートリアルでは、最初から最後まで連絡先管理アプリケーション全体を構築します。 連絡先マネージャアプリケーションでは、連絡先の情報 (名前、電話番号、メールアドレス) を保存できます。

複数のイテレーションでアプリケーションをビルドします。 各反復処理で、アプリケーションを徐々に改善します。 この複数の反復アプローチの目的は、各変更の理由を理解できるようにすることです。

- イテレーション #1 – アプリケーションを作成します。 最初のイテレーションでは、できるだけ簡単な方法で連絡先マネージャーを作成します。 基本的なデータベース操作のサポートを追加: 作成、読み取り、更新、および削除 (CRUD) 。

- イテレーション #2 – アプリケーションを見栄えよくします。 このイテレーションでは、既定の ASP.NET MVC ビュー マスター ページとカスケード スタイル シートを変更することで、アプリケーションの外観を向上させます。

- イテレーション #3 – フォームの検証を追加します。 3 回目のイテレーションでは、基本的なフォーム検証を追加します。 必須のフォームフィールドに入力せずにフォームを送信できないようにします。 また、メールアドレスと電話番号も検証します。

- イテレーション #4 – アプリケーションを疎結合にします。 この 4 回目のイテレーションでは、いくつかのソフトウェア設計パターンを利用して、Contact Manager アプリケーションの保守と変更を容易にします。 たとえば、リポジトリ パターンと依存関係の挿入パターンを使用するようにアプリケーションをリファクタリングします。

- イテレーション #5 – 単体テストを作成します。 5 回目のイテレーションでは、単体テストを追加することで、アプリケーションの保守と変更を容易にします。 データ モデル クラスをモックし、コントローラーと検証ロジックの単体テストをビルドします。

- イテレーション #6 – テスト駆動型開発を使用します。 この 6 回目のイテレーションでは、単体テストを最初に記述し、単体テストに対してコードを記述することで、アプリケーションに新しい機能を追加します。 このイテレーションでは、連絡先グループを追加します。

- イテレーション #7 – Ajax 機能を追加します。 7 回目のイテレーションでは、Ajax のサポートを追加することで、アプリケーションの応答性とパフォーマンスを向上させます。

## <a name="this-iteration"></a>このイテレーション

このイテレーションの目的は、連絡先マネージャー アプリケーションの外観を改善することです。 現在、連絡先マネージャーは、既定のASP.NET MVC ビュー マスター ページとカスケード スタイル シートを使用します (図 1 参照)。 これらは悪く見えませんが、私は連絡先マネージャーが他のすべてのASP.NETMVCウェブサイトのように見えるようにしたくありません。 これらのファイルをカスタム ファイルに置き換える必要があります。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-2-make-the-application-look-nice-vb/_static/image1.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image1.png)

**図 01**: ASP.NET MVC アプリケーションの既定の外観 ([フルサイズの画像を表示する をクリック](iteration-2-make-the-application-look-nice-vb/_static/image2.png)します )

このイテレーションでは、アプリケーションのビジュアルデザインを改善するための 2 つのアプローチについて説明します。 まず、mvc デザイン ギャラリーASP.NETを利用して、MVC デザイン テンプレートを無料でダウンロードする方法ASP.NET説明します。 mvc デザイン ギャラリーASP.NETを使用すると、作業を行わずに本格的な Web アプリケーションを作成できます。

連絡先マネージャー アプリケーションのASP.NET MVC デザイン ギャラリーからテンプレートを使用しないことにしました。 代わりに、私はプロのデザイン会社によって作成されたカスタムデザインを持っていました。 このチュートリアルの第 2 部では、MVC デザインの最終的なASP.NETを作成するために、プロフェッショナルデザイン会社とどのように協力したかを説明します。

## <a name="the-aspnet-mvc-design-gallery"></a>ASP.NET MVC デザイン ギャラリー

ASP.NET MVC デザイン ギャラリーは、マイクロソフトが提供する無料のリソースです。 ASP.NET MVC ギャラリーは、次のアドレスにあります。

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

ASP.NET MVC デザイン ギャラリーは、ASP.NET MVC プロジェクトで使用するために特別に作成された無料の Web サイト デザインのコレクションをホストします。 デザインはコミュニティのメンバーによってアップロードされます。 ギャラリーへの訪問者は、自分の好きなデザインに投票することができます(図2参照)。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-2-make-the-application-look-nice-vb/_static/image2.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image3.png)

**図 02**: mvc デザイン ギャラリーASP.NET ([フルサイズの画像を表示する をクリック](iteration-2-make-the-application-look-nice-vb/_static/image4.png)します )

私はこのチュートリアルを書い、ギャラリーで最も人気のあるデザインは、David Hauserによって10月という名前のデザインです。 この設計は、次の手順を実行して、ASP.NET MVC プロジェクトに使用できます。

1. [**ダウンロード**] ボタンをクリックして、10 月の zip ファイルをコンピュータにダウンロードします。
2. ダウンロードした October.zip ファイルを右クリックし、[**ブロック解除**] ボタンをクリックします (図 3 参照)。
3. 10 月という名前のフォルダーにファイルを解凍します。
4. 10 月のフォルダーに含まれる DesignTemplate フォルダーからすべてのファイルを選択し、ファイルを右クリックし、メニュー オプションの**コピー**を選択します。
5. Visual Studio ソリューション エクスプローラー ウィンドウで ContactManager プロジェクト ノードを右クリックし、メニュー オプション**の [貼り付け**] を選択します (図 4 参照)。
6. Visual Studio のメニュー オプションを選択**して編集、検索と置換、クイック置換と置換** *[MyProjectName]* *を連絡先マネージャー*に置き換えます (図 5 を参照)。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-2-make-the-application-look-nice-vb/_static/image3.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image5.png)

**図 03**: Web からダウンロードしたファイルのブロックを解除する ([フルサイズの画像を表示するには クリック](iteration-2-make-the-application-look-nice-vb/_static/image6.png))

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-2-make-the-application-look-nice-vb/_static/image4.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image7.png)

**図 04**: ソリューション エクスプローラでファイルを上書きする ([フルサイズの画像を表示するにはクリック](iteration-2-make-the-application-look-nice-vb/_static/image8.png))

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-2-make-the-application-look-nice-vb/_static/image5.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image9.png)

**図 05**: [プロジェクト名] を ContactManager に置き換える ([フルサイズの画像を表示する をクリック](iteration-2-make-the-application-look-nice-vb/_static/image10.png)します )

これらの手順を完了すると、Web アプリケーションは新しいデザインを使用します。 図 6 のページは、10 月のデザインでの連絡先マネージャー アプリケーションの外観を示しています。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-2-make-the-application-look-nice-vb/_static/image6.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image11.png)

**図 06**: 10 月のテンプレートを使用した ContactManager ([フルサイズの画像を表示する をクリック](iteration-2-make-the-application-look-nice-vb/_static/image12.png)します)

## <a name="creating-a-custom-aspnet-mvc-design"></a>カスタム ASP.NET MVC デザインの作成

ASP.NET MVC デザイン ギャラリーには、さまざまなデザイン スタイルが選択されています。 ギャラリーでは、ASP.NET MVC アプリケーションの外観をカスタマイズする痛みのない方法を提供します。 そして、もちろん、ギャラリーは完全に自由であることの大きな利点を持っています。

ただし、Web サイトに完全に独自のデザインを作成する必要がある場合があります。 その場合、ウェブサイトのデザイン会社と協力することは理にかなっています。 このアプローチは、連絡先マネージャ アプリケーションの設計に使用することにしました。

イテレーション #1から Contact Manager を圧縮し、プロジェクトを設計会社に送信しました。 彼らはVisual Studioを所有していませんでしたが(恥をかきます)、それは問題を引き起こしませんでした。 Web サイトから無料でマイクロソフトのビジュアル Web 開発者[https://www.asp.net](https://www.asp.net)をダウンロードし、ビジュアル Web 開発者の連絡先マネージャー アプリケーションを開くことができた。 2、3日で、彼らは図7のデザインを作成しました。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-2-make-the-application-look-nice-vb/_static/image7.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image13.png)

**図 07**: mvc 連絡先マネージャー デザインASP.NET ([フルサイズの画像を表示する をクリック](iteration-2-make-the-application-look-nice-vb/_static/image14.png))

新しいデザインは、2 つの主なファイルで構成されました: 新しいカスケード スタイル シート ファイルと新しいビュー マスター ページ ファイル。 ビュー マスター ページには、ASP.NET MVC アプリケーションのビューのレイアウトと共有コンテンツが含まれています。 たとえば、ビュー マスター ページには、図 7 に示すヘッダー、ナビゲーション タブ、およびフッターが含まれています。 デザイン会社の新しい Site.Master ファイルを使用して、ビュー\共有フォルダの既存の Site.Master ビュー マスター ページを上書きしました。

デザイン会社はまた、新しいカスケードスタイルシートと画像のセットを作成しました。 これらの新しいファイルをコンテンツ フォルダに配置し、既存の Site.css ファイルを上書きしました。 すべての静的コンテンツは、コンテンツ フォルダに配置する必要があります。

連絡先マネージャーの新しいデザインには、連絡先を編集および削除するためのイメージが含まれていることに注意してください。 HTML アドレス帳の表の各連絡先の横に[編集]と[削除]画像が表示されます。

もともとは、HTML でレンダリングされたリンク。次のようなアクションリンク() ヘルパー:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample1.aspx)]

Html.ActionLink() メソッドはイメージをサポートしていません (このメソッドはセキュリティ上の理由からリンク テキストを HTML エンコードします)。 したがって、Html.ActionLink() への呼び出しを Url.Action() への呼び出しに置き換えました。

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample2.aspx)]

メソッドは、HTML ハイパーリンク全体をレンダリングします。 一方、Url.Action() メソッドは、&lt;&gt;タグなしで URL だけをレンダリングします。

さらに、新しいデザインには選択されたタブと未選択のタブの両方が含まれていることに注意してください。 たとえば、図 8 では、[**新しい連絡先の作成**] タブが選択され、[**連絡先**] タブは選択されていません。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-2-make-the-application-look-nice-vb/_static/image8.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image15.png)

**図 08**: 選択されたタブと選択されていないタブ ([フルサイズの画像を表示する をクリック](iteration-2-make-the-application-look-nice-vb/_static/image16.png)して )

選択したタブと選択されていないタブの両方のレンダリングをサポートするために、MenuItemHelper という名前のカスタム HTML ヘルパーを作成しました。 このヘルパー メソッドは、現在&lt;の&gt;コントローラーとアクション&lt;がヘルパーに渡されたコントローラー&gt;とアクション名に対応するかどうかに応じて、li タグまたは li class="selected" タグのいずれかをレンダリングします。 メニュー項目ヘルパーのコードは、リスト 1 に含まれています。

**リスト 1 - ヘルパー\メニューアイテムヘルパー.vb**

[!code-vb[Main](iteration-2-make-the-application-look-nice-vb/samples/sample3.vb)]

MenuItemHelper は、内部的にタグビルダー クラスを使用&lt;して&gt;li HTML タグを構築します。 TagBuilder クラスは、新しい HTML タグを構築する必要がある場合にいつでも使用できる非常に便利なユーティリティ クラスです。 属性の追加、CSS クラスの追加、ID の生成、およびタグの内部 HTML の変更を行うためのメソッドが含まれています。

## <a name="summary"></a>まとめ

このイテレーションでは、ASP.NET MVC アプリケーションのビジュアル デザインを改善しました。 最初に、ASP.NET MVC デザイン ギャラリーに導入されました。 ASP.NET MVC アプリケーションで使用できるASP.NET MVC デザイン ギャラリーから無料のデザイン テンプレートをダウンロードする方法を学習しました。

次に、既定のカスケード スタイル シート ファイルとマスター ビュー ページ ファイルを変更して、カスタム デザインを作成する方法について説明しました。 新しい設計をサポートするために、Contact Manager アプリケーションに若干の変更を加える必要がありました。 たとえば、選択されたタブと未選択のタブを表示する MenuItemHelper という名前の新しい HTML ヘルパーを追加しました。

次のイテレーションでは、検証の非常に重要なテーマに取り組みます。 ユーザーが人の姓や名などの必要な値を指定せずに新しい連絡先を作成できないように、アプリケーションに検証コードを追加します。

> [!div class="step-by-step"]
> [前へ](iteration-1-create-the-application-vb.md)
> [次へ](iteration-3-add-form-validation-vb.md)
