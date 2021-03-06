---
title: '方法: ポリモーフィック クエリを実行する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2f05da1e-845b-4f14-83e4-c6353a850553
ms.openlocfilehash: 49e0a6b44af0729959fabf6278cc6d8ecf37a16b
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251508"
---
# <a name="how-to-execute-a-polymorphic-query"></a>方法: ポリモーフィック クエリを実行する

このトピックでは、 [OFTYPE](./language-reference/oftype-entity-sql.md)演算子を[!INCLUDE[esql](../../../../../includes/esql-md.md)]使用してポリモーフィックなクエリを実行する方法について説明します。

### <a name="to-run-the-code-in-this-example"></a>この例のコードを実行するには

1. [School モデル](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100))をプロジェクトに追加し、Entity Framework を使用するようにプロジェクトを構成します。 詳細については、「[方法 :Entity Data Model ウィザード](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))を使用します。

2. アプリケーションのコード ページで、次の `using` ステートメント (Visual Basic の場合は `Imports`) を追加します。

    [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
    [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]

3. チュートリアルの[手順に従って、階層構造の継承を持つように概念モデルを変更します。マッピング継承-階層](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716683(v=vs.100))ごとのテーブル。

## <a name="example"></a>例

次の例では、OFTYPE 演算子を使用し、`OnsiteCourses` のコレクションから `Courses` のコレクションだけを取得して表示します。

[!code-csharp[DP EntityServices Concepts#PolymorphicQuery](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#polymorphicquery)]
[!code-vb[DP EntityServices Concepts#PolymorphicQuery](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#polymorphicquery)]

## <a name="see-also"></a>関連項目

- [Entity Framework 用の EntityClient プロバイダー](entityclient-provider-for-the-entity-framework.md)
- [Entity SQL 言語](./language-reference/entity-sql-language.md)
