---
title: ICorProfilerInfo::GetILToNativeMapping-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo.GetILToNativeMapping
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerInfo::GetILToNativeMapping
helpviewer_keywords:
- GetILToNativeMapping method, ICorProfilerInfo interface [.NET Framework profiling]
- ICorProfilerInfo::GetILToNativeMapping method [.NET Framework profiling]
ms.assetid: 6a5431ef-22fb-4e53-bac5-703986297eb1
topic_type: apiref
caps.latest.revision: "20"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 89ccfcbf69a0d3907ec244d7a214d6f4a5766767
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="icorprofilerinfogetiltonativemapping-method"></a>ICorProfilerInfo::GetILToNativeMapping-Methode
Ruft für den in der angegebenen Funktion enthaltenen Code eine Zuordnung von MSIL-Offsets (Microsoft Intermediate Language) zu systemeigenen Offsets ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT GetILToNativeMapping(  
    [in] FunctionID functionId,  
    [in] ULONG32 cMap,  
    [out] ULONG32 *pcMap,  
    [out, size_is(cMap), length_is(*pcMap)]  
        COR_DEBUG_IL_TO_NATIVE_MAP map[]);  
```  
  
#### <a name="parameters"></a>Parameter  
 `functionId`  
 [in] Die ID der Funktion, die den Code enthält.  
  
 `cMap`  
 [in] Die maximale Größe des `map`-Arrays.  
  
 `pcMap`  
 [out] Die Gesamtanzahl verfügbarer COR_DEBUG_IL_TO_NATIVE_MAP-Strukturen.  
  
 `map`  
 [out] Ein Array von `COR_DEBUG_IL_TO_NATIVE_MAP`-Strukturen, die jeweils die Offsets angeben. Nach Rückgabe der `GetILToNativeMapping`-Methode enthält `map` einige oder alle `COR_DEBUG_IL_TO_NATIVE_MAP`-Strukturen.  
  
## <a name="remarks"></a>Hinweise  
 Die `GetILToNativeMapping`-Methode gibt ein Array von `COR_DEBUG_IL_TO_NATIVE_MAP`-Strukturen zurück. Um vermitteln, dass bestimmte Bereiche systemeigener Anweisungen besonderen Codebereichen (beispielsweise dem Prolog) entsprechen, können ein Eintrag im Array dessen `ilOffset` Feld festgelegt werden, auf den Wert der [CorDebugIlToNativeMappingTypes](../../../../docs/framework/unmanaged-api/debugging/cordebugiltonativemappingtypes-enumeration.md) -Enumeration.  
  
 Nachdem `GetILToNativeMapping` zurückgegeben wurde, müssen Sie sicherstellen, dass der `map`-Puffer groß genug war, um alle `COR_DEBUG_IL_TO_NATIVE_MAP`-Strukturen aufzunehmen. Dazu vergleichen Sie den Wert von `cMap` mit dem Wert des `pcMap`-Parameters. Wenn der `pcMap`-Wert nach Multiplikation mit der Größe einer `COR_DEBUG_IL_TO_NATIVE_MAP`-Struktur größer als `cMap` ist, weisen Sie einen größeren `map`-Puffer zu, aktualisieren Sie `cMap` mit der neuen Größe, und rufen Sie `GetILToNativeMapping` erneut auf.  
  
 Alternativ können Sie zuerst `GetILToNativeMapping` mit einem `map`-Puffer der Länge 0 (null) aufrufen, um die richtige Puffergröße zu ermitteln. Sie können die Puffergröße dann auf den Wert festlegen, der von `pcMap` zurückgegeben wurde, und `GetILToNativeMapping` erneut aufrufen.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorProf.idl, CorProf.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [ICorProfilerInfo-Schnittstelle](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)  
 [GetILToNativeMapping2-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-getiltonativemapping2-method.md)  
 [Profilerstellungsschnittstellen](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
 [Profilerstellung](../../../../docs/framework/unmanaged-api/profiling/index.md)
