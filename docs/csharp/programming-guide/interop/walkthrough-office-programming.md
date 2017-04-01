---
title: 'Exemplarische Vorgehensweise: Office-Programmierung (C# und Visual Basic) | Microsoft-Dokumentation'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- Office, programming in Visual Basic and C#
- Office programming [C#]
- Office programming [Visual Basic]
ms.assetid: 519cff31-f80b-4f0e-a56b-26358d0f8c51
caps.latest.revision: 46
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f93a5403660ca850d6650a1a6406395dfa2cc2e5
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-office-programming-c-and-visual-basic"></a>Exemplarische Vorgehensweise: Office-Programmierung (C# und Visual Basic)
Ab Visual Studio gibt es neue Funktionen in C# und Visual Basic, die die Microsoft Office-Programmierung verbessern. Jede Sprache verfügt über zusätzliche Funktionen, die bereits in der anderen Sprache existieren.  
  
 Zu den neuen Funktionen in C# gehören benannte und optionale Argumente, Rückgabewerte vom Typ `dynamic` und in der COM-Programmierung die Möglichkeit, das Schlüsselwort `ref` auszulassen und auf indizierte Eigenschaften zuzugreifen. Die neuen Funktionen in Visual Basic umfassen automatisch implementierte Eigenschaften, Anweisungen in Lambda-Ausdrücken sowie Auflistungsinitialisierer.  
  
 Beide Sprachen ermöglichen das Einbetten von Typinformationen, wodurch Assemblys bereitgestellt werden können, die mit COM-Komponenten interagieren, ohne primäre Interop-Assemblys (PIAs) auf dem Computer des Benutzers bereitzustellen. Weitere Informationen finden Sie unter [Exemplarische Vorgehensweise: Einbetten von Typen aus verwalteten Assemblys](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21).  
  
 Diese exemplarische Vorgehensweise veranschaulicht die neuen Funktionen im Kontext der Office-Programmierung, aber viele von ihnen sind auch bei der allgemeinen Programmierung nützlich. In der exemplarischen Vorgehensweise verwenden Sie zunächst eine Excel-Add-In-Anwendung, um eine Excel-Arbeitsmappe zu erstellen. Sie werden dann ein Word-Dokument erstellen, das einen Link zur Arbeitsmappe enthält. Abschließend sehen Sie, wie die PIA-Abhängigkeit aktiviert oder deaktiviert werden kann.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 Zum Durchführen dieser exemplarischen Vorgehensweise müssen Microsoft Office Excel 2013 (oder Version 2007 oder höher) und Microsoft Office Word 2013 (oder Version 2007 oder höher) auf Ihrem Computer installiert sein.  
  
 Wenn Sie ein Betriebssystem verwenden, das älter ist als [!INCLUDE[windowsver](../../../csharp/programming-guide/interop/includes/windowsver_md.md)], stellen Sie sicher, dass [!INCLUDE[dnprdnlong](../../../csharp/programming-guide/events/includes/dnprdnlong_md.md)] installiert ist.  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-set-up-an-excel-add-in-application"></a>So richten Sie eine Excel-Add-In-Anwendung ein  
  
1.  Starten Sie Visual Studio.  
  
2.  Zeigen Sie im Menü **Datei** auf **Neu**, und klicken Sie dann auf **Projekt**.  
  
3.  Erweitern Sie im Bereich **Installierte Vorlagen** die Option **Visual Basic** oder **Visual C#**, erweitern Sie dann **Office**, und klicken Sie auf **2013** (oder **2010** oder **2007**).  
  
4.  Klicken Sie im Bereich **Vorlagen** auf **Excel 2013 Add-In** (oder **Excel 2010 Add-In** oder **Excel 2007 Add-In**).  
  
5.  Sehen Sie am oberen Rand des Bereichs **Vorlagen** nach, um sicherzustellen, dass **.NET Framework 4** oder eine höhere Version im Feld **Zielframework** angezeigt wird.  
  
6.  Geben Sie, wenn gewünscht, einen Namen für das Projekt in das Feld **Name** ein.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Das neue Projekt wird im **Projektmappen-Explorer** angezeigt.  
  
### <a name="to-add-references"></a>So fügen Sie Verweise hinzu  
  
1.  Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Projektnamen, und klicken Sie dann auf **Verweis hinzufügen**. Das Dialogfeld **Verweis hinzufügen** wird angezeigt.  
  
2.  Wählen Sie auf der Registerkarte **Assemblys** die Option **Microsoft.Office.Interop.Excel**, Version 15.0.0.0 (oder Version 14.0.0.0 für Excel 2010 oder Version 12.0.0.0 für Excel 2007), in der Liste **Komponentenname** aus, und halten Sie dann die STRG-Taste gedrückt, während Sie **Microsoft.Office.Interop.Word**, Version 15.0.0.0 (oder Version 14.0.0.0 für Word 2010 oder 12.0.0.0 für Word 2007), auswählen.  Wenn keine Assemblys sichtbar sind, müssen Sie unter Umständen sicherstellen, dass sie installiert sind und angezeigt werden (siehe [Vorgehensweise: Installieren von primären Interopassemblys für Office](http://msdn.microsoft.com/library/92948fcc-76c6-4b08-ba63-cab59dd60eb1)).  
  
3.  Klicken Sie auf **OK**.  
  
### <a name="to-add-necessary-imports-statements-or-using-directives"></a>So fügen Sie erforderliche Imports-Anweisungen oder using-Anweisungen hinzu  
  
1.  Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf die Datei **ThisAddIn.vb** oder **ThisAddIn.cs**, und klicken Sie dann auf **Code anzeigen**.  
  
2.  Fügen Sie die folgenden `Imports`-Anweisungen (Visual Basic) oder `using`-Direktiven (C#) am Anfang der Codedatei ein, wenn sie noch nicht vorhanden sind.  
  
     [!code-cs[csOfficeWalkthrough#1](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_1.cs)]
     [!code-vb[csOfficeWalkthrough#1](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_1.vb)]  
  
### <a name="to-create-a-list-of-bank-accounts"></a>So erstellen Sie eine Liste mit Bankkonten  
  
1.  Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Projektnamen, klicken Sie auf **Hinzufügen** und dann auf **Klasse**. Benennen Sie die Klasse "Account.vb", wenn Sie Visual Basic verwenden, oder "Account.cs", wenn Sie C# verwenden. Klicken Sie auf **Hinzufügen**.  
  
2.  Ersetzen Sie die Definition der `Account`-Klasse durch den folgenden Code. Die Klassendefinitionen verwenden *automatisch implementierte Eigenschaften*, die neu in Visual Basic in Visual Studio 2010 sind. Weitere Informationen finden Sie unter [Automatisch implementierte Eigenschaften](../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md).  
  
     [!code-cs[csOfficeWalkthrough#2](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_2.cs)]
     [!code-vb[csOfficeWalkthrough#2](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_2.vb)]  
  
3.  Fügen Sie den folgenden Code in die `bankAccounts`-Methode in "ThisAddIn.vb" oder "ThisAddIn.cs" ein, um eine `ThisAddIn_Startup`-Liste mit zwei Konten zu erstellen. Die Listendeklarationen verwenden *Auflistungsinitialisierer*, die neu in Visual Basic in Visual Studio 2010 sind. Weitere Informationen finden Sie unter [Auflistungsinitialisierer](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md).  
  
     [!code-cs[csOfficeWalkthrough#3](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_3.cs)]
     [!code-vb[csOfficeWalkthrough#3](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_3.vb)]  
  
### <a name="to-export-data-to-excel"></a>So exportieren Sie Daten nach Excel  
  
1.  Fügen Sie in der gleichen Datei die folgende Methode der `ThisAddIn`-Klasse hinzu. Die Methode richtet eine Excel-Arbeitsmappe ein, in die die Daten exportiert werden.  
  
     [!code-cs[csOfficeWalkthrough#4](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_4.cs)]
     [!code-vb[csOfficeWalkthrough#4](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_4.vb)]  
  
     Bei dieser Methode werden zwei neue C#-Funktionen verwendet. Beide Funktionen existieren bereits in Visual Basic.  
  
    -   Die Methode [Add](http://go.microsoft.com/fwlink/?LinkId=210910) hat einen *optionalen Parameter* zum Angeben einer bestimmten Vorlage. Optionale Parameter, die in [!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp_dev10_long_md.md)] neu sind, ermöglichen es Ihnen, das Argument für diesen Parameter auszulassen, wenn Sie den Standardwert des Parameters verwenden möchten. Da im vorherigen Beispiel kein Argument gesendet wurde, verwendet `Add` die Standardvorlage und erstellt eine neue Arbeitsmappe. Die entsprechende Anweisung in früheren Versionen von C# erfordert ein Platzhalterargument: `excelApp.Workbooks.Add(Type.Missing)`.  
  
         Weitere Informationen finden Sie unter [Benannte und optionale Argumente](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md).  
  
    -   Die Eigenschaften `Range` und `Offset` des [range](http://go.microsoft.com/fwlink/?LinkId=210911)-Objekts verwenden die Funktion *Indizierte Eigenschaften*. Diese Funktion ermöglicht es Ihnen, diese Eigenschaften von COM-Typen zu nutzen, indem Sie die folgende typische C#-Syntax verwenden. Indizierte Eigenschaften ermöglichen es Ihnen außerdem, die `Value`-Eigenschaft des `Range`-Objekts zu verwenden, sodass Sie die `Value2`-Eigenschaft nicht mehr verwenden müssen. Die `Value`-Eigenschaft ist indiziert, der Index ist jedoch optional. Optionale Argumente und indizierte Eigenschaften arbeiten im folgenden Beispiel zusammen.  
  
         [!code-cs[csOfficeWalkthrough#5](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_5.cs)]  
  
         In früheren Versionen der Sprache ist die folgende spezielle Syntax erforderlich.  
  
         [!code-cs[csOfficeWalkthrough#6](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_6.cs)]  
  
         Sie können nicht Ihre eigenen indizierten Eigenschaften erstellen. Die Funktion unterstützt nur die Nutzung vorhandener indizierter Eigenschaften.  
  
         Weitere Informationen finden Sie unter [Vorgehensweise: Indizierte Eigenschaften bei der COM-Interop-Programmierung](../../../csharp/programming-guide/interop/how-to-use-indexed-properties-in-com-interop-rogramming.md).  
  
2.  Fügen Sie den folgenden Code am Ende von `DisplayInExcel` hinzu, um die Spaltenbreite an den Inhalt anzupassen.  
  
     [!code-cs[csOfficeWalkthrough#7](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_7.cs)]
     [!code-vb[csOfficeWalkthrough#7](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_7.vb)]  
  
     Diese Ergänzungen veranschaulichen eine weitere neue Funktion in C# 2010: die Behandlung von `Object`-Werten, die von COM-Hosts wie z.B. Office zurückgegeben wurden, als wären sie vom Typ [dynamic](../../../csharp/language-reference/keywords/dynamic.md). Dies geschieht automatisch, wenn **Einbetten von Interop-Typen** auf den Standardwert `True` festgelegt ist oder gleichermaßen wenn die [/link](../../../csharp/language-reference/compiler-options/link-compiler-option.md)-Compileroption auf die Assembly verweist. Der Typ `dynamic` ermöglicht eine späte Bindung, bereits in Visual Basic verfügbar, und vermeidet die in Visual C# 2008 und in früheren Sprachversionen erforderliche explizite Umwandlung.  
  
     `excelApp.Columns[1]` gibt z.B.`Object` zurück, und `AutoFit` ist eine [Range](http://go.microsoft.com/fwlink/?LinkId=210911)-Methode von Excel. Ohne `dynamic` müssen Sie das von `excelApp.Columns[1]` zurückgegebene Objekt als eine Instanz von `Range` umwandeln, bevor Sie die Methode `AutoFit` aufrufen.  
  
     [!code-cs[csOfficeWalkthrough#8](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_8.cs)]  
  
     Weitere Informationen zum Einbetten von Interop-Typen finden Sie in den Verfahren "So suchen Sie den PIA-Verweis" und "So stellen Sie die PIA-Abhängigkeit wieder her" weiter unten in diesem Thema. Weitere Informationen zu `dynamic` finden Sie unter [dynamic](../../../csharp/language-reference/keywords/dynamic.md) oder [Verwenden von dynamischen Typen](../../../csharp/programming-guide/types/using-type-dynamic.md).  
  
### <a name="to-invoke-displayinexcel"></a>So rufen Sie DisplayInExcel auf  
  
1.  Fügen Sie den folgenden Code am Ende der `ThisAddIn_StartUp`-Methode hinzu. Der Aufruf von `DisplayInExcel` enthält zwei Argumente. Das erste Argument ist der Name der Liste mit Konten, die verarbeitet werden sollen. Das zweite Argument ist ein mehrzeiliger Lambda-Ausdruck, der definiert, wie die Daten verarbeitet werden. Die `ID`- und `balance`-Werte für jedes Konto werden in angrenzenden Zellen angezeigt, und die Zeile wird rot dargestellt, wenn der Saldo kleiner als Null ist. Mehrzeilige Lambdaausdrücke sind eine neue Funktion in Visual Basic 2010. Weitere Informationen finden Sie unter [Lambda Expressions (Lambdaausdrücke)](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
     [!code-cs[csOfficeWalkthrough#9](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_9.cs)]
     [!code-vb[csOfficeWalkthrough#9](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_9.vb)]  
  
2.  Drücken Sie F5, um das Programm auszuführen. Ein Excel-Arbeitsblatt wird mit den Kontendaten angezeigt.  
  
### <a name="to-add-a-word-document"></a>So fügen Sie ein Word-Dokument hinzu  
  
1.  Fügen Sie den folgenden Code am Ende der `ThisAddIn_StartUp`-Methode hinzu, um ein Word-Dokument zu erstellen, das einen Link zur Excel-Arbeitsmappe enthält.  
  
     [!code-cs[csOfficeWalkthrough#10](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_10.cs)]
     [!code-vb[csOfficeWalkthrough#10](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_10.vb)]  
  
     Dieser Code veranschaulicht mehrere der neuen Funktionen in C#: die Möglichkeit, das `ref`-Schlüsselwort in der COM-Programmierung auszulassen, benannte Argumente sowie optionale Argumente. Diese Funktionen sind bereits in Visual Basic vorhanden. Die Methode [PasteSpecial](http://go.microsoft.com/fwlink/?LinkId=147099) verfügt über sieben Parameter, die als optionale Verweisparameter definiert sind. Vor Visual C# 2010 mussten Sie Objektvariablen definieren, die als Argumente für die sieben Parameter verwendet wurden, auch wenn Sie keine aussagekräftigen Werte zum Übertragen hatten. Benannte und optionale Argumente ermöglichen es Ihnen, die Parameter festzulegen, auf die Sie namentlich zugreifen möchten, und Argumente nur an diese Parameter zu senden. In diesem Beispiel werden Argumente gesendet, um anzugeben, dass ein Link zur Arbeitsmappe in der Zwischenablage erstellt werden soll (Parameter `Link`) und dass der Link im Word-Dokument als Symbol angezeigt werden soll (Parameter `DisplayAsIcon`). Visual C# 2010 ermöglicht auch das Weglassen des `ref`-Schlüsselworts für diese Argumente. Vergleichen Sie das folgende Codesegment von Visual C# 2008 mit der einzelnen, in Visual C# 2010 erforderlichen Zeile:  
  
     [!code-cs[csOfficeWalkthrough#11](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_11.cs)]  
  
### <a name="to-run-the-application"></a>So führen Sie die Anwendung aus  
  
1.  Drücken Sie F5, um die Anwendung auszuführen. Excel wird gestartet und zeigt eine Tabelle mit den Informationen der beiden Konten in `bankAccounts` an. Anschließend wird ein Word-Dokument angezeigt, das einen Link zur Excel-Tabelle enthält.  
  
### <a name="to-clean-up-the-completed-project"></a>So bereinigen Sie das abgeschlossene Projekt  
  
1.  Klicken Sie in Visual Studio auf **Projektmappe bereinigen** im Menü **Erstellen**. Andernfalls wird das Add-In jedes Mal ausgeführt, wenn Sie Excel auf Ihrem Computer öffnen.  
  
### <a name="to-find-the-pia-reference"></a>So suchen Sie den PIA-Verweis  
  
1.  Führen Sie die Anwendung erneut aus, klicken Sie jedoch nicht auf **Projektmappe bereinigen**.  
  
2.  Klicken Sie im Menü **Start** auf **Alle Programme**. Klicken Sie anschließend auf **Microsoft Visual Studio 2013**, dann auf **Visual Studio-Tools** und dann auf **Visual Studio-Eingabeaufforderung (2013)**.  
  
3.  Geben Sie im Fenster „Visual Studio-Eingabeaufforderung (2013)“ `ildasm` ein, und drücken Sie dann die EINGABETASTE. Das IL DASM-Fenster wird angezeigt.  
  
4.  Klicken Sie im IL DASM-Fenster im Menü **Datei** auf **Öffnen**. Doppelklicken Sie auf **Visual Studio 2013** und dann noch einmal auf **Projekte**. Öffnen Sie den Ordner für das Projekt, und suchen Sie im Ordner „bin/Debug“ nach der Datei *Projektname*.dll. Doppelklicken Sie auf *Projektname*.dll. In einem neuen Fenster werden die Attribute Ihres Projekts sowie Verweise auf andere Module und Assemblys angezeigt. Beachten Sie, dass die Namespaces `Microsoft.Office.Interop.Excel` und `Microsoft.Office.Interop.Word` in der Assembly enthalten sind. Standardmäßig importiert der Compiler in Visual Studio 2013 die benötigten Typen aus einer referenzierten PIA in Ihre Assembly.  
  
     Weitere Informationen finden Sie unter [Vorgehensweise: Ansichtsassemblyinhalt](http://msdn.microsoft.com/library/fb7baaab-4c0d-47ad-8fd3-4591cf834709).  
  
5.  Doppelklicken Sie auf das Symbol **MANIFEST**. Es wird ein Fenster angezeigt, das eine Liste von Assemblys enthält, die vom Projekt referenzierte Elemente enthalten. `Microsoft.Office.Interop.Excel` und `Microsoft.Office.Interop.Word` sind nicht in der Liste enthalten. Da die Typen, die das Projekt benötigt, in die Assembly importiert wurden, sind keine Verweise auf eine PIA erforderlich. Dadurch wird die Bereitstellung vereinfacht. Die PIAs müssen nicht auf dem Computer des Benutzers vorhanden sein, und da für eine Anwendung keine bestimmte PIA-Version bereitgestellt werden muss, können die Anwendungen so konzipiert sein, dass sie mit mehreren Versionen von Office funktionieren, sofern die erforderlichen APIs in allen Versionen vorhanden sind.  
  
     Da die Bereitstellung von primären Interop-Assemblys nicht mehr benötigt wird, können Sie eine Anwendung in erweiterten Szenarien erstellen, bei denen mehrere Versionen von Office, einschließlich früherer Versionen, verwendet werden. Dies funktioniert jedoch nur, wenn Ihr Code keine APIs verwendet, die nicht in der Version von Office verfügbar sind, mit der Sie arbeiten. Es ist nicht immer klar, ob eine bestimmte API in einer früheren Version verfügbar war; daher wird die Arbeit mit früheren Office-Versionen nicht empfohlen.  
  
    > [!NOTE]
    >  Office hat vor Office 2003 keine PIAs veröffentlicht. Aus diesem Grund besteht die einzige Möglichkeit zum Generieren einer Interop-Assembly für Office 2002 oder früheren Versionen darin, den COM-Verweis zu importieren.  
  
6.  Schließen Sie das Manifest-Fenster und das Assembly-Fenster.  
  
### <a name="to-restore-the-pia-dependency"></a>So stellen Sie die PIA-Abhängigkeit wieder her  
  
1.  Klicken Sie im **Projektmappen-Explorer** auf die Schaltfläche **Alle Dateien anzeigen**. Erweitern Sie den Ordner **Verweise**, und wählen Sie **Microsoft.Office.Interop.Excel** aus. Drücken Sie F4, um das Fenster **Eigenschaften** anzuzeigen.  
  
2.  Ändern Sie im Fenster **Eigenschaften** die Eigenschaft **Einbetten von Interop-Typen** von **True** zu **False**.  
  
3.  Wiederholen Sie die Schritte 1 und 2 in dieser Prozedur für `Microsoft.Office.Interop.Word`.  
  
4.  Kommentieren Sie in C# die beiden Aufrufe von `Autofit` am Ende der `DisplayInExcel`-Methode aus.  
  
5.  Drücken Sie F5, um sicherzustellen, dass das Projekt immer noch ordnungsgemäß ausgeführt wird.  
  
6.  Wiederholen Sie die Schritte 1 bis 3 der vorherigen Prozedur, um das Assembly-Fenster zu öffnen. Beachten Sie, dass `Microsoft.Office.Interop.Word` und `Microsoft.Office.Interop.Excel` nicht mehr in der Liste der eingebetteten Assemblys sind.  
  
7.  Doppelklicken Sie auf das Symbol **MANIFEST**, und führen Sie einen Bildlauf durch die Liste der referenzierten Assemblys durch. `Microsoft.Office.Interop.Word` und `Microsoft.Office.Interop.Excel` befinden sich in der Liste. Da die Anwendung auf die Excel- und Word-PIAs verweist und die Eigenschaft **Einbetten von Interop-Typen** auf **False** gesetzt ist, müssen beide Assemblys auf dem Computer des Endbenutzers vorhanden sein.  
  
8.  Klicken Sie in Visual Studio im Menü **Erstellen** auf **Projektmappe bereinigen**, um das abgeschlossene Projekt zu bereinigen.  
  
## <a name="see-also"></a>Siehe auch  
 [Automatisch implementierte Eigenschaften](../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md)   
 [Automatisch implementierte Eigenschaften](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)   
 [Auflistungsinitialisierer](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)   
 [Objekt- und Auflistungsinitialisierer](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)   
 [Optionale Parameter](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [Übergeben von Argumenten nach Position und Name](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [Benannte und optionale Argumente](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)   
 [Frühes und spätes Binden](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)   
 [dynamic](../../../csharp/language-reference/keywords/dynamic.md)   
 [Verwenden von dynamischen Typen](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [Lambda Expressions (Lambdaausdrücke)](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [Lambda Expressions (Lambdaausdrücke)](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [Vorgehensweise: Indizierte Eigenschaften bei der COM-Interop-Programmierung](../../../csharp/programming-guide/interop/how-to-use-indexed-properties-in-com-interop-rogramming.md)   
 [Exemplarische Vorgehensweise: Einbetten von Typinformationen aus Microsoft Office-Assemblys](http://msdn.microsoft.com/library/85b55e05-bc5e-4665-b6ae-e1ada9299fd3)   
 [Exemplarische Vorgehensweise: Einbetten von Typen aus verwalteten Assemblys](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21)   
 [Exemplarische Vorgehensweise: Erstellen des ersten VSTO-Add-Ins für Excel](http://msdn.microsoft.com/library/a855e2be-3ecf-4112-a7f5-ec0f7fad3b5f)   
 [COM-Interop](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Interoperabilität](../../../csharp/programming-guide/interop/index.md)