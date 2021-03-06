---
title: SQL Server での安全な動的 SQL の作成
ms.date: 03/30/2017
ms.assetid: df5512b0-c249-40d2-82f9-f9a2ce6665bc
ms.openlocfilehash: c02455ba8798df1de1d52f6b4db3426d41b95daf
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791424"
---
# <a name="writing-secure-dynamic-sql-in-sql-server"></a>SQL Server での安全な動的 SQL の作成
SQL インジェクションとは、悪意のあるユーザーによって、有効な入力データの代わりに Transact-SQL ステートメントが入力されることをいいます。 この入力データが検証されずにサーバーに直接渡され、挿入されたコードがアプリケーションでそのまま実行された場合、その攻撃によってデータが破損または破壊される可能性があります。  
  
 SQL Server では、構文的に有効であれば受信したクエリがすべて実行されるため、SQL ステートメントを構成するすべてのプロシージャに対して、インジェクションに対する脆弱性をレビューする必要があります。 高いスキルを持った攻撃者は、その気になればパラメーター化されたデータでさえも操作できます。 動的 SQL を使用する場合は、必ずコマンドをパラメーター化するようにし、パラメーター値を直接クエリ文字列に追加することは避けてください。  
  
## <a name="anatomy-of-a-sql-injection-attack"></a>SQL インジェクション攻撃の分析  
 インジェクションのプロセスは、テキスト文字列を途中で終了し、新しいコマンドを追加することによって行われます。 挿入されたコマンドが実行される前に別の文字列が追加される可能性があるため、攻撃者は挿入する文字列をコメント記号 "--" で終了させます。 後続のテキストは実行時には無視されます。 セミコロン (;) 区切り記号を使用することで、複数のコマンドを挿入できます。  
  
 挿入された SQL コードが構文的に正しい限り、改ざんをプログラムによって検出するのは不可能です。 そのため、すべてのユーザー入力を検証し、使用しているサーバーで作成された SQL コマンドを実行するコードを注意深くレビューする必要があります。 検証されていないユーザー入力は決して連結しないでください。 文字列の連結は、スクリプト インジェクションの最初の段階です。  
  
 次に、有用なガイドラインを示します。  
  
- Transact-SQL ステートメントはユーザー入力から直接作成しないでください。ストアド プロシージャを使用して、ユーザー入力を検証してください。  
  
- ユーザー入力の型、長さ、形式、範囲をテストし、検証してください。 システム名をエスケープするには Transact-SQL の QUOTENAME() 関数を使用し、文字列内の任意の文字をエスケープするには REPLACE() 関数を使用します。  
  
- アプリケーションの各層に、複数層の検証を実装します。  
  
- 入力のサイズとデータ型をテストし、適切な制限を適用します。 これは、意図的なバッファー オーバーランを防ぐのに役立ちます。  
  
- 文字列変数の内容をテストし、期待値のみを許可します。 バイナリ データ、エスケープ シーケンス、およびコメント文字を含む入力は拒否します。  
  
- XML ドキュメントを扱う場合、入力時にすべてのデータをスキーマに照らして検証します。  
  
- 多層環境では、信頼済みゾーンに入ることを許可する前にすべてのデータを検証する必要があります。  
  
- ファイル名を作成するフィールドには、次の文字列を使用できません。AUX、CLOCK $、COM1 ~ COM8、CON、CONFIG $、LPT1 ~ LPT8、NUL、および PRN。  
  
- <xref:System.Data.SqlClient.SqlParameter> オブジェクトにストアド プロシージャとコマンドを組み合わせ、型チェックと長さ検証を実行します。  
  
- クライアント コードで <xref:System.Text.RegularExpressions.Regex> 式を使用して、無効な文字を排除します。  
  
## <a name="dynamic-sql-strategies"></a>動的 SQL を利用した手法  
 プロシージャ コードで動的に生成された SQL ステートメントを実行することで組み合わせ所有権を破棄すると、SQL Server は動的 SQL によりアクセスされるオブジェクトに対する呼び出し元の権限をチェックします。  
  
 SQL Server には、動的 SQL を実行するストアド プロシージャやユーザー定義関数を使用したデータ アクセスをユーザーに許可するための方法があります。  
  
- Transact-SQL EXECUTE AS 句による偽装を利用する。詳細は、[SQL Server で偽装を利用してアクセス許可をカスタマイズする](customizing-permissions-with-impersonation-in-sql-server.md)方法に関するページにあります。  
  
- 証明書を利用してストアド プロシージャに署名する。詳細は、[SQL Server でストアド プロシージャに署名する](signing-stored-procedures-in-sql-server.md)方法に関するページにあります。  
  
### <a name="execute-as"></a>EXECUTE AS  
 EXECUTE AS 句を使用すると、呼び出し元の権限が EXECUTE AS 句で指定されたユーザーの権限に置き換えられます。 入れ子になったストアド プロシージャやトリガーは、プロキシ ユーザーのセキュリティ コンテキストで実行されることに注意してください。 これにより、行レベルのセキュリティに依存するアプリケーションや監査を必要とするアプリケーションが中断されることがあります。 ユーザーの識別情報を返す関数では、最初の呼び出し元ではなく EXECUTE AS 句で指定されたユーザーが返されます。 プロシージャの実行後、または REVERT ステートメントが発行されたときにのみ、実行コンテキストが最初の呼び出し元に戻ります。  
  
### <a name="certificate-signing"></a>証明書署名  
 証明書により署名されているストアド プロシージャが実行されると、証明書ユーザーに許可される権限が呼び出し元の権限にマージされます。 実行コンテキストは変わりません。証明書ユーザーは呼び出し元の権限を借用しません。 ストアド プロシージャの署名を実装するには、いくつかの手順を実行する必要があります。 プロシージャが変更されるたびに、再度署名する必要があります。  
  
### <a name="cross-database-access"></a>複数のデータベースへのアクセス  
 動的に生成された SQL ステートメントを実行する場合、複数データベースの組み合わせ所有権は機能しません。 SQL Server では、別のデータベースのデータにアクセスするストアド プロシージャを作成し、両方のデータベースに存在する証明書でそのプロシージャに署名することによって、この制限を回避できます。 これにより、ユーザーは、データベースへのアクセス許可が付与されていなくても、そのプロシージャによって使用されるデータベース リソースにアクセスできるようになります。  
  
## <a name="external-resources"></a>外部リソース  
 詳細については、次のリソースを参照してください。  
  
|リソース|説明|  
|--------------|-----------------|  
|「[ストアド プロシージャ](/sql/relational-databases/stored-procedures/stored-procedures-database-engine)」と「[SQL インジェクション](/sql/relational-databases/security/sql-injection)」 (SQL Server オンライン ブック)|ストアド プロシージャの作成方法と SQL インジェクションのしくみについて説明します。|  
  
## <a name="see-also"></a>関連項目

- [ADO.NET アプリケーションのセキュリティ保護](../securing-ado-net-applications.md)
- [SQL Server セキュリティの概要](overview-of-sql-server-security.md)
- [SQL Server におけるアプリケーション セキュリティのシナリオ](application-security-scenarios-in-sql-server.md)
- [SQL Server でのストアド プロシージャを使用したアクセス許可の管理](managing-permissions-with-stored-procedures-in-sql-server.md)
- [SQL Server でのストアド プロシージャの署名](signing-stored-procedures-in-sql-server.md)
- [SQL Server での借用を使用したアクセス許可のカスタマイズ](customizing-permissions-with-impersonation-in-sql-server.md)
- [ADO.NET の概要](../ado-net-overview.md)
