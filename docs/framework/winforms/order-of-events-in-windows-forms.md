---
title: Ordre des événements dans les Windows Forms
ms.date: 03/30/2017
helpviewer_keywords:
- events [Windows Forms], order of
- focus event order
- application shutdown event order
- sequence [Windows Forms], of events
- validation events [Windows Forms], order of
- application startup event order
ms.assetid: e81db09b-4453-437f-b78a-62d7cd5c9829
ms.openlocfilehash: 10a6451827a16605ba738cf74b7f684b69adb5dc
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33538468"
---
# <a name="order-of-events-in-windows-forms"></a>Ordre des événements dans les Windows Forms
L’ordre dans lequel les événements sont déclenchés dans les applications Windows Forms est particulièrement intéressant pour les développeurs soucieux de gérer chacun de ces événements tour à tour. Quand une situation nécessite une gestion méticuleuse des événements, par exemple quand vous redessinez certaines parties du formulaire, une connaissance de l'ordre exact dans lequel les événements sont déclenchés au moment de l'exécution est nécessaire. Cette rubrique fournit des détails sur l'ordre des événements durant plusieurs phases importantes de la durée de vie des applications et des contrôles. Pour plus d’informations spécifiques sur l’ordre des événements d’entrée de souris, consultez [les événements de souris dans les Windows Forms](../../../docs/framework/winforms/mouse-events-in-windows-forms.md). Pour une vue d’ensemble des événements dans les Windows Forms, consultez [vue d’ensemble des événements](../../../docs/framework/winforms/events-overview-windows-forms.md). Pour plus d’informations sur la création de gestionnaires d’événements, consultez [vue d’ensemble des gestionnaires d’événements](../../../docs/framework/winforms/event-handlers-overview-windows-forms.md).  
  
## <a name="application-startup-and-shutdown-events"></a>Événements de démarrage et d'arrêt des applications  
 Les classes <xref:System.Windows.Forms.Form> et <xref:System.Windows.Forms.Control> exposent un ensemble d'événements liés au démarrage et à l'arrêt de l'application. Lors du démarrage d’une application Windows Forms, les événements de démarrage du formulaire principal sont déclenchés dans l’ordre suivant :  
  
-   <xref:System.Windows.Forms.Control.HandleCreated?displayProperty=nameWithType>  
  
-   <xref:System.Windows.Forms.Control.BindingContextChanged?displayProperty=nameWithType>  
  
-   <xref:System.Windows.Forms.Form.Load?displayProperty=nameWithType>  
  
-   <xref:System.Windows.Forms.Control.VisibleChanged?displayProperty=nameWithType>  
  
-   <xref:System.Windows.Forms.Form.Activated?displayProperty=nameWithType>  
  
-   <xref:System.Windows.Forms.Form.Shown?displayProperty=nameWithType>  
  
 Lors de la fermeture d'une application, les événements d'arrêt du formulaire principal sont déclenchés dans l'ordre suivant :  
  
-   <xref:System.Windows.Forms.Form.Closing?displayProperty=nameWithType>  
  
-   <xref:System.Windows.Forms.Form.FormClosing?displayProperty=nameWithType>  
  
-   <xref:System.Windows.Forms.Form.Closed?displayProperty=nameWithType>  
  
-   <xref:System.Windows.Forms.Form.FormClosed?displayProperty=nameWithType>  
  
-   <xref:System.Windows.Forms.Form.Deactivate?displayProperty=nameWithType>  
  
 L'événement <xref:System.Windows.Forms.Application.ApplicationExit> de la classe <xref:System.Windows.Forms.Application> est déclenché après les événements d'arrêt du formulaire principal.  
  
> [!NOTE]
>  Visual Basic 2005 fournit des événements d'application supplémentaires, tels que <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup?displayProperty=nameWithType> et <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown?displayProperty=nameWithType>.  
  
## <a name="focus-and-validation-events"></a>Événements de focus et de validation  
 Quand vous modifiez le focus à l'aide du clavier (Tab, Maj+Tab, etc.) en appelant la méthode <xref:System.Windows.Forms.Control.Select%2A> ou <xref:System.Windows.Forms.Control.SelectNextControl%2A> ou en affectant le formulaire actuel comme valeur de la propriété <xref:System.Windows.Forms.ContainerControl.ActiveControl%2A>, les événements de focus de la classe <xref:System.Windows.Forms.Control> se produisent dans l'ordre suivant :  
  
-   <xref:System.Windows.Forms.Control.Enter>  
  
-   <xref:System.Windows.Forms.Control.GotFocus>  
  
-   <xref:System.Windows.Forms.Control.Leave>  
  
-   <xref:System.Windows.Forms.Control.Validating>  
  
-   <xref:System.Windows.Forms.Control.Validated>  
  
-   <xref:System.Windows.Forms.Control.LostFocus>  
  
 Quand vous modifiez le focus à l'aide de la souris ou en appelant la méthode <xref:System.Windows.Forms.Control.Focus%2A>, les événements de focus de la classe <xref:System.Windows.Forms.Control> se produisent dans l'ordre suivant :  
  
-   <xref:System.Windows.Forms.Control.Enter>  
  
-   <xref:System.Windows.Forms.Control.GotFocus>  
  
-   <xref:System.Windows.Forms.Control.LostFocus>  
  
-   <xref:System.Windows.Forms.Control.Leave>  
  
-   <xref:System.Windows.Forms.Control.Validating>  
  
-   <xref:System.Windows.Forms.Control.Validated>  
  
## <a name="see-also"></a>Voir aussi  
 [Création de gestionnaires d’événements dans les Windows Forms](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)
