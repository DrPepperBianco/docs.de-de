---
title: Konfigurieren und Erweitern der Laufzeit mit Verhalten
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: attaching extensions using behaviors [WCF]
ms.assetid: 149b99b6-6eb6-4f45-be22-c967279677d9
caps.latest.revision: "20"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 2ea157ea1ac73a287ba39c1468e7e9a5781d40a0
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="configuring-and-extending-the-runtime-with-behaviors"></a>Konfigurieren und Erweitern der Laufzeit mit Verhalten
Verhalten ermöglichen es, das Standardverhalten zu ändern und benutzerdefinierte Erweiterungen hinzuzufügen, die die Dienstkonfiguration überprüfen, oder das Laufzeitverhalten in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]-Client- und Dienstanwendungen zu ändern. In diesem Thema werden die Verhaltensschnittstellen beschrieben und erläutert, wie sie implementiert und wie sie zur Dienstbeschreibung (in einer Dienstanwendung) oder zu einem Endpunkt (in einer Clientanwendung) programmgesteuert oder in einer Konfigurationsdatei hinzugefügt werden können. Weitere Informationen zum Verwenden von vom System bereitgestellte Verhalten, finden Sie unter [Run-Time-Dienstverhalten angeben](../../../../docs/framework/wcf/specifying-service-run-time-behavior.md) und [Angabe zur Laufzeit Clientverhalten](../../../../docs/framework/wcf/specifying-client-run-time-behavior.md).  
  
## <a name="behaviors"></a>Verhalten  
 Verhaltenstypen werden zu den Dienst- oder Dienstendpunkt-Beschreibungsobjekten (auf der Dienst- bzw. Clientseite) hinzugefügt, bevor diese Objekte von [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] zum Erstellen einer Laufzeit verwendet werden, die einen [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Dienst oder einen [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Client ausführt. Wenn diese Verhaltenstypen während des Lauftzeitkonstruktionsprozesses aufgerufen werden, können sie auf Laufzeiteigenschaften und -methoden zugreifen, die die vom Vertrag, von den Bindungen und von den Adressen erstellte Laufzeit ändern.  
  
### <a name="behavior-methods"></a>Verhaltensmethoden  
 Alle Verhaltenstypen verfügen über eine `AddBindingParameters`-Methode, eine `ApplyDispatchBehavior`-Methode, eine `Validate`-Methode und eine `ApplyClientBehavior`-Methode mit einer Ausnahme: Da <xref:System.ServiceModel.Description.IServiceBehavior> nicht in einem Client ausgeführt werden kann, wird `ApplyClientBehavior` nicht implementiert.  
  
-   Verwenden Sie die `AddBindingParameters`-Methode, um benutzerdefinierte Objekte zu ändern oder einer Sammlung hinzuzufügen, auf die benutzerdefinierte Bindungen beim Erstellen der Laufzeit für ihre Verwendung zugreifen können. Ein Beispiel hierfür ist, wie Schutzanforderungen festgelegt werden, die beeinflussen, wie der Kanal erstellt wird, jedoch dem Kanalentwickler nicht bekannt sind.  
  
-   Verwenden Sie die `Validate`-Methode, um die Beschreibungsstruktur und das entsprechende Laufzeitobjekt zu untersuchen und sicherzustellen, dass es einen bestimmten Satz von Kriterien erfüllt.  
  
-   Verwenden Sie die `ApplyDispatchBehavior`-Methode und die `ApplyClientBehavior`-Methode, um die Beschreibungsstruktur zu untersuchen und die Laufzeit für einen bestimmten Bereich entweder im Dienst oder auf dem Client zu ändern. Sie können auch Erweiterungsobjekte einfügen.  
  
    > [!NOTE]
    >  Obwohl eine Beschreibungsstruktur in diesen Methoden bereitgestellt wird, dient sie nur zur Überprüfung. Wenn eine Beschreibungsstruktur geändert wird, ist das Verhalten nicht definiert.  
  
 Der Zugriff auf die Eigenschaften, die Sie ändern können, und die Anpassungsschnittstellen, die Sie implementieren können, erfolgt über die Dienst- und Clientlaufzeitklassen. Die Diensttypen sind die <xref:System.ServiceModel.Dispatcher.DispatchRuntime>-Klasse und die <xref:System.ServiceModel.Dispatcher.DispatchOperation>-Klasse. Die Clienttypen sind die <xref:System.ServiceModel.Dispatcher.ClientRuntime>-Klasse und die <xref:System.ServiceModel.Dispatcher.ClientOperation>-Klasse. Die <xref:System.ServiceModel.Dispatcher.ClientRuntime>-Klasse und die <xref:System.ServiceModel.Dispatcher.DispatchRuntime>-Klasse sind Erweiterungseinstiegspunkte, um clientweit und dienstweit auf Laufzeiteigenschaften bzw. Erweiterungssammlungen zuzugreifen. Entsprechend machen die <xref:System.ServiceModel.Dispatcher.ClientOperation>-Klasse und die <xref:System.ServiceModel.Dispatcher.DispatchOperation>-Klasse Clientvorgangs- und Dienstvorgangslaufzeit-Eigenschaften bzw. Erweiterungssammlungen verfügbar. Sie können jedoch auf das breiter angelegte Laufzeitobjekt vom Vorgangslaufzeitobjekt aus und umgekehrt zugreifen, sofern erforderlich.  
  
> [!NOTE]
>  Eine Erläuterung der Laufzeiteigenschaften und Erweiterungstypen enthalten, die Sie verwenden können, um das Ausführungsverhalten eines Clients zu ändern, finden Sie unter [Erweitern von Clients](../../../../docs/framework/wcf/extending/extending-clients.md). Eine Erläuterung der Laufzeiteigenschaften und Erweiterungstypen enthalten, die Sie verwenden können, um das Ausführungsverhalten eines Verteilers Dienst zu ändern, finden Sie unter [Erweitern von Verteilern](../../../../docs/framework/wcf/extending/extending-dispatchers.md).  
  
 Die meisten [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Benutzer interagieren nicht direkt mit der Laufzeit. Stattdessen verwenden sie Kernprogrammierungskonstrukte wie Endpunkte, Verträge, Bindungen, Adressen und Verhaltensattribute für Klassen oder Verhalten in Konfigurationsdateien. Diese Konstrukte bilden die *beschreibungsstruktur*, dies ist die vollständige Spezifikation für die Erstellung einer Laufzeit zur Unterstützung von eines Diensts oder Client von der beschreibungsstruktur beschriebenen.  
  
 Es gibt vier Arten von Verhalten in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   Dienstverhalten (<xref:System.ServiceModel.Description.IServiceBehavior>-Typen) ermöglicht die Anpassung der ganzen Dienstlaufzeit, einschließlich <xref:System.ServiceModel.ServiceHostBase>.  
  
-   Endpunktverhalten (<xref:System.ServiceModel.Description.IEndpointBehavior>-Typen) ermöglicht die Anpassung von Dienstendpunkten und ihren zugeordneten <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>-Objekten.  
  
-   Vertragsverhalten (<xref:System.ServiceModel.Description.IContractBehavior>-Typen) ermöglicht die Anpassung sowohl der <xref:System.ServiceModel.Dispatcher.ClientRuntime>-Klasse als auch der <xref:System.ServiceModel.Dispatcher.DispatchRuntime>-Klasse in Client- bzw. Dienstanwendungen.  
  
-   Vorgangsverhalten (<xref:System.ServiceModel.Description.IOperationBehavior>-Typen) ermöglicht ebenfalls die Anpassung der <xref:System.ServiceModel.Dispatcher.ClientOperation>-Klasse und der <xref:System.ServiceModel.Dispatcher.DispatchOperation>-Klasse in Client- bzw. Dienstanwendungen.  
  
 Sie können diese Verhaltenstypen zu verschiedenen Beschreibungsobjekten hinzufügen, indem Sie benutzerdefinierte Attribute implementieren, Anwendungskonfigurationsdateien verwenden oder sie direkt zur Verhaltenssammlung des entsprechenden Beschreibungsobjekts hinzufügen. Sie müssen jedoch zu einer Dienstbeschreibung oder einem Dienstendpunkt-Beschreibungsobjekt hinzugefügt werden, bevor <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> auf dem <xref:System.ServiceModel.ServiceHost> oder einer <xref:System.ServiceModel.ChannelFactory%601> aufgerufen wird.  
  
### <a name="behavior-scopes"></a>Verhaltensbereiche  
 Es stehen vier Verhaltenstypen zur Verfügung, die jeweils einem bestimmten Bereich des Laufzeitzugriffs entsprechen.  
  
#### <a name="service-behaviors"></a>Dienstverhalten  
 Dienstverhalten, das <xref:System.ServiceModel.Description.IServiceBehavior> implementiert, ist der Hauptmechanismus, mit dem die gesamte Dienstlaufzeit geändert wird. Für das Hinzufügen von Dienstverhalten zu einem Dienst stehen drei Mechanismen zur Verfügung.  
  
1.  Verwenden eines Attributs in der Dienstklasse.  Wenn ein <xref:System.ServiceModel.ServiceHost>-Objekt erstellt wird, wird von der <xref:System.ServiceModel.ServiceHost>-Implementierung Spiegelung eingesetzt, um den Attributsatz für den Diensttyp zu ermitteln. Falls eines der Attribute Implementierungen von <xref:System.ServiceModel.Description.IServiceBehavior> darstellt, wird es der Verhaltenssammlung für <xref:System.ServiceModel.Description.ServiceDescription> hinzugefügt. Dadurch können diese Verhaltenstypen an der Erstellung der Dienstlaufzeit partizipieren.  
  
2.  Programmgesteuertes Hinzufügen des Verhaltens zur Verhaltenssammlung in <xref:System.ServiceModel.Description.ServiceDescription>. Dies kann durch die folgenden Codezeilen erreicht werden:  
  
    ```  
    ServiceHost host = new ServiceHost(/* Parameters */);  
    host.Description.Behaviors.Add(/* Service Behavior */);  
    ```  
  
3.  Implementieren eines benutzerdefinierten <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>, das die Konfiguration erweitert. Dies ermöglicht die Verwendung des Dienstverhaltens von Anwendungskonfigurationsdateien aus.  
  
 Beispiele für das Dienstverhalten in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] umfassen das <xref:System.ServiceModel.ServiceBehaviorAttribute>-Attribut, das <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>-Verhalten und das <xref:System.ServiceModel.Description.ServiceMetadataBehavior>-Verhalten.  
  
#### <a name="contract-behaviors"></a>Vertragsverhalten  
 Vertragsverhalten, das die <xref:System.ServiceModel.Description.IContractBehavior>-Schnittstelle implementiert, dient zur Erweiterung der Client- sowie Dienstlaufzeit in einem Vertrag.  
  
 Für das Hinzufügen von Vertragsverhalten zu einem Vertrag stehen zwei Mechanismen zur Verfügung.  Der erste Mechanismus besteht im Erstellen eines benutzerdefinierten Attributs zur Verwendung in der Vertragsschnittstelle. Wenn eine Vertragsschnittstelle entweder an einen <xref:System.ServiceModel.ServiceHost> oder eine <xref:System.ServiceModel.ChannelFactory%601> weitergegeben wird, untersucht [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] die Attribute an der Schnittstelle. Falls eines der Attribute Implementierungen von <xref:System.ServiceModel.Description.IContractBehavior> darstellt, wird es der Verhaltenssammlung in der für diese Schnittstelle erstellten <xref:System.ServiceModel.Description.ContractDescription?displayProperty=nameWithType> hinzugefügt.  
  
 Sie können das <xref:System.ServiceModel.Description.IContractBehaviorAttribute?displayProperty=nameWithType> auch im benutzerdefinierten Vertragsverhaltensattribut implementieren. In diesem Fall sieht das Verhalten wie folgt aus bei der Anwendung auf:  
  
 • Eine Vertragsschnittstelle. In diesem Fall wird das Verhalten an jedem beliebigen Endpunkt auf alle Verträge dieses Typs angewendet, und [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ignoriert den Wert der <xref:System.ServiceModel.Description.IContractBehaviorAttribute.TargetContract%2A?displayProperty=nameWithType>-Eigenschaft.  
  
 • Eine Dienstklasse. In diesem Fall wird das Verhalten nur auf Endpunkte angewendet, deren Vertrag der Wert der  <xref:System.ServiceModel.Description.IContractBehaviorAttribute.TargetContract%2A>-Eigenschaft ist.  
  
 • Eine Rückrufklasse. In diesem Fall wird das Verhalten auf den Endpunkt des Duplexclients angewendet, und [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ignoriert den Wert der <xref:System.ServiceModel.Description.IContractBehaviorAttribute.TargetContract%2A>-Eigenschaft.  
  
 Der zweite Mechanismus besteht im Hinzufügen des Verhaltens zur Verhaltenssammlung einer <xref:System.ServiceModel.Description.ContractDescription>.  
  
 Beispiele für das Vertragsverhalten in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] umfassen das <xref:System.ServiceModel.DeliveryRequirementsAttribute?displayProperty=nameWithType>-Attribut. Weitere Informationen und ein Beispiel hierzu finden Sie im Verweisthema.  
  
#### <a name="endpoint-behaviors"></a>Endpunktverhalten  
 Endpunktverhalten, das <xref:System.ServiceModel.Description.IEndpointBehavior> implementiert, ist der Hauptmechanismus, mit dem die gesamte Dienst- oder Clientlaufzeit für einen bestimmten Endpunkt geändert wird.  
  
 Für das Hinzufügen von Endpunktverhalten zu einem Dienst stehen zwei Mechanismen zur Verfügung.  
  
1.  Hinzufügen des Verhaltens zur <xref:System.ServiceModel.Description.ServiceEndpoint.Behaviors%2A>-Eigenschaft.  
  
2.  Implementieren eines benutzerdefinierten <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>, das die Konfiguration erweitert.  
  
 Weitere Informationen und ein Beispiel hierzu finden Sie im Verweisthema.  
  
#### <a name="operation-behaviors"></a>Vorgangsverhalten  
 Vorgangsverhalten, das die <xref:System.ServiceModel.Description.IOperationBehavior>-Schnittstelle implementiert, dient zur Erweiterung der Client- sowie Dienstlaufzeit für jeden Vorgang.  
  
 Für das Hinzufügen von Vorgangsverhalten zu einem Vorgang stehen zwei Mechanismen zur Verfügung. Der erste Mechanismus besteht im Erstellen eines benutzerdefinierten Attributs zur Verwendung in der Methode, die den Vorgang formt. Wenn ein Vorgang entweder einem <xref:System.ServiceModel.ServiceHost> oder einer <xref:System.ServiceModel.ChannelFactory> hinzugefügt wird, fügt [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] jedes <xref:System.ServiceModel.Description.IOperationBehavior>-Attribut zur Verhaltenssammlung in der für diesen Vorgang erstellten <xref:System.ServiceModel.Description.OperationDescription> hinzu.  
  
 Der zweite Mechanismus besteht im direkten Hinzufügen des Verhaltens zur Verhaltenssammlung einer konstruierten <xref:System.ServiceModel.Description.OperationDescription>.  
  
 Beispiele für Vorgangsverhalten in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] umfassen <xref:System.ServiceModel.OperationBehaviorAttribute> und <xref:System.ServiceModel.TransactionFlowAttribute>.  
  
 Weitere Informationen und ein Beispiel hierzu finden Sie im Verweisthema.  
  
### <a name="using-configuration-to-create-behaviors"></a>Verwenden der Konfiguration zur Erstellung von Verhalten  
 Dienst-, Endpunkt- und Vertragsverhalten können so konzipiert werden, dass sie in Code oder mithilfe von Attributen angegeben werden. Nur Dienst- und Endpunktverhalten können mit Anwendungs- oder Webkonfigurationsdateien konfiguriert werden. Durch das Verfügbarmachen von Verhalten mit Attributen können Entwickler ein Verhalten zum Kompilierungszeitpunkt angeben, das zur Laufzeit weder hinzugefügt, entfernt oder geändert werden kann. Dies ist häufig für Verhalten nützlich, das für den korrekten Betrieb eines Diensts immer erforderlich ist (z. B. die transaktionsbezogenen Parameter für das <xref:System.ServiceModel.ServiceBehaviorAttribute?displayProperty=nameWithType>-Attribut). Durch Verfügbarmachen von Verhalten unter Verwendung der Konfiguration können Entwickler die Spezifikation und Konfiguration des Verhaltens den Personen überlassen, die den Dienst bereitstellen. Dieses Verfahren ist nützlich für Verhalten, das aus optionalen Komponenten oder einer anderen bereitstellungsspezifischen Konfiguration besteht, wie z. B. ob Metadaten für den Dienst verfügbar gemacht werden oder die spezifische Autorisierungskonfiguration für einen Dienst.  
  
> [!NOTE]
>  Sie können konfigurationsunterstützendes Verhalten auch zur Durchsetzung von Unternehmensrichtlinien verwenden, indem sie in die Konfigurationsdatei machine.config eingefügt werden und diese Elemente gesperrt werden. Eine Beschreibung und ein Beispiel finden Sie unter [Vorgehensweise: Sperren Sie die Endpunkte im Unternehmen](../../../../docs/framework/wcf/extending/how-to-lock-down-endpoints-in-the-enterprise.md).  
  
 Um ein Verhalten unter Verwendung der Konfiguration verfügbar zu machen, muss ein Entwickler eine abgeleitete Klasse von <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> erstellen und die Erweiterung anschließend in der Konfiguration registrieren.  
  
 Das folgende Codebeispiel veranschaulicht, wie ein <xref:System.ServiceModel.Description.IEndpointBehavior> <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> implementiert:  
  
```  
// BehaviorExtensionElement members  
    public override Type BehaviorType  
    {  
      get { return typeof(EndpointBehaviorMessageInspector); }  
    }  
  
    protected override object CreateBehavior()  
    {  
      return new EndpointBehaviorMessageInspector();  
    }  
```  
  
 Damit das Konfigurationssystem ein benutzerdefiniertes <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> laden kann, muss es als Erweiterung registriert werden. Das folgende Codebeispiel zeigt die Konfigurationsdatei für das vorhergehende Endpunktverhalten:  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service   
        name="Microsoft.WCF.Documentation.SampleService"  
        behaviorConfiguration="metadataSupport"  
      >  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost:8080/ServiceMetadata" />  
          </baseAddresses>  
        </host>  
        <endpoint  
          address="/SampleService"  
          binding="wsHttpBinding"  
          behaviorConfiguration="withMessageInspector"   
          contract="Microsoft.WCF.Documentation.ISampleService"  
        />  
        <endpoint  
           address="mex"  
           binding="mexHttpBinding"  
           contract="IMetadataExchange"  
        />  
      </service>  
    </services>  
    <behaviors>  
      <serviceBehaviors>  
      <behavior name="metadataSupport">  
        <serviceMetadata httpGetEnabled="true" httpGetUrl=""/>  
      </behavior>  
      </serviceBehaviors>  
      <endpointBehaviors>  
        <behavior name="withMessageInspector">  
          <endpointMessageInspector />  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
    <extensions>  
      <behaviorExtensions>  
        <add   
          name="endpointMessageInspector"  
          type="Microsoft.WCF.Documentation.EndpointBehaviorMessageInspector, HostApplication, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null"  
        />  
      </behaviorExtensions>  
    </extensions>  
  </system.serviceModel>  
</configuration>  
```  
  
 Wobei `Microsoft.WCF.Documentation.EndpointBehaviorMessageInspector` ist der verhaltenserweiterungstyp und `HostApplication` ist der Name der Assembly, zu der diese Klasse kompiliert wurde.  
  
### <a name="evaluation-order"></a>Auswertungsreihenfolge  
 Die <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType> und der <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> sind für das Erstellen der Laufzeit aus dem Programmierungsmodell und der Beschreibung verantwortlich. Verhaltenstypen, wie zuvor beschrieben, tragen zu diesem Erstellungsprozess auf der Dienst-, Endpunkt-, Vertrags- und Vorgangsebene bei.  
  
 Der <xref:System.ServiceModel.ServiceHost> wendet Verhalten in folgender Reihenfolge an:  
  
1.  Dienst  
  
2.  Vertrag  
  
3.  Endpunkt  
  
4.  Vorgang  
  
 Innerhalb einer Verhaltenssammlung wird keine Reihenfolge garantiert.  
  
 Der <xref:System.ServiceModel.ChannelFactory%601> wendet Verhalten in folgender Reihenfolge an:  
  
1.  Vertrag  
  
2.  Endpunkt  
  
3.  Vorgang  
  
 Innerhalb einer Verhaltenssammlung wird auch in diesem Fall keine Reihenfolge garantiert.  
  
### <a name="adding-behaviors-programmatically"></a>Programmgesteuertes Hinzufügen von Verhalten  
 Eigenschaften von <xref:System.ServiceModel.Description.ServiceDescription?displayProperty=nameWithType> in der Dienstanwendung dürfen nicht im Anschluss an die <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A?displayProperty=nameWithType>-Methode auf <xref:System.ServiceModel.ServiceHostBase?displayProperty=nameWithType> geändert werden. Einige Member, wie die <xref:System.ServiceModel.ServiceHostBase.Credentials%2A?displayProperty=nameWithType>-Eigenschaft und die `AddServiceEndpoint`-Methoden auf <xref:System.ServiceModel.ServiceHostBase> und <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType>, lösen eine Ausnahme aus, wenn eine Änderung über diesen Punkt hinaus stattfindet. Andere Member können geändert werden, wobei das Ergebnis jedoch nicht definiert ist.  
  
 Ähnlich verhält es sich mit den <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=nameWithType>-Werten, die auf dem Client nach dem Aufruf von <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A> auf <xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType> nicht geändert werden dürfen. Die <xref:System.ServiceModel.ChannelFactory.Credentials%2A?displayProperty=nameWithType>-Eigenschaft löst eine Ausnahme aus, wenn sie über diesen Punkt hinaus geändert wird. Die anderen Clientbeschreibungswerte können jedoch ohne Fehler geändert werden. Das Ergebnis ist allerdings nicht definiert.  
  
 Sowohl für den Dienst als auch den Client wird empfohlen, die Beschreibung vor dem Aufruf von <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A?displayProperty=nameWithType> zu ändern.  
  
### <a name="inheritance-rules-for-behavior-attributes"></a>Vererbungsregeln für Verhaltensattribute  
 Alle vier Verhaltenstypen können mit Attributen aufgefüllt werden – Dienstverhalten und Vertragsverhalten. Da Attribute für verwaltete Objekte und Member definiert werden und verwaltete Objekte und Member die Vererbung unterstützen, ist es notwendig zu definieren, wie Verhaltensattribute im Vererbungskontext funktionieren.  
  
 Auf höherer Ebene gilt die Regel, dass für einen bestimmten Bereich (z. B. Dienst, Vertrag oder Vorgang) alle Verhaltensattribute in der Vererbungshierarchie für diesen Bereich angewendet werden. Wenn zwei Verhaltensattribute desselben Typs vorhanden sind, wird nur der Typ mit den meisten Ableitungen verwendet.  
  
#### <a name="service-behaviors"></a>Dienstverhalten  
 Für eine bestimmte Dienstklasse werden alle Dienstverhaltensattribute für diese Klasse und für übergeordnete Elemente dieser Klasse angewendet. Wenn derselbe Attributtyp an mehreren Stellen der Vererbungshierarchie angewendet wird, wird nur der Typ mit den meisten Ableitungen verwendet.  
  
```  
[ServiceBehavior(ConcurrencyMode = ConcurrencyMode.Multiple)]  
[AspNetCompatibilityRequirementsAttribute(  
    AspNetCompatibilityRequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]  
public class A { /* … */ }  
  
[ServiceBehavior(InstanceContextMode = InstanceContextMode.Single)]  
public class B : A { /* … */}  
```  
  
 Im vorhergehenden Fall weist der Dienst B am Ende den <xref:System.ServiceModel.InstanceContextMode>-Modus <xref:System.ServiceModel.InstanceContextMode.Single>, den <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode>-Modus <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed> und den <xref:System.ServiceModel.ConcurrencyMode>-Modus <xref:System.ServiceModel.ConcurrencyMode.Single> auf. Der <xref:System.ServiceModel.ConcurrencyMode>-Modus lautet <xref:System.ServiceModel.ConcurrencyMode.Single>, da das <xref:System.ServiceModel.ServiceBehaviorAttribute>-Attribut für den Dienst B "mehr Ableitungen" aufweist als Dienst A.  
  
#### <a name="contract-behaviors"></a>Vertragsverhalten  
 Für einen bestimmten Vertrag werden alle Vertragsverhaltensattribute für diese Schnittstelle und für übergeordnete Elemente dieser Schnittstelle angewendet. Wenn derselbe Attributtyp an mehreren Stellen der Vererbungshierarchie angewendet wird, wird nur der Typ mit den meisten Ableitungen verwendet.  
  
#### <a name="operation-behaviors"></a>Vorgangsverhalten  
 Wenn ein bestimmter Vorgang einen vorhandenen abstrakten oder virtuellen Vorgang nicht überschreibt, werden keine Vererbungsregeln angewendet.  
  
 Wenn ein Vorgang einen vorhandenen Vorgang überschreibt, werden alle Vorgangsverhaltensattribute für diesen Vorgang und für die übergeordneten Elemente dieses Vorgangs angewendet.  Wenn derselbe Attributtyp an mehreren Stellen der Vererbungshierarchie angewendet wird, wird nur der Typ mit den meisten Ableitungen verwendet.
