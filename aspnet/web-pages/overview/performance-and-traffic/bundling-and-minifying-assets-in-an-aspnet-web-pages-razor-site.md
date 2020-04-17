---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: ASP.NET Web ページ (Razor) サイトでアセットをバンドルおよび縮小する |マイクロソフトドキュメント
author: rick-anderson
description: バンドルと縮小は、サイトをより速くする方法です。 バンドルを使用すると、複数の JavaScript ( .js ) ファイルまたは複数のカスケード スタイル シート (..
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 2a877c1e1a06ea2357f96b37ec4ae72f9f9c9ff3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81539921"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="52bb8-104">ASP.NET Web ページ (Razor) サイトでアセットをバンドルし、小さくする</span><span class="sxs-lookup"><span data-stu-id="52bb8-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="52bb8-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="52bb8-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="52bb8-106">バンドルと縮小は、サイトをより速くする方法です。</span><span class="sxs-lookup"><span data-stu-id="52bb8-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="52bb8-107">バンドルを使用すると、複数の JavaScript (*.js*) ファイルまたは複数のカスケード スタイル シート (*.css*) ファイルを組み合わせて、一度に 1 つずつではなく、1 つの単位としてダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="52bb8-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="52bb8-108">縮小は空白を絞り出し、ダウンロードしたファイルをできるだけ小さくするために他の種類の圧縮を実行します。</span><span class="sxs-lookup"><span data-stu-id="52bb8-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="52bb8-109">ASP.NET Web ページ 2 の RC リリースでは、必要な要素を含むパッケージが Microsoft WebMatrix でまだ使用できないため、バンドルと縮小はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="52bb8-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="52bb8-110">ご不便をおかけして申し訳ありません。</span><span class="sxs-lookup"><span data-stu-id="52bb8-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="52bb8-111">パッケージは、web ページ 2 と WebMatrix 2 ASP.NETの最終リリースで利用可能になると予想されます。</span><span class="sxs-lookup"><span data-stu-id="52bb8-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
