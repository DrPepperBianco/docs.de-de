---
title: '&lt;endpoint&gt;-Element'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2fc8fedc-78d0-4e87-8142-fbfd26c15a4e
caps.latest.revision: "23"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 7175cf55df6bb735367effa8f806a472b9ce5ea6
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="ltendpointgt-element"></a>&lt;endpoint&gt;-Element
Gibt die Bindung, den Vertrag und Adresseigenschaften für einen Dienstendpunkt an, der zur Verfügbarmachung von Diensten verwendet wird.  
  
 \<System. ServiceModel >  
\<Dienst >  
\<Endpunkt >  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<endpoint address="String"  
   behaviorConfiguration="String"  
   binding="String"  
   bindingConfiguration="String"  
   bindingName="String"  
   bindingNamespace="String"  
   contract="String"  
   endpointConfiguration="String"   isSystemEndpoint="Boolean"   kind="String"   listenUriMode="Explicit/Unique"  
   listenUri="Uri"  
</endpoint>  
```  
  
## <a name="attributes-and-elements"></a>Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|Adresse|Eine Zeichenfolge mit der Adresse des Endpunkts. Die Adresse kann als absolute oder relative Adresse angegeben werden. Bei Bereitstellung einer relativen Adresse wird vom Host erwartet, dass er eine Basisadresse bereitstellt, die für das in der Bindung verwendete Transportschema geeignet ist. Wenn keine Adresse konfiguriert wird, wird angenommen, dass die Basisadresse der Adresse für diesen Endpunkt entspricht.<br /><br /> Der Standardwert ist eine leere Zeichenfolge.|  
|behaviorConfiguration|Eine Zeichenfolge mit dem Namen des Verhaltens, das am Endpunkt verwendet werden soll.|  
|Bindung|Erforderliches Zeichenfolgenattribut, das den Typ der zu verwendenden Bindung angibt. Dieser muss einen registrierten Konfigurationsabschnitt aufweisen, da sonst nicht auf ihn verwiesen werden kann. Der Typ wird anhand des Abschnittsnamens registriert, nicht anhand des Typnamens der Bindung.|  
|bindingConfiguration|Eine Zeichenfolge, die den Namen der Bindung enthält, die beim Instanziieren des Endpunkts verwendet werden soll. Der Name der Bindung muss sich bei der Endpunktdefinition im Gültigkeitsbereich befinden. Der Standardwert ist eine leere Zeichenfolge.<br /><br /> Dieses Attribut wird zusammen mit `binding` zum Verweisen auf eine spezifische Bindungskonfiguration in der Konfigurationsdatei verwendet. Legen Sie dieses Attribut fest, wenn Sie eine benutzerdefinierte Bindung verwenden möchten. Andernfalls wird unter Umständen eine Ausnahme ausgelöst.|  
|bindingName|Eine Zeichenfolge, die den eindeutigen qualifizierten Namen der Bindung für den Definitionsexport über WSDL definiert. Der Standardwert ist eine leere Zeichenfolge.|  
|bindingNamespace|Eine Zeichenfolge, die den qualifizierten Namen des Namespaces der Bindung für den Definitionsexport über WSDL definiert. Der Standardwert ist eine leere Zeichenfolge.|  
|Vertrag (Contract)|Eine Zeichenfolge, die angibt, welche Verträge von diesem Endpunkt verfügbar gemacht werden. Die Assembly muss den Vertragstyp implementieren. Wenn eine Dienstimplementierung einen einzelnen Vertragstyp implementiert, kann diese Eigenschaft ausgelassen werden. Der Standardwert ist eine leere Zeichenfolge.|  
|endpointConfiguration|Eine Zeichenfolge, die den Namen des Standardendpunkts angibt, der mit dem `kind`-Attribut festgelegt wird, das auf die zusätzlichen Konfigurationsinformationen dieses Standardendpunkts verweist. Der gleiche Name muss im Abschnitt `<standardEndpoints>` definiert werden.|  
|isSystemEndpoint|Ein boolescher Wert, der angibt, ob ein Endpunkt ein Infrastrukturendpunkt ist.|  
|kind|Eine Zeichenfolge, die den Typ des angewendeten Standardendpunkts angibt. Der Typ muss im Abschnitt `<extensions>` oder in machine.config registriert werden. Wenn kein Wert angegeben wird, wird ein allgemeiner Dienstendpunkt erstellt.|  
|listenUriMode|Gibt an, wie der Transport die `ListenUri` verarbeitet, die für die Überwachung durch den Dienst bereitgestellt wurde. Folgende Werte sind gültig:<br /><br /> -Explizite<br />-Eindeutig<br /><br /> Der Standardwert ist Explicit.|  
|listenUri|Eine Zeichenfolge mit dem URI, an dem der Dienstendpunkt lauscht. Der Standardwert ist eine leere Zeichenfolge.|  
|Name|Optionales Attribut. Eine Zeichenfolge, die den Namen des Dienstendpunkts angibt. Der Standardwert ist die Verkettung des Bindungsnamen und des Vertragsbeschreibungsnamens. Dienste haben möglicherweise mehrere Endpunkte, sodass das `name`-Attribut des Endpunkts sich vom Namen des Diensts unterscheidet.|  
  
### <a name="child-elements"></a>Untergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[\<Header >](../../../../../docs/framework/configure-apps/file-schema/wcf/headers.md)|Eine Auflistung von Adressheadern.|  
|[\<Identität >](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)|Eine Identität, welche die Authentifizierung eines Endpunkts durch andere Endpunkte ermöglicht, mit denen Nachrichten ausgetauscht werden.|  
  
### <a name="parent-elements"></a>Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[\<Dienst >](../../../../../docs/framework/configure-apps/file-schema/wcf/service.md)|Ein Konfigurationsabschnitt, der eine Liste mit Endpunkten definiert, zu denen ein Client eine Verbindung herstellen kann.|  
  
## <a name="example"></a>Beispiel  
 Dies ist ein Beispiel für eine Dienstendpunkt-Konfiguration.  
  
```xml  
<endpoint   
    address="/HelloWorld/"  
    bindingConfiguration="usingDefaults"  
    bindingName="MyBinding"  
    binding="customBinding"  
    contract="HelloWorld">  
    <Headers>  
       <Region xmlns="http://tempuri.org/">EastCoast</Region>  
       <Member xmlns="http://tempuri.org/">Gold</Member>  
    </Headers>  
</endpoint>  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.ServiceModel.Configuration.ServiceEndpointElement>  
 <xref:System.ServiceModel.EndpointAddress>  
 <xref:System.ServiceModel.Description.ServiceEndpoint>  
 [Endpunkte: Adressen, Bindungen und Verträge](../../../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)  
 [Vorgehensweise: Erstellen eines Dienstendpunkts in einer Konfiguration](../../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)
