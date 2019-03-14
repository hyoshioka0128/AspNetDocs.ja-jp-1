---
title: ASP.NET Core でのキーの管理
author: rick-anderson
description: ASP.NET Core データ保護キー管理 Api の実装の詳細について説明します。
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/key-management
ms.openlocfilehash: 431bdf2d3076c83279b78f327ddb647f69e6e584
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042579"
---
# <a name="key-management-in-aspnet-core"></a>ASP.NET Core でのキーの管理

<a name="data-protection-implementation-key-management"></a>

データ保護システムは、自動的に保護し、ペイロードの保護を解除するために使用するマスター _ キーの有効期間を管理します。 各キーは、4 つの段階のいずれかで存在できます。

* 作成したキーをキー リング内に存在するが認証されていません。 キーの使用できません新しい保護操作十分な時間が経過するまで、キーがこのキー リングを使用しているすべてのマシンに反映されるまでの可能性を持っています。

* アクティブな - キーはキー リング内に存在して、すべての新しい保護操作のために使用する必要があります。

* キーは、有効期限切れ - 自然な有効期間にわたって実行し、保護操作では使用できなくする必要があります。

* 失効のキーが侵害され、新しい保護操作には使用しないでください。

受信したペイロードを解除するために、作成された、アクティブ、および有効期限が切れたキーをすべてに使用する可能性があります。 既定では失効したキーが、ペイロードを解除するために使用できませんが、アプリケーション開発者は[この動作をオーバーライド](xref:security/data-protection/consumer-apis/dangerous-unprotect#data-protection-consumer-apis-dangerous-unprotect)必要な場合。

>[!WARNING]
> 開発者は、(例: ファイル システムから対応するファイルを削除する) をキー リングからキーを削除したくなるかもしれません。 その時点では、キーによって保護されているすべてのデータが完全に解読し、失効したキーであるような緊急のオーバーライドはありません。 、本当に破壊的な動作は、キーの削除と、その結果、データ保護システムを公開しませんファーストクラス API この操作を実行するためです。

## <a name="default-key-selection"></a>既定のキーの選択

データ保護システムでは、バックアップ リポジトリからキー リングを読み取り、ときに、"default"キーをキー リングから検出を試みます。 既定のキーは、新しい保護操作に使用されます。

一般的なヒューリスティックは、データ保護システムは、既定のキーとして、最新のアクティブ化日付のキーを選択します。 (はサーバー間のクロックのずれを許可する一種の小さな) です。かどうか、アプリケーションが無効になっていない自動とキーの生成、キーが期限切れか失効してかどうかは、即時のライセンス認証ごとに新しいキーが生成されます、[キーの有効期限とローリング](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management-expiration)以下のポリシー。

新しいキーの生成を新しいキーの前にアクティブ化されたすべてのキーの有効期限が暗黙の型として扱うことが別のキーへのフォールバックするのではなく、データ保護システム理由がすぐに新しいキーを生成します。 一般的な考え方は、新しいキーが異なるアルゴリズムまたはより古いキーは、保存時の暗号化メカニズムで構成されている、システムは、フォールバックより現在の構成を優先する必要がありますです。

例外が発生します。 アプリケーション開発者が[自動キーの生成を無効になっている](xref:security/data-protection/configuration/overview#disableautomatickeygeneration)、データ保護システムは、既定のキーとして何かを選択する必要があります。 このフォールバックのシナリオでは、システムは、クラスター内の他のコンピューターに反映されるまでの時間があるキーに指定された基本設定、最新のライセンス認証日、失効していないキーを選択します。 その結果、既定の有効期限が切れたキーを選択すること、フォールバック システムになります。 フォールバック システムは既定のキーと失効したキーを選択しないでくださいとキー リングが空か、すべてのキーが失効している場合は、システムが初期化時にエラーが発生します。

<a name="data-protection-implementation-key-management-expiration"></a>

## <a name="key-expiration-and-rolling"></a>キーの有効期限とロール

キーが作成されるをアクティブ化する日の {0} 現在 + 2 日} と {現在 + 90 日間} の有効期限の日付が提供されて自動的に。 アクティブ化する前に 2 日間の遅延は、キーに反映されるまで、システム時刻を示します。 つまり、強まることキー リングが反映されることになるはアクティブなときにする必要があるすべてのアプリケーションを使用して、その確率で、[次へ] の自動更新期間、キーを観察するその他のアプリケーション、バッキング ストアをポイントできます。

2 日以内の既定のキーを有効期限が切れると、既定のキーの期限切れ時にアクティブになるキーをキー リングを持っていない場合は、新しいキーをキー リングが自動的にデータ保護システムに保持します。 この新しいキーについては、アクティブ化する日の既定のキーの有効期限日} と {現在 + 90 日間} の有効期限の日付。 これにより、サービスの中断することなくが定期的にキーを自動的にロールバックするシステムです。

ある可能性がありますの状況で即時のライセンス認証キーが作成される場所。 1 つの例は、時間、アプリケーションが実行されていないし、キー リング内のすべてのキーが期限切れになります。 この場合、キーには、通常 2 日間のアクティブ化の待機時間なしの {0} には現在} のアクティブ化日付が与えられます。

これが次の例のようには構成可能な既定キーの有効期間が 90 日間です。

```csharp
services.AddDataProtection()
       // use 14-day lifetime instead of 90-day lifetime
       .SetDefaultKeyLifetime(TimeSpan.FromDays(14));
```

明示的に呼び出す場合、管理者は、システム全体の既定値を変更もできます`SetDefaultKeyLifetime`システム全体のポリシーよりも優先されます。 既定キーの有効期間は 7 日間より短くすることはできません。

## <a name="automatic-key-ring-refresh"></a>キー リングを自動更新

データ保護システムでは、初期化時にキー リングを基になるリポジトリから読み取るし、メモリにキャッシュします。 このキャッシュは、保護と保護の解除の操作をバッキング ストアにアクセスせずに続行を許可します。 システムでは、約 24 時間ごと、または現在の既定のキーの有効期限、先に達したときに、変更のバッキング ストアは自動的にチェックします。

>[!WARNING]
> 場合は、開発者が非常にまれには、キーの管理 Api を直接使用する必要があります。 データ保護システムは前述のように、自動キー管理を実行します。

データ保護システム インターフェイスを公開する`IKeyManager`を使用して、検査し、キー リングを変更することができます。 インスタンスを提供する DI システム`IDataProtectionProvider`のインスタンスを指定できますも`IKeyManager`の使用量に対する。 また、プルすることができます、`IKeyManager`から直接、`IServiceProvider`次の例のようにします。

すべての操作 (新しいキーを明示的に作成または失効を実行する) のキー リングを変更するには、メモリ内キャッシュが無効になります。 次回の呼び出し`Protect`または`Unprotect`により、データ保護システムをキー リングを読み込んで、キャッシュを再作成します。

次の例では、使用方法を示します、`IKeyManager`インターフェイスを検査して取り消しの既存のキーと新しいキーを手動で生成するなど、キー リングを操作します。

[!code-csharp[](key-management/samples/key-management.cs)]

## <a name="key-storage"></a>キー ストレージ

データ保護システムでは、ヒューリスティックを適切なキー記憶域の場所と保存時の暗号化メカニズムを自動的に推定しようとすることがあります。 キーの永続化メカニズムでは、アプリ開発者によって構成も。 次のドキュメントでは、これらのメカニズムのボックスでの実装について説明します。

* <xref:security/data-protection/implementation/key-storage-providers>
* <xref:security/data-protection/implementation/key-encryption-at-rest>