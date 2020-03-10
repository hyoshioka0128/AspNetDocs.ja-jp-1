---
uid: web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
title: '[How Do I]: Persist the State of a User Control During a Postback | Microsoft Docs'
author: rick-anderson
description: このビデオでは、ユーザーコントロールで1つ以上のオブジェクトの状態を保持する方法を示します。 まず、ユーザーコントロールが作成されます。
ms.author: riande
ms.date: 04/02/2009
ms.assetid: d1bca4c6-838c-40f7-87ec-80bb67e483e5
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
msc.type: video
ms.openlocfilehash: c87bd6c5c993a1bde8f8a84f6d53b431e54541d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516274"
---
# <a name="how-do-i-persist-the-state-of-a-user-control-during-a-postback"></a>[操作方法]: ポストバック中にユーザーコントロールの状態を永続化する
[How Do I]: Persist the State of a User Control During a Postback

<span data-ttu-id="44f5f-104">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="44f5f-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="44f5f-105">このビデオでは、ユーザーコントロールで1つ以上のオブジェクトの状態を保持する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="44f5f-105">In this video Chris Pels shows how to persist the state of one or more objects in a user control.</span></span> <span data-ttu-id="44f5f-106">まず、ユーザーが検索のフィルター条件を指定する機能を表すユーザーコントロールが作成されます。</span><span class="sxs-lookup"><span data-stu-id="44f5f-106">First, a user control is created that represents the ability for a user to specify filter criteria for a search.</span></span> <span data-ttu-id="44f5f-107">また、フィルター情報を格納するためのコンパニオンフィルタークラスが作成されます。</span><span class="sxs-lookup"><span data-stu-id="44f5f-107">In addition, a companion Filter class is created to store the filter information.</span></span> <span data-ttu-id="44f5f-108">フィルターコントロールにはいくつかのユーザーインターフェイス要素が追加され、フィルタークラスのインスタンスに現在のフィルター情報を格納するためのメソッドとプロパティがいくつか追加されています。</span><span class="sxs-lookup"><span data-stu-id="44f5f-108">Several user interface elements are added to the filter control along with some methods and properties to store the current filter information in the Filter class instance.</span></span> <span data-ttu-id="44f5f-109">次に、RegisterRequiresControlState メソッドと関連する保存/復元メソッドを使用して、ユーザーコントロールの永続化が実装されます。</span><span class="sxs-lookup"><span data-stu-id="44f5f-109">Next, the user control persistence is implemented using the RegisterRequiresControlState method and associated Save/Restore methods.</span></span> <span data-ttu-id="44f5f-110">これらのメソッドは、ページポストバック中にフィルタークラスとそのデータのインスタンスを格納します。</span><span class="sxs-lookup"><span data-stu-id="44f5f-110">These methods store the instance of the filter class and its data during page postbacks.</span></span> <span data-ttu-id="44f5f-111">最後に、コントロールの状態の実装に複数のオブジェクトを格納する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="44f5f-111">Finally, there is a discussion of how to store multiple objects in control state implementation.</span></span>

[<span data-ttu-id="44f5f-112">&#9654;ビデオを見る (23 分)</span><span class="sxs-lookup"><span data-stu-id="44f5f-112">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-persist-the-state-of-a-user-control-during-a-postback)
