---
title: MSMQ-Integrationstransport
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2bf9893a-fbd1-41fc-b6de-a41a44279936
caps.latest.revision: "5"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 18dd1262c572a7e8844d9fe2beb5de7f52c28e1e
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="msmq-integration-transport"></a>MSMQ-Integrationstransport
In diesem Thema sind alle vom MSMQ-Integrationstransport erzeugten Ausnahmen aufgeführt.  
  
## <a name="exception-list"></a>Ausnahmeliste  
  
|Ressourcencode|Ressourcenzeichenfolge|  
|-------------------|---------------------|  
|MessageSizeMustBeInIntegerRange|Diese Factory puffert Nachrichten, deshalb müssen die Nachrichtengrößen im Bereich eines ganzzahligen Werts sein.|  
|MsmqByteArrayBodyExpected|Ein Konflikt ist zwischen dem angegebenen Serialisierungsformat und dem Text der MSMQ-Nachricht aufgetreten. Die Nachricht kann nicht gesendet oder empfangen werden. Das Serialisierungsformat ByteArray erfordert, dass der Text der MSMQ-Nachricht vom Typ Byte[] ist.|  
|MsmqCannotDeserializeActiveXMessage|Ein ActiveX-Serialisierungsfehler ist aufgetreten. Die Nachricht kann nicht gesendet oder empfangen werden. Der angegebene Variantentyp für den Text passt nicht zum tatsächlichen MSMQ-Nachrichtentext.|  
|MsmqCannotUseBodyTypeWithActiveXSerialization|Die Eigenschaften der Nachricht stimmen nicht überein. Die Nachricht kann nicht gesendet oder empfangen werden. Die BodyType-Nachrichteneigenschaft kann nicht angegeben werden, wenn das ActiveX-Serialisierungsformat verwendet wird.|  
|MsmqInvalidServiceOperationForMsmqIntegrationBinding|Die MsmqIntegrationBinding-Validierung ist fehlgeschlagen. Der Dienstendpunkt kann nicht gestartet werden. Die angegebene Bindung unterstützt die Methodensignatur für den angegebenen Dienstvorgang im angegebenen Vertrag nicht. Korrigieren Sie den Dienstvorgang, um MsmqIntegrationBinding zu verwenden.|  
|MsmqInvalidTypeDeserialization|Die ActiveX-Serialisierung ist fehlgeschlagen, da das Serialisierungsformat nicht erkannt werden kann. Die Nachricht kann nicht gesendet oder empfangen werden.|  
|MsmqInvalidTypeSerialization|Der Variantentyp wird nicht erkannt. Die ActiveX-Serialisierung ist fehlgeschlagen. Die Nachricht kann nicht gesendet oder empfangen werden. Der angegebene Variantentyp wird nicht unterstützt.|  
|MsmqStreamBodyExpected|Konflikt zwischen Serialisierungsformat und Textinhalt. Nachricht kann nicht gesendet oder empfangen werden. Nur ein Text vom Typ "Stream" kann über den Stream-Serialisierungsmodus gesendet oder empfangen werden.|
