---
title: Guide pratique pour vérifier l'état de la connexion en Visual Basic
ms.date: 07/20/2015
helpviewer_keywords:
- Web connections [Visual Basic]
- IsAvailable property [Visual Basic], about IsAvailable
- connections [Visual Basic], checking status
- connection status [Visual Basic]
ms.assetid: 4d9ee8ab-9a6f-4279-ace4-b75afc976a74
ms.openlocfilehash: 4a6cb67474d03ada5e0a73d94f65da7a381c44a8
ms.sourcegitcommit: 412bbc2e43c3b6ca25b358cdf394be97336f0c24
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/24/2018
ms.locfileid: "42911939"
---
# <a name="how-to-check-connection-status-in-visual-basic"></a>Guide pratique pour vérifier l'état de la connexion en Visual Basic
Vous pouvez utiliser la propriété <xref:Microsoft.VisualBasic.Devices.Network.IsAvailable> pour déterminer si l’ordinateur dispose d’une connexion Internet ou réseau active.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-check-whether-a-computer-has-a-working-connection"></a>Pour vérifier si un ordinateur dispose d’une connexion active  
  
-   Vérifiez si la propriété `IsAvailable` est `True` ou `False`. Le code suivant vérifie l’état de la propriété et le signale :  
  
     [!code-vb[VbResourceTasks#3](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-check-connection-status_1.vb)]  
  
     Cet exemple de code est également disponible sous la forme d’un extrait de code IntelliSense. Dans le sélecteur d’extraits de code, il se trouve sous **Connectivité et réseau**. Pour plus d’informations, consultez [Extraits de code](/visualstudio/ide/code-snippets).  
  
## <a name="see-also"></a>Voir aussi  
 <xref:Microsoft.VisualBasic.Devices.Network?displayProperty=nameWithType>  
 <xref:Microsoft.VisualBasic.Devices.Network.IsAvailable>
