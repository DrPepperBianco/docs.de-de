---
title: Suchen der in einem lokalen System definierten Zeitzonen
ms.custom: 
ms.date: 04/10/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time zones [.NET Framework], local
- time zones [.NET Framework], finding local system time zones
- time zone identifiers [.NET Framework]
- local time zone access
- time zones [.NET Framework], retrieving
- UTC times, finding local system time zones
- time zones [.NET Framework], UTC
ms.assetid: 3f63b1bc-9a4b-4bde-84ea-ab028a80d3e1
caps.latest.revision: "14"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: e61f05741c1edd86d9baad4f6ebc9f4e91318250
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/23/2017
---
# <a name="finding-the-time-zones-defined-on-a-local-system"></a>Suchen der in einem lokalen System definierten Zeitzonen

Die <xref:System.TimeZoneInfo>-Klasse macht keinen öffentlichen Konstruktor verfügbar. Demzufolge kann das `new`-Schlüsselwort nicht zum Erstellen eines neuen <xref:System.TimeZoneInfo>-Objekts verwendet werden. Stattdessen werden <xref:System.TimeZoneInfo>-Objekte entweder durch Abrufen von Informationen über vordefinierte Zeitzonen aus der Registrierung oder durch Erstellen einer benutzerdefinierten Zeitzone instanziiert. Dieses Thema behandelt die Instanziierung einer Zeitzone von den in der Registrierung gespeicherten Daten. Darüber hinaus ermöglichen die `static`-Eigenschaften (`shared` in Visual Basic) der <xref:System.TimeZoneInfo>-Klasse Zugriff auf die koordinierte Weltzeit (Universal Coordinated Time, UTC) und die lokale Zeitzone.

> [!NOTE]
> Für Zeitzonen, die nicht in der Registrierung definiert sind, können Sie benutzerdefinierte Zeitzonen durch Aufrufen der Überladungen der <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>-Methode erstellen. Erstellen einer benutzerdefinierten Zeitzone wird erläutert, der [Vorgehensweise: Erstellen von Zeitzonen ohne Anpassungsregeln](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md) und [Vorgehensweise: Erstellen von Zeitzonen mit Anpassungsregeln](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md) Themen. Darüber hinaus können Sie ein <xref:System.TimeZoneInfo>-Objekt durch Wiederherstellen aus einer serialisierten Zeichenfolge mit der <xref:System.TimeZoneInfo.FromSerializedString%2A>-Methode instanziieren. Serialisiert und deserialisiert eine <xref:System.TimeZoneInfo> Objekt wird erläutert, der [wie: Speichern von Zeitzonen in einer eingebetteten Ressource](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md) und [Vorgehensweise: Wiederherstellen von Zeitzonen aus einer eingebetteten Ressource](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md) Themen.

## <a name="accessing-individual-time-zones"></a>Zugreifen auf einzelne Zeitzonen

Die <xref:System.TimeZoneInfo>-Klasse bietet zwei vordefinierte Zeitzonenobjekte, die die koordinierte Weltzeit und die lokale Zeitzone darstellen. Diese werden jeweils über die <xref:System.TimeZoneInfo.Utc%2A>- und die <xref:System.TimeZoneInfo.Local%2A>-Eigenschaft zur Verfügung gestellt. Anleitungen zum Zugreifen auf die UTC oder die lokalen Zeitzonen finden Sie unter [Vorgehensweise: Zugreifen auf die vordefinierte UTC und Ortszeit Zonenobjekte](../../../docs/standard/datetime/access-utc-and-local.md).

Sie können auch ein <xref:System.TimeZoneInfo>-Objekt instanziieren, das die in der Registrierung definierten Zeitzonen darstellt. Anleitungen zum Instanziieren einer bestimmten Zeitzonenobjekts finden Sie unter [wie: Instanziieren eines TimeZoneInfo-Objekts](../../../docs/standard/datetime/instantiate-time-zone-info.md).

## <a name="time-zone-identifiers"></a>Zeitzonenbezeichner

Der Zeitzonenbezeichner ist ein Schlüsselfeld, das die Zeitzone eindeutig identifiziert. Während die meisten Schlüssel relativ kurz sind, ist der Zeitzonenbezeichner vergleichsweise lang. In den meisten Fällen entspricht der dazugehörige Wert der <xref:System.TimeZoneInfo.StandardName%2A?displayProperty=nameWithType>-Eigenschaft, die zum Bereitstellen des Namens der Standardzeit für die Zeitzone verwendet wird. Es gibt jedoch auch Ausnahmen. Die beste Möglichkeit, um sicherzustellen, dass Sie einen gültigen Bezeichner angeben, besteht darin, die auf Ihrem System verfügbaren Zeitzonen aufzulisten und die dazugehörigen IDs zur Kenntnis zu nehmen.

## <a name="see-also"></a>Siehe auch

[Datumsangaben, Uhrzeiten und Zeitzonen](../../../docs/standard/datetime/index.md)
[Vorgehensweise: Zugreifen auf die vordefinierte UTC und Ortszeit Zonenobjekte](../../../docs/standard/datetime/access-utc-and-local.md)
[wie: Instanziieren eines TimeZoneInfo-Objekts](../../../docs/standard/datetime/instantiate-time-zone-info.md) 
 [Konvertieren von Uhrzeiten zwischen Zeitzonen](../../../docs/standard/datetime/converting-between-time-zones.md)
