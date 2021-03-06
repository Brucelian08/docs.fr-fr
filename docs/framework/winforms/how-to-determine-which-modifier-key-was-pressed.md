---
title: 'Comment : identifier la touche de modification activée'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- keyboard input
- shift keys
- events [Windows Forms], mouse
- Keys.ControlKey enumeration member
- keys [Windows Forms], control keys
- user input [Windows Forms], checking for keyboard
- keys [Windows Forms], determining last pressed
- keys [Windows Forms], shift keys
- keys [Windows Forms], modifier keys
- control keys
- keys [Windows Forms], alt keys
- alt keys
- Keys.Shift enumeration member
- events [Windows Forms], keyboard
- keyboards [Windows Forms], keyboard input
- Keys.Alt enumeration member
- modifier keys
ms.assetid: 1e184048-0ae3-4067-a200-d4ba31dbc2cb
ms.openlocfilehash: f73dea640bc2059353b2a250188b901f360ea750
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/08/2018
ms.locfileid: "44202035"
---
# <a name="how-to-determine-which-modifier-key-was-pressed"></a>Comment : identifier la touche de modification activée
Lorsque vous créez une application qui accepte des séquences de touches de l’utilisateur, vous souhaiterez également analyser les touches de modification telles que les touches MAJ, ALT et CTRL. Lorsqu’une touche de modification est enfoncée en combinaison avec d’autres clés, ou avec les clics de souris, votre application peut réagir de façon appropriée. Par exemple, si l’utilisateur appuie sur la lettre S, cela peut entraîner tout simplement d’un « s » à l’écran, mais si les touches CTRL + S sont utilisées, le document actuel peut être enregistré. Si vous gérez le <xref:System.Windows.Forms.Control.KeyDown> événement, le <xref:System.Windows.Forms.KeyEventArgs.Modifiers%2A> propriété de la <xref:System.Windows.Forms.KeyEventArgs> reçu par l’événement gestionnaire spécifie les touches de modification sont enfoncées. Vous pouvez également le <xref:System.Windows.Forms.KeyEventArgs.KeyData%2A> propriété du <xref:System.Windows.Forms.KeyEventArgs> Spécifie le caractère qui a été enfoncé, ainsi que les touches de modification combinées avec une opération OR au niveau du bit. Toutefois, si vous gérez le <xref:System.Windows.Forms.Control.KeyPress> événement ou un événement de souris, le Gestionnaire d’événements ne reçoit pas ces informations. Dans ce cas, vous devez utiliser le <xref:System.Windows.Forms.Control.ModifierKeys%2A> propriété de la <xref:System.Windows.Forms.Control> classe. Dans les deux cas, vous devez effectuer une opération AND au niveau du bit d’approprié <xref:System.Windows.Forms.Keys> valeur et la valeur que vous testez. Le <xref:System.Windows.Forms.Keys> énumération offre des variations de chaque touche de modification, il est donc important d’effectuer l’opération de bits et avec la valeur correcte. Par exemple, la touche MAJ est représenté par <xref:System.Windows.Forms.Keys.Shift>, <xref:System.Windows.Forms.Keys.ShiftKey>, <xref:System.Windows.Forms.Keys.RShiftKey> et <xref:System.Windows.Forms.Keys.LShiftKey> la valeur correcte pour tester, MAJ comme une touche de modification est <xref:System.Windows.Forms.Keys.Shift>. De même, pour tester CTLR et ALT en tant que modificateurs vous devez utiliser le <xref:System.Windows.Forms.Keys.Control> et <xref:System.Windows.Forms.Keys.Alt> des valeurs, respectivement.  
  
> [!NOTE]
>  Les programmeurs Visual Basic peuvent également accéder à des informations de clé par le biais du <xref:Microsoft.VisualBasic.Devices.Computer.Keyboard%2A> propriété  
  
### <a name="to-determine-which-modifier-key-was-pressed"></a>Pour déterminer la touche a été activée.  
  
-   Utilisez l’opérateur de bits `AND` opérateur avec la <xref:System.Windows.Forms.Control.ModifierKeys%2A> propriété et une valeur de la <xref:System.Windows.Forms.Keys> énumération pour déterminer si une touche de modification particulière est enfoncée. L’exemple de code suivant montre comment déterminer si la touche MAJ est activée dans un <xref:System.Windows.Forms.Control.KeyPress> Gestionnaire d’événements.  
  
     [!code-cpp[System.Windows.Forms.DetermineModifierKey#5](../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/cpp/form1.cpp#5)]
     [!code-csharp[System.Windows.Forms.DetermineModifierKey#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/CS/form1.cs#5)]
     [!code-vb[System.Windows.Forms.DetermineModifierKey#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/VB/form1.vb#5)]  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Windows.Forms.Keys>  
 <xref:System.Windows.Forms.Control.ModifierKeys%2A>  
 [Entrée au clavier dans une application Windows Forms](../../../docs/framework/winforms/keyboard-input-in-a-windows-forms-application.md)  
 [Comment : déterminer si la touche VERR. MAJ. est activée dans Visual Basic](https://msdn.microsoft.com/library/91e60f5c-dd61-4222-ba5f-39af803afd8c)
