---
title: Exemple d'activité compensable
ms.date: 03/30/2017
ms.assetid: 58f4898c-b2b8-44a4-9a73-3bef4da6d5ba
ms.openlocfilehash: 3bf1d120cd700830a98f53495f7e9989ffec73db
ms.sourcegitcommit: 6eac9a01ff5d70c6d18460324c016a3612c5e268
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2018
ms.locfileid: "45678254"
---
# <a name="compensable-activity-sample"></a>Exemple d'activité compensable
Cet exemple montre comment utiliser l'activité `CompensableActivity` pour définir le travail à faire pour une action donnée pendant une exécution normale et le travail qui doit être fait pour compenser cette action, si nécessaire ultérieurement.  La première partie de l’exemple montre comment les unités de travail compensable peuvent être définies dans Windows Workflow Foundation (WF) à l’aide un `CompensableActivity` activité et comment elles sont exécutées dans une exécution réussie.  La deuxième partie de l'exemple montre comment ces mêmes unités de travail compensable se chargent automatiquement de la compensation lorsqu'un événement inattendu est atteint et que l'instance de workflow est annulée.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Pour configurer, générer et exécuter l'exemple  
  
1.  À l'aide de Visual Studio 2010, ouvrez CompensableActivity.sln.  
  
2.  Générez la solution en appuyant sur Ctrl+Maj+B.  
  
3.  Exécutez l'application en appuyant sur F5.  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur. Recherchez le répertoire (par défaut) suivant avant de continuer.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n’existe pas, accédez à [Windows Communication Foundation (WCF) et des exemples de Windows Workflow Foundation (WF) pour .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) pour télécharger tous les Windows Communication Foundation (WCF) et [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemples. Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Compensation\BasicCompensableActivity`