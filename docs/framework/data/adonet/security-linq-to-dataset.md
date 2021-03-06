---
title: セキュリティ (LINQ to DataSet)
ms.date: 03/30/2017
ms.assetid: 6116b2b8-75f4-4d8b-aea6-c13e55cda50b
ms.openlocfilehash: d6f00fccb0ea2f49c19b640e31d96e575c0d48b9
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782785"
---
# <a name="security-linq-to-dataset"></a>セキュリティ (LINQ to DataSet)
このトピックでは、LINQ to DataSet のセキュリティの問題について説明します。  
  
## <a name="passing-a-query-to-an-untrusted-component"></a>信頼できないコンポーネントへのクエリの受け渡し  
 LINQ to DataSet クエリは、プログラムの1つの時点で独自に設定し、別の場所で実行できます。 このクエリは、それが定義されている場所から見えるすべての要素、たとえば、呼び出し元のメソッドが所属しているクラスのプライベート メンバーやローカル変数/引数を表すシンボルなどを参照できます。 実行時には、呼び出し元のコードから見えなくても、クエリの定義時に参照されたメンバーであれば、事実上アクセスできることになります。 クエリを実行するコードが、任意に見える要素を増やすことはできません。つまり、アクセスできる範囲を実行元のコードそのものが決めることはできません。 アクセスの範囲は、クエリがアクセスできる範囲に限定されており、そのクエリ自体を通してのみアクセスできます。  
  
 つまり、クエリへの参照をコードの別の部分に渡した場合、そのクエリを受け取ったコンポーネントが信頼され、パブリックであるか、プライベートであるかに関係なく、クエリによって参照されたすべてのメンバーに対するアクセスが許可されます。 一般に、秘密に保持する必要のある情報を公開しないように、クエリが慎重に構築されていない限り、LINQ to DataSet クエリを信頼されていないコンポーネントに渡すことはできません。  
  
## <a name="external-input"></a>外部入力  
 アプリケーションによっては (ユーザーや他の外部エージェントからの) 外部入力を受け取り、その入力内容に応じた処理を実行する場合があります。  LINQ to DataSet の場合、アプリケーションでは、外部入力に基づいて、またはクエリで外部入力を使用して、特定の方法でクエリを作成することがあります。 LINQ to DataSet クエリは、リテラルが受け入れられるすべての場所でパラメーターを受け取ります。 アプリケーションの開発者は、外部エージェントから受け取ったリテラルを直接クエリに挿入することは避け、パラメーター化クエリを使用するようにしてください。  
  
 直接、間接を問わず、ユーザーまたは外部エージェントから受け取った入力には、対象言語の構文を巧みに利用して不正なアクションを実行する内容が含まれている可能性があります。 これは、対象言語が Transact-SQL である場合、その攻撃パターンにちなんで SQL インジェクション攻撃と呼ばれます。 クエリに直接挿入されるユーザー入力を使用して、データベースのテーブルを削除したり、サービス拒否の状態を引き起こしたり、本来実行される操作を改変したりします。 LINQ to DataSet ではクエリの構成が可能ですが、オブジェクトモデルの API を使用して実行されます。 LINQ to DataSet クエリは、Transact-sql の場合と同じように、文字列操作や連結を使用して構成されるわけではなく、従来の意味では SQL インジェクション攻撃を受ける可能性がありません。  
  
## <a name="see-also"></a>関連項目

- [プログラミング ガイド](programming-guide-linq-to-dataset.md)
