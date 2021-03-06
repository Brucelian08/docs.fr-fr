---
title: Fournisseur EntityClient pour Entity Framework
ms.date: 03/30/2017
ms.assetid: 8c5db787-78e6-4a34-8dc1-188bca0aca5e
ms.openlocfilehash: 1bafdc250c7edc009352d668e8ee7962a86fe8bf
ms.sourcegitcommit: 3c1c3ba79895335ff3737934e39372555ca7d6d0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43806171"
---
# <a name="entityclient-provider-for-the-entity-framework"></a>Fournisseur EntityClient pour Entity Framework
Le fournisseur EntityClient est un fournisseur de données utilisé par les applications Entity Framework pour accéder à des données décrites dans un modèle conceptuel. Pour plus d’informations sur les modèles conceptuels, consultez [de modélisation et mappage](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md). EntityClient utilise d'autres fournisseurs de données .NET Framework pour accéder à la source de données. Par exemple, EntityClient utilise le fournisseur de données .NET Framework pour SQL Server (SqlClient) lors de l'accès à une base de données SQL Server. Pour plus d’informations sur le fournisseur SqlClient, consultez [SqlClient pour Entity Framework](../../../../../docs/framework/data/adonet/ef/sqlclient-for-the-entity-framework.md). Le fournisseur EntityClient est implémenté dans l'espace de noms <xref:System.Data.EntityClient>.  
  
## <a name="managing-connections"></a>Gestion des connexions  
 Le [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] s’appuie sur spécifiques au stockage [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)] des fournisseurs de données en fournissant un <xref:System.Data.EntityClient.EntityConnection> à un fournisseur de données sous-jacent et de la base de données relationnelle. Pour construire un <xref:System.Data.EntityClient.EntityConnection> de l’objet, vous devez référencer un ensemble de métadonnées qui contient les modèles nécessaires et de mappage et également une chaîne de connexion et de nom de fournisseur des données de stockage spécifique. Après le <xref:System.Data.EntityClient.EntityConnection> est en place, les entités sont accessibles via les classes générées à partir du modèle conceptuel.  
  
 Vous pouvez spécifier une chaîne de connexion dans le fichier app.config.  
  
 <xref:System.Data.EntityClient> comprend également la classe <xref:System.Data.EntityClient.EntityConnectionStringBuilder>. Cette classe permet aux développeurs de créer par programme des chaînes de connexion correctes du point de vue syntaxique, et d'analyser et régénérer les chaînes de connexion existantes, à l'aide des propriétés et des méthodes de la classe. Pour plus d’informations, consultez [Comment : créer une chaîne de connexion EntityConnection](../../../../../docs/framework/data/adonet/ef/how-to-build-an-entityconnection-connection-string.md).  
  
## <a name="creating-queries"></a>Création de requêtes  
 Le [!INCLUDE[esql](../../../../../includes/esql-md.md)] language est un dialecte indépendant du stockage de SQL qui fonctionne directement avec les schémas d’entité conceptuels et prend en charge les concepts Entity Data Model comme l’héritage et les relations. Le <xref:System.Data.EntityClient.EntityCommand> classe est utilisée pour exécuter un [!INCLUDE[esql](../../../../../includes/esql-md.md)] commande sur un modèle d’entité. Au moment de la construction d'objets <xref:System.Data.EntityClient.EntityCommand>, vous pouvez spécifier un nom de procédure stockée ou un texte de requête. [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] utilise des fournisseurs de données de stockage pour traduire le langage [!INCLUDE[esql](../../../../../includes/esql-md.md)] générique en requêtes de stockage. Pour plus d’informations sur l’écriture [!INCLUDE[esql](../../../../../includes/esql-md.md)] de requêtes, consultez [langage Entity SQL](../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md).  
  
 L’exemple suivant crée un <xref:System.Data.EntityClient.EntityCommand> objet et lui affecte un [!INCLUDE[esql](../../../../../includes/esql-md.md)] requête de texte à son <xref:System.Data.EntityClient.EntityCommand.CommandText%2A?displayProperty=nameWithType> propriété. Cela [!INCLUDE[esql](../../../../../includes/esql-md.md)] requête demande les produits classés par prix courant du modèle conceptuel. Le code suivant fait une totale abstraction du modèle de stockage.  
  
 `EntityCommand cmd = conn.CreateCommand();`  
  
 `cmd.CommandText = @"` `SELECT VALUE p`  
  
 `FROM AdventureWorksEntities.Product AS p`  
  
 `ORDER BY p.ListPrice ";`  
  
## <a name="executing-queries"></a>Exécution de requêtes  
 Lorsqu'une requête est exécutée, elle est analysée et convertie en arborescence de commandes canonique. Tous les traitements ultérieurs sont exécutés sur l'arborescence de commandes. L'arborescence de commandes est le moyen de communication entre <xref:System.Data.EntityClient> et le fournisseur de données [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] sous-jacent, tel que <xref:System.Data.SqlClient>.  
  
 <xref:System.Data.EntityClient.EntityDataReader> expose les résultats de l'exécution d'un objet <xref:System.Data.EntityClient.EntityCommand> sur un modèle conceptuel. Pour exécuter la commande qui retourne l'objet <xref:System.Data.EntityClient.EntityDataReader>, appelez la méthode <xref:System.Data.EntityClient.EntityCommand.ExecuteReader%2A>. <xref:System.Data.EntityClient.EntityDataReader> implémente <xref:System.Data.IExtendedDataRecord> pour décrire des résultats structurés et enrichis.  
  
## <a name="managing-transactions"></a>Gestion des transactions  
 Dans Entity Framework, il existe deux modes d'utilisation des transactions : automatique et explicite. Les transactions automatiques utilisent l'espace de noms <xref:System.Transactions>, tandis que les transactions explicites utilisent la classe <xref:System.Data.EntityClient.EntityTransaction>.  
  
 Pour mettre à jour des données qui sont exposées via un modèle conceptuel ; consultez [Comment : gérer des Transactions dans Entity Framework](https://msdn.microsoft.com/library/4a55eb7f-f826-4a48-9df1-aebe2352ebef).  
  
## <a name="in-this-section"></a>Dans cette section  
 [Guide pratique pour créer une chaîne de connexion EntityConnection](../../../../../docs/framework/data/adonet/ef/how-to-build-an-entityconnection-connection-string.md)  
  
 [Guide pratique pour exécuter une requête qui retourne les résultats PrimitiveType](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-primitivetype-results.md)  
  
 [Guide pratique pour exécuter une requête qui retourne les résultats StructuralType](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)  
  
 [Guide pratique pour exécuter une requête qui retourne les résultats RefType](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-reftype-results.md)  
  
 [Guide pratique pour exécuter une requête qui retourne les types complexes](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-complex-types.md)  
  
 [Guide pratique pour exécuter une requête qui retourne les collections imbriquées](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-nested-collections.md)  
  
 [Guide pratique pour exécuter une requête paramétrée Entity SQL avec EntityCommand](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-parameterized-entity-sql-query-using-entitycommand.md)  
  
 [Guide pratique pour exécuter une procédure stockée paramétrée utilisant EntityCommand](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-parameterized-stored-procedure-using-entitycommand.md)  
  
 [Guide pratique pour exécuter une requête polymorphe](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-polymorphic-query.md)  
  
 [Guide pratique pour naviguer parmi les relations avec l’opérateur Navigate](../../../../../docs/framework/data/adonet/ef/how-to-navigate-relationships-with-the-navigate-operator.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Gestion des connexions et Transactions](https://msdn.microsoft.com/library/b6659d2a-9a45-4e98-acaa-d7a8029e5b99)  
 [ADO.NET Entity Framework](../../../../../docs/framework/data/adonet/ef/index.md)  
 [Informations de référence sur le langage](../../../../../docs/framework/data/adonet/ef/language-reference/index.md)
