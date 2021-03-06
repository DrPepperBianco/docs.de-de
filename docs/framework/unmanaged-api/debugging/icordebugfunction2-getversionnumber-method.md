---
title: ICorDebugFunction2::GetVersionNumber-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugFunction2.GetVersionNumber
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugFunction2::GetVersionNumber
helpviewer_keywords:
- ICorDebugFunction2::GetVersionNumber method [.NET Framework debugging]
- GetVersionNumber method, ICorDebugFunction2 interface [.NET Framework debugging]
ms.assetid: e3a1ce48-9bb9-4ed6-a5fe-5e1819a6333f
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 16902d1a50f691ae555fdbc964bb9a1c6bf563c4
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="icordebugfunction2getversionnumber-method"></a>ICorDebugFunction2::GetVersionNumber-Methode
Ruft die Version dieser Funktion bearbeiten und fortfahren.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT GetVersionNumber (  
    [out] ULONG32   *pnVersion  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `pnVersion`  
 [out] Ein Zeiger auf eine ganze Zahl, die Versionsnummer der Funktion, die von diesem ICorDebugFunction2-Objekt dargestellt wird.  
  
## <a name="remarks"></a>Hinweise  
 Die Common Language Runtime behält den Überblick über der Anzahl der Änderungen, die jedes Modul während einer Debugsitzung stattgefunden haben. Die Versionsnummer einer Funktion ist eine weitere als die Anzahl der Bearbeitung, die die Funktion eingeführt wurde. Ursprüngliche Version der Funktion ist die Version 1. Die Zahl ist für ein Modul jedes Mal inkrementiert [ICorDebugModule2:: ApplyChanges](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule2-applychanges-method.md) für dieses Modul aufgerufen wird. Daher, wenn eine Funktion Text in der ersten und dritten Aufruf von ersetzt wurde `ICorDebugModule2::ApplyChanges`, `GetVersionNumber` gelegten Version 1, 2 oder 4 für diese Funktion, jedoch nicht Version 3. (Diese Funktion müssten keine Version 3.)  
  
 Die Versionsnummer wird für jedes Modul separat nachverfolgt. Also wenn vier Bearbeitungen für 1-Modul und keinen für Module2 ausgeführt wird, wird die nächste Bearbeitung auf Modul1 eine Versionsnummer von 6 die bearbeiteten Funktionen im Modul1 zuweisen. Wenn die gleiche Module2 Bearbeitungsvorgang, erhalten die Funktionen im Module2 eine Versionsnummer von 2.  
  
 Die Versionsnummer zu erhalten, indem die `GetVersionNumber` Methode ist möglicherweise niedriger als die von [ICorDebugFunction:: GetCurrentVersionNumber](../../../../docs/framework/unmanaged-api/debugging/icordebugfunction-getcurrentversionnumber-method.md).  
  
 Die [ICorDebugCode:: GetVersionNumber](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-getversionnumber-method.md) -Methode führt den gleichen Vorgang als `ICorDebugFunction2::GetVersionNumber`.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
