---
title: Activités de transaction dans WF
ms.date: 03/30/2017
ms.assetid: fb33378e-82c6-4ea0-870f-76dc77e7f0fe
ms.openlocfilehash: f2709601fc4fd88a1c5223a5a3e97e139ceca954
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33516601"
---
# <a name="transaction-activities-in-wf"></a>Activités de transaction dans WF
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] a plusieurs activités fournies par le système pour modéliser les transactions, la compensation et l'annulation. Ces modèles de programmation permettent au workflow de poursuivre la progression vers l'avant dans le cas de modifications de logique métier et de gestion des erreurs. Pour plus d’informations sur les transactions, la compensation et l’annulation, consultez [Transactions](../../../docs/framework/windows-workflow-foundation/workflow-transactions.md), [Compensation](../../../docs/framework/windows-workflow-foundation/compensation.md), et [annulation](../../../docs/framework/windows-workflow-foundation/modeling-cancellation-behavior-in-workflows.md).  
  
## <a name="transaction-activities"></a>Activités de transaction  
  
|||  
|-|-|  
|<xref:System.Activities.Statements.CancellationScope>|Associe la logique d'annulation, sous la forme d'une activité, à un chemin d'accès principal d'exécution, également exprimé sous la forme d'une activité.|  
|<xref:System.Activities.Statements.CompensableActivity>|Prend en charge la compensation de ses activités enfants.|  
|<xref:System.Activities.Statements.Compensate>|Appelle explicitement le gestionnaire de compensation d'un <xref:System.Activities.Statements.CompensableActivity>.|  
|<xref:System.Activities.Statements.Confirm>|Appelle explicitement le gestionnaire de confirmation d'un <xref:System.Activities.Statements.CompensableActivity>.|  
|<xref:System.Activities.Statements.TransactionScope>|Délimite une limite de transaction.|  
|<xref:System.ServiceModel.Activities.TransactedReceiveScope>|Définit la durée de vie d'une transaction créée par un message reçu. La transaction peut être transmise dans le workflow sur le message de départ ou peut être créée par un répartiteur lorsque le message est reçu. **Remarque :** le <xref:System.ServiceModel.Activities.TransactedReceiveScope> se trouve dans le **messagerie** section de la **boîte à outils**.|
