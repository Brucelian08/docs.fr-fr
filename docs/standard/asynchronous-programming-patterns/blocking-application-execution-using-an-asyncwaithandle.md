---
title: Blocage de l'exécution d'applications à l'aide d'un AsyncWaitHandle
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- blocks, asynchronous operations
- ending asynchronous operations
- asynchronous programming, ending operations
- asynchronous programming, blocking applications
- stopping asynchronous operations
- blocking application execution
ms.assetid: 3e32daf2-8161-4e8f-addd-9fd9ff101b03
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 054af36987d60c8aeb752c9c711f1cce19733efc
ms.sourcegitcommit: 6eac9a01ff5d70c6d18460324c016a3612c5e268
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2018
ms.locfileid: "45624468"
---
# <a name="blocking-application-execution-using-an-asyncwaithandle"></a>Blocage de l'exécution d'applications à l'aide d'un AsyncWaitHandle
Les applications qui ne peuvent pas continuer à effectuer d’autres tâches en attendant les résultats d’une opération asynchrone doivent se bloquer jusqu'à ce que cette opération se termine. Pour bloquer le thread principal de votre application en attendant la fin d’une opération asynchrone, utilisez l’une des options suivantes :  
  
-   Utilisez la propriété <xref:System.IAsyncResult.AsyncWaitHandle%2A> du <xref:System.IAsyncResult> retourné par la méthode **Begin***NomOpération* de l’opération asynchrone. Cette approche est illustrée dans cette rubrique.  
  
-   Appelez la méthode **End***NomOpération* de l’opération asynchrone. Vous trouverez un exemple illustrant cette approche sur la page [Bloquer l'exécution d'applications en mettant fin à une opération asynchrone](../../../docs/standard/asynchronous-programming-patterns/blocking-application-execution-by-ending-an-async-operation.md).  
  
 Les applications qui utilisent un ou plusieurs objets <xref:System.Threading.WaitHandle> pour se bloquer jusqu'à la fin d’une opération asynchrone appellent généralement la méthode **Begin***NomOpération*, effectuent tout le travail réalisable sans les résultats de l’opération, puis se bloquent jusqu'à la fin de la ou des opérations asynchrones. Une application peut se bloquer sur une seule opération en appelant l’une des méthodes <xref:System.Threading.WaitHandle.WaitOne%2A> à l’aide du <xref:System.IAsyncResult.AsyncWaitHandle%2A>. Pour imposer un blocage en attendant qu’un ensemble d’opérations asynchrones se termine, stockez les objets <xref:System.IAsyncResult.AsyncWaitHandle%2A> associés dans un tableau et appelez l’une des méthodes <xref:System.Threading.WaitHandle.WaitAll%2A>. Pour imposer un blocage en attendant que l’une des opérations asynchrones se termine, stockez les objets <xref:System.IAsyncResult.AsyncWaitHandle%2A> associés dans un tableau et appelez l’une des méthodes <xref:System.Threading.WaitHandle.WaitAny%2A>.  
  
## <a name="example"></a>Exemple  
 L’exemple de code suivant montre comment utiliser des méthodes asynchrones dans la classe DNS afin de récupérer les informations DNS (Domain Name System) pour un ordinateur spécifié par l’utilisateur. Il illustre le blocage avec la <xref:System.Threading.WaitHandle> associée à l’opération asynchrone. Notez que `null` (`Nothing` en Visual Basic) est transmis aux paramètres <xref:System.Net.Dns.BeginGetHostByName%2A>`requestCallback` et `stateObject`, car ils ne sont pas requis dans cette approche.  
  
 [!code-csharp[AsyncDesignPattern#2](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/Async_EndBlockWait.cs#2)]
 [!code-vb[AsyncDesignPattern#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/Async_EndBlockWait.vb#2)]  
  
## <a name="see-also"></a>Voir aussi

- [Modèle asynchrone basé sur les événements (EAP)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)  
- [Vue d’ensemble du modèle asynchrone basé sur les événements](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)
