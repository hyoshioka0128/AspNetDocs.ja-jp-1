---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: MVC 実行プロセスASP.NETについて |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NET MVC フレームワークがブラウザー要求を段階的に処理する方法について説明します。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541027"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a>ASP.NET MVC 実行プロセスを理解する

[マイクロソフト](https://github.com/microsoft)

> ASP.NET MVC フレームワークがブラウザー要求を段階的に処理する方法について説明します。

MVC ベースの web アプリケーション ASP.NETへの要求は、まず HTTP モジュールである**UrlRoutingModule**オブジェクトを通過します。 このモジュールは、要求を解析してルートの選択を行います。 オブジェクト**は**、現在の要求に一致する最初のルート オブジェクトを選択します。 (ルート オブジェクトは**RouteBase**を実装するクラスで、通常は**Route**クラスのインスタンスです)。一致するルートがない場合 **、UrlRoutingModule**オブジェクトは何も行わないので、要求は通常のASP.NETまたは IIS 要求の処理にフォールバックします。

選択した**ルート**オブジェクトから **、UrlRoutingModule**オブジェクトは、**ルート**オブジェクトに関連付けられている**IRouteHandler**オブジェクトを取得します。 通常、MVC アプリケーションでは、これは**MvcRouteHandler**のインスタンスになります。 インスタンス**は****、IHttpHandler**オブジェクトを作成し、それを**渡**します。 既定では、MVC の**IHttpHandler**インスタンスは**MvcHandler**オブジェクトです。 **MvcHandler**オブジェクトは、最終的に要求を処理するコント ローラーを選択します。

> [!NOTE]
> ASP.NET MVC Web アプリケーションを IIS 7.0 で実行する場合、MVC プロジェクトにファイル名の拡張子は必要ありません。 IIS 6.0 で実行する場合は、ファイル名の拡張子 .mvc を ASP.NET ISAPI DLL に関連付ける必要があります。

モジュールとハンドラーは、ASP.NET MVC フレームワークへのエントリ ポイントです。 これらは次のアクションを実行します。

- MVC Web アプリケーションの適切なコントローラーを選択する。
- 特定のコントローラー インスタンスを取得する。
- コントローラの**Execute**メソッドを呼び出します。

MVC Web プロジェクトの実行の段階を次に示します。

- アプリケーションへの最初の要求を受け取る 

    - グローバル.asax ファイルでは、**ルート**オブジェクトが**RouteTable**オブジェクトに追加されます。
- ルーティングを実行する 

    - モジュール**は****、RouteTable**コレクション内の最初に一致する**Route**オブジェクトを使用して**RouteData**オブジェクトを作成し、そのオブジェクトを使用して**要求コンテキスト**(**IHttpContext**) オブジェクトを作成します。
- MVC 要求ハンドラーを作成する 

    - オブジェクト**は****、MvcHandler**クラスのインスタンスを作成し、**それを渡す、要求コンテキスト**インスタンスです。
- コントローラーを作成する 

    - **MvcHandler**オブジェクトは、**コント**ローラー インスタンスを作成する**IControllerFactory**オブジェクト (通常は **、クラス**のインスタンス) を識別するインスタンスを使用します。
- コント ローラーの実行 - **MvcHandler**インスタンスは、コント ローラーの**Execute**メソッドを呼び出します。 |
- アクションを呼び出す 

    - ほとんどのコントローラは、**コントローラ**の基本クラスから継承します。 コントローラーを呼び出すコント ローラーに関連付けられているコント ローラー**アクション呼び出**しオブジェクトは、呼び出すコント ローラー クラスのアクション メソッドを決定し、そのメソッドを呼び出します。
- 結果を実行する 

    - 一般的なアクション メソッドでは、ユーザー入力を受け取り、適切な応答データを準備し、結果の型を返して結果を実行します。 実行できる組み込み結果の型には、**次**のものが含**JsonResult****まれます。** **RedirectToRouteResult** **RedirectResult** **ContentResult**
