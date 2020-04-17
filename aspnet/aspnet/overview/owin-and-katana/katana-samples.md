---
uid: aspnet/overview/owin-and-katana/katana-samples
title: 片方のサンプル |マイクロソフトドキュメント
author: rick-anderson
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 15cc1084b16db2619f2295ee21dec4f49eb2e354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540442"
---
# <a name="katana-samples"></a>Katana サンプル

[マイクロソフト](https://github.com/microsoft)

## <a name="katana-samples"></a>Katana サンプル

**ASP.NETルートサンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
アプリケーションによっては、Asp.Netルート テーブル内の OWIN コンポーネントを非 OWIN コンポーネントと並べてフックする必要があります。 このサンプルでは、ルートコレクション拡張メソッドを使用する方法を示しています。

**分岐パイプラインのサンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
OWIN 要求処理パイプラインは線形である必要はありません。 このサンプルでは、要求パスまたはヘッダーなどの他の要求データに基づいて分岐パイプラインを構築する方法を示します。 これらのコンポーネントは、Microsoft.Owin.Mapping の nuget パッケージで使用できます。

**カスタム サーバー サンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)   
OWIN を自己ホストする場合にカスタム OWIN サーバーを使用する方法を示します。

**埋め込みサンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)  
OWIN サーバーの中には、独自のプロセス (&quot;自己ホスト&quot;型 ) の内部で実行できるものもあります。 このサンプルでは、Microsoft.Owin.Hosting の nuget パッケージによって提供されるツールを使用して OWIN アプリケーションを起動する方法を示します。

**ハローワールドサンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN は、さまざまなサーバー間でアプリケーションの移植性を可能にする HTTP サーバー API の抽象化です。 このサンプルでは、生の OWIN 抽象化を単純**なラッパー**で使用して Hello World アプリケーションを作成し、ASP.NETのような Web サーバー上で実行する方法を示します。

**ハローワールド生のOWINサンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
このサンプルでは、**生**の OWIN 抽象化を使用して Hello World アプリケーションを作成し、Asp.Netのような Web サーバー上で実行する方法を示します。

**SignalR サンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
OWIN /カタナを使用して SignalR を自己ホストする方法を示します。 自己ホスト型 SignalR について詳しくは、「[チュートリアル: SignalR セルフ ホスト](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)」を参照してください。

**静的ファイルのサンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)   
OWIN / Katana を使用して静的ファイルの HTTP 要求をサポートする方法について説明します。

**Web API** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)   
このサンプルでは、IIS で OWIN をホストし、OWIN パイプラインに Web API を追加する方法を示します。

**Web ソケットサンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)   
クラスを使用して OWIN で Web[ソケットをサポートする方法を示します](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)。
