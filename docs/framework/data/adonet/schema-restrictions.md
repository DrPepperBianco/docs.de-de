---
title: "Schemaeinschränkungen"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: 73d2980e-e73c-4987-913a-8ddc93d09144
caps.latest.revision: "3"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: dotnet
ms.openlocfilehash: 4a3cc1f0c27af1ad41e14374b4c155e6b8620f28
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="schema-restrictions"></a>Schemaeinschränkungen
Den optionalen zweiten Parameter von der **GetSchema** Methode ist die Einschränkungen, die verwendet werden, um die Begrenzung des Umfangs der Schemainformationen zurückgegeben und erfolgt eine Übergabe an die **GetSchema** -Methode ein Array von Zeichenfolgen . Die Position im Array bestimmt die Werte, die zurückgegeben werden können. Dies entspricht der Anzahl der Einschränkungen.  
  
 In der folgenden Tabelle werden beispielsweise die Einschränkungen beschrieben, die von der Schemaauflistung "Tables" mithilfe des .NET Framework-Datenanbieters für SQL Server unterstützt werden. Zusätzliche Einschränkungen für SQL Server-Schemaauflistungen werden am Ende dieses Themas aufgeführt.  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catalog|@Catalog|TABLE_CATALOG|1|  
|Besitzer|@Owner|TABLE_SCHEMA|2|  
|Tabelle|@Name|TABLE_NAME|3|  
|TableType|@TableType|TABLE_TYPE|4|  
  
## <a name="specifying-restriction-values"></a>Angeben der Einschränkungswerte  
 Wenn Sie eine der Einschränkungen der Tables-Schemaauflistung verwenden möchten, erstellen Sie ein Zeichenfolgenarray mit vier Elementen und fügen einen Wert in das Element ein, das mit der Einschränkungsnummer übereinstimmt. Z. B. zum Einschränken der Tabellen zurückgegeben, durch die **GetSchema** Methode, um nur die Tabellen im Schema "Sales" legen Sie das zweite Element des Arrays "Sales" vor der Übergabe an die **GetSchema** Methode.  
  
> [!NOTE]
>  Die Einschränkungsauflistungen für den `SqlClient` und den `OracleClient` verfügen über eine zusätzliche `ParameterName`-Spalte. Die Spalte für den Einschränkungsstandard ist zwar aus Gründen der Abwärtskompatibilität vorhanden, wird aber derzeit ignoriert. Verwenden Sie Abfragen mit Parametern statt Zeichenfolgenersetzungen, um das Risiko eines SQL-Injection-Angriffs beim Angeben der Einschränkungswerte zu minimieren.  
  
> [!NOTE]
>  Die Anzahl der Elementen im Array muss kleiner oder gleich der Anzahl der Einschränkungen sein, die für die angegebene Schemaauflistung unterstützt werden, da sonst eine <xref:System.ArgumentException> ausgelöst wird. Es können weniger Elemente als die maximale Anzahl der Einschränkungen vorhanden sein. Es wird davon ausgegangen, dass die fehlenden Einschränkungen NULL (uneingeschränkt) sind.  
  
 Sie können einen verwalteten .NET Framework-Anbieter, um die Liste der unterstützten Einschränkungen durch Aufrufen von Abfragen die **GetSchema** Methode mit dem Namen der schemaauflistung der Einschränkungen, die "Restrictions" lautet. Dabei wird eine <xref:System.Data.DataTable> mit einer Liste der Auflistungsnamen, Einschränkungsnamen, Standardeinschränkungswerte und der Anzahl der Einschränkungen zurückgegeben.  
  
### <a name="example"></a>Beispiel  
 Die folgenden Beispiele veranschaulichen, wie Sie die <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> Methode von der .NET Framework-Datenanbieter für SQL Server <xref:System.Data.SqlClient.SqlConnection> -Klasse zum Abrufen von Schemainformationen zu allen enthaltenen Tabellen die **AdventureWorks**Beispieldatenbank und zum Einschränken der Informationen, die an die Tabellen im "Sales"-Schema zurückgegeben:  
  
```vb  
Imports System.Data.SqlClient  
  
Module Module1  
Sub Main()  
  Dim connectionString As String = _  
    "Data Source=(local);Database=AdventureWorks;" & _  
       "Integrated Security=true;";  
  
  Dim restrictions(3) As String  
  Using connection As New SqlConnection(connectionString)  
    connection.Open()  
  
    'Specify the restrictions.  
    restrictions(1) = "Sales"  
    Dim table As DataTable = connection.GetSchema("Tables", _  
       restrictions)  
  
    ' Display the contents of the table.  
      For Each row As DataRow In table.Rows  
         For Each col As DataColumn In table.Columns  
            Console.WriteLine("{0} = {1}", col.ColumnName, row(col))  
         Next  
         Console.WriteLine("============================")  
      Next  
    Console.WriteLine("Press any key to continue.")  
    Console.ReadKey()  
  End Using  
End Sub  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
  
class Program  
{  
  static void Main()  
  {  
    string connectionString =   
       "Data Source=(local);Database=AdventureWorks;" +  
       "Integrated Security=true;";  
    using (SqlConnection connection =  
       new SqlConnection(connectionString))  
    {  
        connection.Open();  
  
        // Specify the restrictions.  
        string[] restrictions = new string[4];  
        restrictions[1] = "Sales";  
        System.Data.DataTable table = connection.GetSchema(  
          "Tables", restrictions);  
  
        // Display the contents of the table.  
        foreach (System.Data.DataRow row in table.Rows)  
        {  
            foreach (System.Data.DataColumn col in table.Columns)  
            {  
                Console.WriteLine("{0} = {1}",   
                  col.ColumnName, row[col]);  
            }  
            Console.WriteLine("============================");  
        }  
        Console.WriteLine("Press any key to continue.");  
        Console.ReadKey();  
    }  
  }  
  
  private static string GetConnectionString()  
  {  
     // To avoid storing the connection string in your code,  
     // you can retrieve it from a configuration file.  
     return "Data Source=(local);Database=AdventureWorks;" +  
        "Integrated Security=true;";  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
     foreach (System.Data.DataRow row in table.Rows)  
     {  
        foreach (System.Data.DataColumn col in table.Columns)  
        {  
           Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
        }  
     Console.WriteLine("============================");  
     }  
  }  
}  
```  
  
## <a name="sql-server-schema-restrictions"></a>SQL Server-Schemabeschränkungen  
 In den folgenden Tabellen sind die Beschränkungen für SQL Server-Schemaauflistungen aufgeführt.  
  
### <a name="users"></a>Benutzer  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|User_Name|@Name|Name|1|  
  
### <a name="databases"></a>Databases  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|name|@Name|name|1|  
  
### <a name="tables"></a>Tabellen  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catalog|@Catalog|TABLE_CATALOG|1|  
|Besitzer|@Owner|TABLE_SCHEMA|2|  
|Tabelle|@Name|TABLE_NAME|3|  
|TableType|@TableType|TABLE_TYPE|4|  
  
### <a name="columns"></a>Columns  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catalog|@Catalog|TABLE_CATALOG|1|  
|Besitzer|@Owner|TABLE_SCHEMA|2|  
|Tabelle|@Table|TABLE_NAME|3|  
|Spalte|@Column|COLUMN_NAME|4|  
  
### <a name="structuredtypemembers"></a>StructuredTypeMembers  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catalog|@Catalog|TABLE_CATALOG|1|  
|Besitzer|@Owner|TABLE_SCHEMA|2|  
|Tabelle|@Table|TABLE_NAME|3|  
|Spalte|@Column|COLUMN_NAME|4|  
  
### <a name="views"></a>Ansichten  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catalog|@Catalog|TABLE_CATALOG|1|  
|Besitzer|@Owner|TABLE_SCHEMA|2|  
|Tabelle|@Table|TABLE_NAME|3|  
  
### <a name="viewcolumns"></a>ViewColumns  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catalog|@Catalog|VIEW_CATALOG|1|  
|Besitzer|@Owner|VIEW_SCHEMA|2|  
|Tabelle|@Table|VIEW_NAME|3|  
|Spalte|@Column|COLUMN_NAME|4|  
  
### <a name="procedureparameters"></a>ProcedureParameters  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catalog|@Catalog|SPECIFIC_CATALOG|1|  
|Besitzer|@Owner|SPECIFIC_SCHEMA|2|  
|name|@Name|SPECIFIC_NAME|3|  
|Parameter|@Parameter|PARAMETER_NAME|4|  
  
### <a name="procedures"></a>Verfahren  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catalog|@Catalog|SPECIFIC_CATALOG|1|  
|Besitzer|@Owner|SPECIFIC_SCHEMA|2|  
|name|@Name|SPECIFIC_NAME|3|  
|Typ|@Type|ROUTINE_TYPE|4|  
  
### <a name="indexcolumns"></a>IndexColumns  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catalog|@Catalog|db_name()|1|  
|Besitzer|@Owner|user_name()|2|  
|Tabelle|@Table|o.name|3|  
|ConstraintName|@ConstraintName|x.name|4|  
|Spalte|@Column|c.name|5|  
  
### <a name="indexes"></a>Indexes  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catalog|@Catalog|db_name()|1|  
|Besitzer|@Owner|user_name()|2|  
|Tabelle|@Table|o.name|3|  
  
### <a name="userdefinedtypes"></a>UserDefinedTypes  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|assembly_name|@AssemblyName|assemblies.name|1|  
|udt_name|@UDTName|types.assembly_class|2|  
  
### <a name="foreignkeys"></a>ForeignKeys  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catalog|@Catalog|CONSTRAINT_CATALOG|1|  
|Besitzer|@Owner|CONSTRAINT_SCHEMA|2|  
|Tabelle|@Table|TABLE_NAME|3|  
|name|@Name|CONSTRAINT_NAME|4|  
  
## <a name="sql-server-2008-schema-restrictions"></a>SQL Server 2008-Schemabeschränkungen  
 In den folgenden Tabellen sind die Beschränkungen für SQL Server 2008-Schemaauflistungen aufgeführt. Diese Beschränkungen gelten ab Version 3.5 SP1 von .NET Framework und SQL Server 2008. Sie werden in früheren Versionen von .NET Framework und SQL Server nicht unterstützt.  
  
### <a name="columnsetcolumns"></a>ColumnSetColumns  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catalog|@Catalog|TABLE_CATALOG|1|  
|Besitzer|@Owner|TABLE_SCHEMA|2|  
|Tabelle|@Table|TABLE_NAME|3|  
  
### <a name="allcolumns"></a>AllColumns  
  
|Einschränkungsname|Parametername|Einschränkungsstandard|Einschränkungsnummer|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catalog|@Catalog|TABLE_CATALOG|1|  
|Besitzer|@Owner|TABLE_SCHEMA|2|  
|Tabelle|@Table|TABLE_NAME|3|  
|Spalte|@Column|COLUMN_NAME|4|  
  
## <a name="see-also"></a>Siehe auch  
 [ADO.NET Managed Provider und DataSet Developer Center](http://go.microsoft.com/fwlink/?LinkId=217917)
