---
title: ICLRDataTarget::SetThreadContext メソッド
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.SetThreadContext
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::SetThreadContext
helpviewer_keywords:
- SetThreadContext method, ICLRDataTarget interface [.NET Framework debugging]
- ICLRDataTarget::SetThreadContext method [.NET Framework debugging]
ms.assetid: 103c8502-81fe-40d7-9c1e-9008d8fb19e1
topic_type:
- apiref
ms.openlocfilehash: cceafc8358ce2b0eafa62a3855c4eb1e96adae11
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73113311"
---
# <a name="iclrdatatargetsetthreadcontext-method"></a>ICLRDataTarget::SetThreadContext メソッド
ターゲットプロセス内の指定されたスレッドの現在のコンテキストを設定します。 このメソッドは、共通言語ランタイム (CLR) データアクセスサービスによって呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetThreadContext (  
    [in] ULONG32            threadID,  
    [in] ULONG32            contextSize,  
    [in, size_is(contextSize)]   
         BYTE               *context  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `threadID`  
 からターゲットプロセス内のスレッドのオペレーティングシステム識別子。  
  
 `contextSize`  
 からコンテキストのサイズ。  
  
 `context`  
 からコンテキストを格納しているバッファーへのポインター。  
  
 `context` バッファー内のデータは、Win32 `CONTEXT` 構造の形式になります。 コンテキストはプロセッサ固有のレジスタデータを指定するため、Win32 `CONTEXT` 構造体の定義は、プロセッサのアーキテクチャによって異なります。 Win32 `CONTEXT` 構造の定義については、Winnt.h ヘッダーファイルを参照してください。  
  
## <a name="remarks"></a>Remarks  
 このメソッドは、デバッグ アプリケーションの作成者によって実装されます。  
  
## <a name="requirements"></a>［要件］  
 **:** 「[システム要件](../../../../docs/framework/get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ClrData .idl, ClrData .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRDataTarget インターフェイス](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget-interface.md)
