---
title: ICorDebugProcess::GetHelperThreadID-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugProcess.GetHelperThreadID
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugProcess::GetHelperThreadID
helpviewer_keywords:
- GetHelperThreadID method [.NET Framework debugging]
- ICorDebugProcess::GetHelperThreadID method [.NET Framework debugging]
ms.assetid: 84e1e605-37c1-49a5-8e12-35db85654622
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 03e801cb58b8f5c3f658085fcee4288278e545c5
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="icordebugprocessgethelperthreadid-method"></a>ICorDebugProcess::GetHelperThreadID-Methode
Ruft das Betriebssystem (BS)-Thread-ID des internen Hilfsthreads des Debuggers an.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT GetHelperThreadID (  
    [out] DWORD *pThreadID  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `pThreadID`  
 [out] Ein Zeiger auf das Betriebssystem thread-ID des internen Hilfsthreads des Debuggers.  
  
## <a name="remarks"></a>Hinweise  
 Beim Debuggen von verwaltetem und nicht verwaltetem ist es der Debugger dafür verantwortlich, um sicherzustellen, dass der Thread mit der angegebenen ID weiterhin ausgeführt wird, wenn sie einen Haltepunkt vom Debugger platziert erreichen. Ein Debugger kann auch dieses Threads vom Benutzer ausblenden möchten. Wenn keine Hilfs-Thread im Prozess noch vorhanden ist die `GetHelperThreadID` Methodenrückgabe 0 (null) in *`pThreadID`.  
  
 Die Thread-ID des Threads Hilfsprogramm kann nicht zwischengespeichert werden, da er im Laufe der Zeit ändern kann. Sie müssen das Thread-ID bei jeder Stopping-Ereignis erneut abfragen.  
  
 Die Thread-ID, Hilfsthreads des Debuggers wird auf korrekt sein, jede nicht verwaltete [ICorDebugManagedCallback:: CreateThread](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-createthread-method.md) Ereignis, sodass einen Debugger bestimmen die Thread-ID seines Hilfsthreads und vom Benutzer zu verbergen. Ein Thread, der als Hilfsthread, während ein nicht verwaltetes identifiziert wird `ICorDebugManagedCallback::CreateThread` Ereignis verwalteter Benutzercode nie ausgeführt.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl. CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
