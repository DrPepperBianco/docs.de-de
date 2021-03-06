---
title: 'Exemplarische Vorgehensweise: Einfaches Objektmodell und Abfrage (C#)'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 419961cc-92d6-45f5-ae8a-d485bdde3a37
caps.latest.revision: "3"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: dotnet
ms.openlocfilehash: 1c118948f0eac8a9df81432b75297511172b10f0
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="walkthrough-simple-object-model-and-query-c"></a>Exemplarische Vorgehensweise: Einfaches Objektmodell und Abfrage (C#)
Diese exemplarische Vorgehensweise stellt ein grundlegendes End-to-End-Szenario für [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] mit minimaler Komplexität bereit. Sie erstellen eine Entitätsklasse, die die Customers-Tabelle in der Beispieldatenbank Northwind modelliert. Sie erstellen dann eine einfache Abfrage, um Kunden aus London aufzulisten.  
  
 Diese exemplarische Vorgehensweise ist codeorientiert, um [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]-Konzepte zu verdeutlichen. In der Regel verwenden Sie [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] zum Erstellen des Objektmodells.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Diese exemplarische Vorgehensweise wurde mithilfe von Visual C#-Entwicklungseinstellungen geschrieben.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
  
-   Diese exemplarische Vorgehensweise verwendet einen dedizierten Ordner ("c:\linqtest5") als Speicherort für Dateien. Erstellen Sie diesen Ordner, bevor Sie die exemplarische Vorgehensweise starten.  
  
-   Für dieses Beispiel wird die Beispieldatenbank Northwind benötigt. Befindet sich diese Datenbank nicht auf Ihrem Entwicklungscomputer, können Sie diese von der Microsoft Downloadsite herunterladen. Anweisungen hierzu finden Sie unter [Herunterladen von Beispieldatenbanken](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md). Nachdem Sie die Datenbank heruntergeladen haben, kopieren Sie die Datei in den Ordner c:\linqtest5.  
  
## <a name="overview"></a>Übersicht  
 Diese exemplarische Vorgehensweise umfasst sechs Hauptaufgaben:  
  
-   Erstellen einer [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]-Lösung in [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)].  
  
-   Zuordnen einer Datenbanktabelle zu einer Klasse.  
  
-   Festlegen von Eigenschaften für die Klasse, um Datenbankspalten darzustellen.  
  
-   Herstellen einer Verbindung zur Beispieldatenbank Northwind.  
  
-   Erstellen einer einfachen Abfrage der Datenbank.  
  
-   Ausführen der Abfrage und Prüfen der Ergebnisse  
  
## <a name="creating-a-linq-to-sql-solution"></a>Erstellen einer LINQ to SQL-Lösung  
 In dieser ersten Aufgabe erstellen Sie eine [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)]-Lösung, die die erforderlichen Verweise zur Erstellung und Ausführung eines [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]-Projekts enthält.  
  
#### <a name="to-create-a-linq-to-sql-solution"></a>So erstellen Sie eine LINQ to SQL-Lösung  
  
1.  Auf der [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] **Datei** Sie im Menü **neu**, und klicken Sie dann auf **Projekt**.  
  
2.  In der **-Projekttypen** im Bereich der **neues Projekt** (Dialogfeld), klicken Sie auf **Visual C#-**.  
  
3.  Klicken Sie im Bereich **Vorlagen** auf **Konsolenanwendung**.  
  
4.  In der **Namen** geben **LinqConsoleApp**.  
  
5.  In der **Speicherort** Vergewissern Sie sich, wo die Projektdateien gespeichert werden sollen.  
  
6.  Klicken Sie auf **OK**.  
  
## <a name="adding-linq-references-and-directives"></a>Hinzufügen von LINQ-Verweisen und Anweisungen  
 Diese exemplarische Vorgehensweise verwendet Assemblys, die im Projekt u. U. nicht standardmäßig installiert sind. Wenn System.Data.Linq nicht als Verweis im Projekt aufgeführt ist (Erweitern Sie die **Verweise** Knoten **Projektmappen-Explorer**), fügen Sie diesen wie nachfolgend beschrieben hinzu.  
  
#### <a name="to-add-systemdatalinq"></a>So fügen Sie System.Data.Linq hinzu  
  
1.  In **Projektmappen-Explorer**, mit der rechten Maustaste **Verweise**, und klicken Sie dann auf **Verweis hinzufügen**.  
  
2.  In der **Verweis hinzufügen** (Dialogfeld), klicken Sie auf **.NET**, klicken Sie auf die System.Data.Linq-Assembly, und klicken Sie dann auf **OK**.  
  
     Dem Projekt wird die Assembly hinzugefügt.  
  
3.  Fügen Sie die folgenden Direktiven am oberen Rand **"Program.cs"**:  
  
     [!code-csharp[DLinqWalk1CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#1)]  
  
## <a name="mapping-a-class-to-a-database-table"></a>Zuordnen einer Klasse zu einer Datenbanktabelle.  
 In diesem Schritt erstellen Sie eine Klasse und ordnen diese einer Datenbanktabelle zu. Eine solche Klasse spricht man ein *Entitätsklasse*. Beachten Sie, dass die Zuordnung durch Hinzufügen des <xref:System.Data.Linq.Mapping.TableAttribute>-Attributs erreicht wird. Die <xref:System.Data.Linq.Mapping.TableAttribute.Name%2A>-Eigenschaft gibt den Namen der Tabelle in der Datenbank an.  
  
#### <a name="to-create-an-entity-class-and-map-it-to-a-database-table"></a>So erstellen Sie eine Entitätsklasse und weisen diese einer Datenbanktabelle zu  
  
-   Geben Sie den folgenden Code direkt oberhalb der `Program`-Klassendeklaration in Program.cs ein, oder fügen Sie ihn ein:  
  
     [!code-csharp[DLinqWalk1CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#2)]  
  
## <a name="designating-properties-on-the-class-to-represent-database-columns"></a>Festlegen von Eigenschaften für die Klasse, um Datenbankspalten darzustellen  
 In diesem Schritt erledigen Sie mehrere Aufgaben.  
  
-   Sie verwenden das <xref:System.Data.Linq.Mapping.ColumnAttribute>-Attribut, um die `CustomerID`-Eigenschaft und die `City`-Eigenschaft der Entitätsklasse für die Darstellung von Spalten in der Datenbanktabelle festzulegen.  
  
-   Sie legen die `CustomerID`-Eigenschaft zur Darstellung einer Primärschlüsselspalte in der Datenbank fest.  
  
-   Sie legen `_CustomerID`- und `_City`-Felder für den privaten Speicher fest. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] kann Werte dann direkt speichern und abrufen, statt öffentliche Accessoren zu verwenden, die möglicherweise Geschäftslogik umfassen.  
  
#### <a name="to-represent-characteristics-of-two-database-columns"></a>So stellen Sie Eigenschaften von zwei Datenbankspalten dar  
  
-   Geben Sie den folgenden Code in die geschweiften Klammern der `Customer`-Klasse in Program.cs ein, oder fügen Sie ihn ein.  
  
     [!code-csharp[DLinqWalk1CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#3)]  
  
## <a name="specifying-the-connection-to-the-northwind-database"></a>Herstellen einer Verbindung zur Beispieldatenbank Northwind  
 In diesem Schritt verwenden Sie ein <xref:System.Data.Linq.DataContext>-Objekt zur Einrichtung einer Verbindung zwischen Ihren codebasierten Datenstrukturen und der Datenbank selbst. Der <xref:System.Data.Linq.DataContext> ist der Hauptkanal, durch den Sie Objekte von der Datenbank abrufen und Änderungen übergeben.  
  
 Sie deklarieren außerdem eine `Table<Customer>` als logische, typisierte Tabelle für Ihre Abfragen der Customers-Tabelle in der Datenbank. Die Erstellung und Ausführung dieser Abfragen erfolgt später.  
  
#### <a name="to-specify-the-database-connection"></a>So definieren Sie die Datenbankverbindung  
  
-   Geben Sie den folgenden Code in die `Main`-Methode ein, oder fügen Sie ihn ein:  
  
     Beachten Sie, dass die Datei `northwnd.mdf` im Ordner linqtest5 angenommen wird. Weitere Informationen finden Sie im Abschnitt zu Voraussetzungen weiter oben in dieser exemplarischen Vorgehensweise.  
  
     [!code-csharp[DLinqWalk1CS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#4)]  
  
## <a name="creating-a-simple-query"></a>Erstellen einer einfachen Abfrage  
 In diesem Schritt erstellen Sie eine Abfrage, um zu ermitteln, welche Kunden in der Customers-Datenbanktabelle aus London stammen. Im Abfragecode in diesem Schritt wird nur die Abfrage beschrieben. Die Abfrage wird nicht ausgeführt. Dieser Ansatz wird als bezeichnet *verzögerte Ausführung*. Weitere Informationen finden Sie unter [Introduction to LINQ queries (C#) (Einführung in LINQ-Abfragen (C#))](~/docs/csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).  
  
 Sie erzeugen auch eine Protokollausgabe, um die SQL-Befehle anzuzeigen, die [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] erzeugt. Diese Protokolllierungsfunktion (die <xref:System.Data.Linq.DataContext.Log%2A> verwendet), eignet sich für das Debugging. Sie stellt außerdem sicher, dass die an die Datenbank übergebenen Befehle Ihre Abfrage genau wiedergeben.  
  
#### <a name="to-create-a-simple-query"></a>So erstellen Sie eine einfache Abfrage  
  
-   Geben Sie den folgenden Code in die `Main`-Methode nach der `Table<Customer>`-Deklaration ein, oder fügen Sie ihn ein:  
  
     [!code-csharp[DLinqWalk1ACS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1ACS/cs/Program.cs#5)]  
  
## <a name="executing-the-query"></a>Ausführen der Abfrage  
 In diesem Schritt führen Sie die Abfrage aus. Die in den vorherigen Schritten erstellten Abfrageausdrücke werden erst ausgewertet, wenn die Ergebnisse benötigt werden. Wenn Sie die `foreach`-Iteration beginnen, wird ein SQL-Befehl in der Datenbank ausgeführt, und Objekte werden erstellt.  
  
#### <a name="to-execute-the-query"></a>So führen Sie die Abfrage aus  
  
1.  Geben Sie den folgenden Code am Ende der `Main`-Methode (nach der Abfragebeschreibung) ein. oder fügen Sie ihn ein:  
  
     [!code-csharp[DLinqWalk1ACS#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1ACS/cs/Program.cs#6)]  
  
2.  Drücken Sie F5, um die Anwendung zu debuggen.  
  
    > [!NOTE]
    >  Wenn die Anwendung einen Laufzeitfehler erzeugt, finden Sie im Abschnitt Problembehandlung der [lernen durch Exemplarische Vorgehensweisen](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md).  
  
     Die Abfrageergebnisse im Konsolenfenster werden wie folgt angezeigt:  
  
     `ID=AROUT, City=London`  
  
     `ID=BSBEV, City=London`  
  
     `ID=CONSH, City=London`  
  
     `ID=EASTC, City=London`  
  
     `ID=NORTS, City=London`  
  
     `ID=SEVES, City=London`  
  
3.  Drücken Sie die EINGABETASTE im Konsolenfenster, um die Anwendung zu schließen.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Die [Exemplarische Vorgehensweise: Beziehungsübergreifendes Abfragen (c#)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-querying-across-relationships-csharp.md) Thema fortgesetzt wird, in dieser exemplarischen Vorgehensweise endet. Die beziehungsübergreifenden Abfragen zeigt, wie [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tabellenübergreifende Abfragen ausführt, ähnlich wie *Joins* in einer relationalen Datenbank.  
  
 Wenn Sie die exemplarische Vorgehensweise zu beziehungsübergreifenden Abfragen absolvieren möchten, stellen Sie sicher, dass Sie die gerade erstellte Lösung speichern, da diese benötigt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Lernen durch exemplarische Vorgehensweisen](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)
