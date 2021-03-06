---
title: Vue d'ensemble de l'utilisation de la disposition automatique
ms.date: 03/30/2017
helpviewer_keywords:
- layout [WPF], automatic
- automatic layout [WPF]
ms.assetid: 6fed9264-18bb-4d05-8867-1fe356c6f687
ms.openlocfilehash: a43b3c0e008025171e3b1fdeba3bc514d01e28c8
ms.sourcegitcommit: 3c1c3ba79895335ff3737934e39372555ca7d6d0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43856035"
---
# <a name="use-automatic-layout-overview"></a>Vue d'ensemble de l'utilisation de la disposition automatique
Cette rubrique présente des instructions pour les développeurs sur la façon d’écrire [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] applications localisables [!INCLUDE[TLA#tla_ui#plural](../../../../includes/tlasharptla-uisharpplural-md.md)]. Dans le passé, la localisation d’un [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] a été beaucoup de temps. Chaque langage qui le [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] était adaptée nécessitait un réglage pixel par pixel. Aujourd'hui, grâce à la conception et des normes de codage, de droite [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] peut être construite afin que les traducteurs aient moins de redimensionnement et de repositionnement. L’approche à écrire des applications qui peuvent être plus facilement redimensionnées et repositionnées est appelée à la disposition automatique et peut être obtenue en utilisant [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] design de l’application.  
  
<a name="advantages_of_autolayout"></a>   
## <a name="advantages-of-using-automatic-layout"></a>Avantages de l’utilisation de la disposition automatique  
 Étant donné que le [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] système de présentation est puissant et flexible, il fournit la possibilité de disposer des éléments dans une application qui peuvent être ajustés pour répondre aux exigences des différentes langues. La liste suivante souligne quelques-uns des avantages de la disposition automatique.  
  
-   L’[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] s’affiche correctement dans n’importe quelle langue.  
  
-   Réduit le besoin de réajuster la position et la taille des contrôles une fois le texte traduit.  
  
-   Réduit le besoin de réajuster la taille de la fenêtre.  
  
-   La disposition de l’[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] s’affiche correctement dans n’importe quelle langue.  
  
-   La localisation peut se trouver réduite à sa plus simple expression, à savoir la traduction d’une chaîne.  
  
<a name="autolayout_controls"></a>   
## <a name="automatic-layout-and-controls"></a>Disposition automatique et contrôles  
 La disposition automatique permet à une application d’ajuster automatiquement la taille d’un contrôle. Par exemple, un contrôle peut changer pour accommoder la longueur d’une chaîne. Cette fonctionnalité permet aux responsables de la localisation de traduire la chaîne sans devoir redimensionner le contrôle pour que le texte traduit s’ajuste. L’exemple suivant crée un bouton avec un contenu en anglais.  
  
 [!code-xaml[LocalizationBtn_snip#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn_snip/CS/Pane1.xaml#1)]  
  
 Dans l’exemple, il vous suffit de changer le texte pour que le bouton soit en espagnol. Par exemple :  
  
 [!code-xaml[LocalizationBtn#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn/CS/Pane1.xaml#1)]  
  
 Le graphique suivant illustre la sortie des exemples de code.  
  
 ![Même bouton avec le texte dans différentes langues](../../../../docs/framework/wpf/advanced/media/globalizationbutton.png "GlobalizationButton")  
Bouton redimensionnable automatiquement  
  
<a name="autolayout_coding"></a>   
## <a name="automatic-layout-and-coding-standards"></a>Disposition automatique et normes de codage  
 À l’aide de l’approche de la disposition automatique nécessite un ensemble de normes de codage et de conception et de règles pour produire entièrement localisable [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]. Les indications suivantes vont simplifier le codage de votre disposition automatique.  
  
| Normes de codage | Description |
| ---------------------- | ----------------- |
| Ne pas utiliser de positions absolues | <ul><li>N’utilisez pas <xref:System.Windows.Controls.Canvas> , car il positionne les éléments absolument.</li><li>Utilisez <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.StackPanel>, et <xref:System.Windows.Controls.Grid> pour positionner les contrôles.</li><li>Pour une discussion sur divers types de panneaux, consultez [vue d’ensemble de panneaux](../../../../docs/framework/wpf/controls/panels-overview.md).</li></ul> |
| Ne pas définir de fenêtre à taille fixe | -Utilisez <xref:System.Windows.Window.SizeToContent%2A>.<br />Exemple :<br /><br /> [!code-xaml[LocalizationGrid#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#2)] |
| Ajoutez un <xref:System.Windows.FrameworkElement.FlowDirection%2A> | <ul><li>Ajouter un <xref:System.Windows.FrameworkElement.FlowDirection%2A> à l’élément racine de votre application.</li><li>WPF fournit un moyen pratique pour prendre en charge horizontales, bidirectionnelles et des dispositions verticales. Dans l’infrastructure de présentation, le <xref:System.Windows.FrameworkElement.FlowDirection%2A> propriété peut être utilisée pour définir la disposition. Les modèles de sens du déroulement sont les suivants :<br /><br /> <ul><li><xref:System.Windows.FlowDirection.LeftToRight> (LrTb) : disposition horizontale pour le Latin, Asie de l’est et ainsi de suite.</li><li><xref:System.Windows.FlowDirection.RightToLeft> (RlTb) — bidirectionnelle pour l’arabe, hébreu et ainsi de suite.</li></ul></li></ul> |
| Utiliser des polices composites au lieu des polices physiques | <ul><li>Avec les polices composites, le <xref:System.Windows.Controls.Control.FontFamily%2A> propriété ne doit pas être localisé.</li><li>Les développeurs peuvent utiliser l’une des polices suivantes ou créer la leur.<br /><br /> <ul><li>Interface utilisateur globale</li><li>Sans Serif global</li><li>Serif global</li></ul></li></ul> |
| Ajouter xml:lang | <ul><li>Ajouter le `xml:lang` attribut dans l’élément racine de votre [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], tel que `xml:lang="en-US"` pour une application en anglais.</li><li>Étant donné que les polices composites utilisent `xml:lang` pour déterminer la police à utiliser, définissez cette propriété pour prendre en charge les scénarios multilingues.</li></ul> |
  
<a name="autolay_grids"></a>   
## <a name="automatic-layout-and-grids"></a>Disposition automatique et grilles  
 Le <xref:System.Windows.Controls.Grid> élément, est utile pour la disposition automatique car il permet à un développeur positionner des éléments. Un <xref:System.Windows.Controls.Grid> contrôle est capable de répartir l’espace disponible entre ses éléments enfants, à l’aide d’une disposition de ligne et de colonne. Le [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] éléments peuvent s’étendre sur plusieurs cellules, et il est possible d’avoir des grilles imbriquées. Grilles sont utiles car ils permettent de créer et de positionner complexe [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]. L’exemple suivant illustre l’utilisation d’une grille pour positionner des boutons et du texte. Notez que la hauteur et la largeur des cellules sont définies sur <xref:System.Windows.GridUnitType.Auto>; par conséquent, la cellule qui contient le bouton avec une image s’ajuste à l’image.  
  
 [!code-xaml[LocalizationGrid#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#1)]  
  
 Le graphique suivant montre la grille produite par le code précédent.  
  
 ![Exemple de grille](../../../../docs/framework/wpf/advanced/media/glob-grid.png "glob_grid")  
Grille  
  
<a name="autolay_grids_issharedsizescope"></a>   
## <a name="automatic-layout-and-grids-using-the-issharedsizescope-property"></a>Disposition automatique et grilles avec la propriété IsSharedSizeScope  
 Un <xref:System.Windows.Controls.Grid> élément est utile dans des applications localisables pour créer des contrôles qui s’ajustent en fonction du contenu. Cependant, il peut parfois être nécessaire que les contrôles conservent une taille particulière quel que soit le contenu. Par exemple, pour les boutons « OK », « Annuler » et « Parcourir », vous n’avez probablement pas besoin que les boutons s’adaptent à la taille du contenu. Dans ce cas le <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A?displayProperty=nameWithType> propriété jointe est utile pour partager le même dimensionnement entre plusieurs éléments de grille. L’exemple suivant montre comment partager des données entre plusieurs de dimensionnement de ligne et de colonne <xref:System.Windows.Controls.Grid> éléments.  
  
 [!code-xaml[gridIssharedsizescopeProp#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#2)]  
  
 **Remarque** pour l’exemple de code complet, consultez [partage de propriétés de dimensionnement entre grilles](../../../../docs/framework/wpf/controls/how-to-share-sizing-properties-between-grids.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Globalisation pour WPF](../../../../docs/framework/wpf/advanced/globalization-for-wpf.md)  
 [Utiliser la disposition automatique pour créer un bouton](../../../../docs/framework/wpf/advanced/how-to-use-automatic-layout-to-create-a-button.md)  
 [Utiliser une grille pour la disposition automatique](../../../../docs/framework/wpf/advanced/how-to-use-a-grid-for-automatic-layout.md)
