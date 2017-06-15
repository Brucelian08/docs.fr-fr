---
title: "&#201;tats et versions de ligne | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2e6642c9-bfc6-425c-b3a7-e4912ffa6c1f
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# &#201;tats et versions de ligne
ADO.NET gère les lignes des tables à l'aide des états et des versions de ligne.  Un état de ligne indique le statut d'une ligne ; les versions de ligne conservent les valeurs stockées dans une ligne pendant leur modification, notamment les valeurs actuelles, d'origine et par défaut.  Par exemple, une fois qu'une modification a été apportée à une colonne dans une ligne, la ligne possède un état de ligne `Modified` et deux versions de ligne : `Current`, qui contient les valeurs de ligne actuelles et `Original`, qui renferme les valeurs de ligne avant la modification de la colonne.  
  
 Chaque objet <xref:System.Data.DataRow> a la propriété <xref:System.Data.DataRow.RowState%2A> que vous pouvez examiner pour déterminer l'état actuel de la ligne.  Le tableau suivant fournit une brève description de chacune des valeurs d'énumération `RowState`.  
  
|Valeur RowState|Description|  
|---------------------|-----------------|  
|<xref:System.Data.DataRowState>|Aucune modification n'a été apportée depuis le dernier appel à `AcceptChanges` ou depuis la création de la ligne par `DataAdapter.Fill`.|  
|<xref:System.Data.DataRowState>|La ligne a été ajoutée à la table mais la `AcceptChanges` n'a pas été appelé.|  
|<xref:System.Data.DataRowState>|Certains éléments de la ligne ont été modifiés.|  
|<xref:System.Data.DataRowState>|La ligne a été supprimée d'une table et `AcceptChanges` n'a pas été appelé.|  
|<xref:System.Data.DataRowState>|La ligne ne fait partie d'aucun `DataRowCollection`.  Le `RowState` d'une ligne nouvellement créée prend la valeur `Detached`.  Une fois le `DataRow` ajouté au `DataRowCollection` à l'aide de l'appel à la méthode `Add`, la propriété `RowState` prend la valeur `Added`.<br /><br /> `Detached` est également défini pour une ligne qui a été supprimée d'un `DataRowCollection` à l'aide de la méthode `Remove` ou par la méthode `Delete` suivie de la méthode `AcceptChanges`.|  
  
 Lorsque `AcceptChanges` est appelé sur un <xref:System.Data.DataSet>, <xref:System.Data.DataTable>, ou sur un <xref:System.Data.DataRow>, toutes les lignes avec un état de ligne `Deleted` sont supprimées.  Un état de ligne `Unchanged` est attribué aux autres lignes et les valeurs de la version de ligne `Original` sont remplacées par celles de la version de ligne `Current`.  Lorsque `RejectChanges` est appelé, toutes les lignes avec un état de ligne `Added` sont supprimées.  Un état de ligne `Unchanged` est attribué aux autres lignes et les valeurs de la version de ligne `Current` sont remplacées par celles de la version de ligne `Original`.  
  
 Vous pouvez afficher les différentes versions de ligne d'une ligne en passant un paramètre <xref:System.Data.DataRowVersion> avec la référence de colonne, comme le montre l'exemple suivant.  
  
```vb  
Dim custRow As DataRow = custTable.Rows(0)  
Dim custID As String = custRow("CustomerID", DataRowVersion.Original).ToString()  
  
```  
  
```csharp  
DataRow custRow = custTable.Rows[0];  
string custID = custRow["CustomerID", DataRowVersion.Original].ToString();  
```  
  
 Le tableau suivant fournit une brève description de chacune des valeurs d'énumération `DataRowVersion`.  
  
|Valeur DataRowVersion|Description|  
|---------------------------|-----------------|  
|<xref:System.Data.DataRowVersion>|Les valeurs actuelles de la ligne.  Cette version de ligne n'existe pas pour les lignes ayant un `RowState` `Deleted`.|  
|<xref:System.Data.DataRowVersion>|Version de ligne par défaut d'une ligne particulière.  La version de ligne par défaut d'une ligne `Added`, `Modified` ou `Unchanged` est `Current`.  La version de ligne par défaut d'une ligne `Deleted` est `Original`.  La version de ligne par défaut d'une ligne `Detached` est `Proposed`.|  
|<xref:System.Data.DataRowVersion>|Les valeurs d'origine de la ligne.  Cette version de ligne n'existe pas pour les lignes ayant un `RowState` `Added`.|  
|<xref:System.Data.DataRowVersion>|Les valeurs proposées de la ligne.  Cette version de ligne existe pendant une opération de modification sur une ligne ou pour une ligne qui ne fait pas partie d'un `DataRowCollection`.|  
  
 Vous pouvez vérifier si un `DataRow` possède une version de ligne particulière en appelant la méthode <xref:System.Data.DataRow.HasVersion%2A> et en transmettant un `DataRowVersion` comme argument.  Par exemple, `DataRow.HasVersion(DataRowVersion.Original)` retournera la valeur `false` pour des lignes qui ont été ajoutées avant l'appel à la méthode `AcceptChanges`.  
  
 L'exemple de code suivant affiche les valeurs dans toutes les lignes supprimées d'une table.  Les lignes `Deleted` n'ont pas de version de ligne `Current`, vous devez donc passer `DataRowVersion.Original` lors de l'accès aux valeurs de colonne.  
  
```vb  
Dim catTable As DataTable = catDS.Tables("Categories")  
  
Dim delRows() As DataRow = catTable.Select(Nothing, Nothing, DataViewRowState.Deleted)  
  
Console.WriteLine("Deleted rows:" & vbCrLf)  
  
Dim catCol As DataColumn  
Dim delRow As DataRow  
  
For Each catCol In catTable.Columns  
  Console.Write(catCol.ColumnName & vbTab)  
Next  
Console.WriteLine()  
  
For Each delRow In delRows  
  For Each catCol In catTable.Columns  
    Console.Write(delRow(catCol, DataRowVersion.Original) & vbTab)  
  Next  
  Console.WriteLine()  
Next  
  
```  
  
```csharp  
DataTable catTable = catDS.Tables["Categories"];  
  
DataRow[] delRows = catTable.Select(null, null, DataViewRowState.Deleted);  
  
Console.WriteLine("Deleted rows:\n");  
  
foreach (DataColumn catCol in catTable.Columns)  
  Console.Write(catCol.ColumnName + "\t");  
Console.WriteLine();  
  
foreach (DataRow delRow in delRows)  
{  
  foreach (DataColumn catCol in catTable.Columns)  
    Console.Write(delRow[catCol, DataRowVersion.Original] + "\t");  
  Console.WriteLine();  
}  
```  
  
## Voir aussi  
 [Manipulation de données dans un DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [Objets DataSet, DataTable et DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [DataAdapters et DataReaders](../../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Fournisseurs managés ADO.NET et Centre de développement de DataSet](http://go.microsoft.com/fwlink/?LinkId=217917)