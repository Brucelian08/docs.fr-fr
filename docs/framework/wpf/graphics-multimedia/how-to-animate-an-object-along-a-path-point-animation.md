---
title: 'Comment : animer un objet sur un tracé (animation de point)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], objects along paths (point animation)
- point animation [WPF]
ms.assetid: 1fa3f817-35bc-41a1-b366-f5a20b70da0c
ms.openlocfilehash: d6dc79cd7a15aef2a4168fffb293c5e1f33cde08
ms.sourcegitcommit: 4b6490b2529707627ad77c3a43fbe64120397175
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44259780"
---
# <a name="how-to-animate-an-object-along-a-path-point-animation"></a>Comment : animer un objet sur un tracé (animation de point)
Cet exemple montre comment utiliser un <xref:System.Windows.Media.Animation.PointAnimationUsingPath> objet à animer un <xref:System.Windows.Point> sur un tracé courbé.  
  
## <a name="example"></a>Exemple  
 L’exemple suivant déplace un <xref:System.Windows.Media.EllipseGeometry> sur un tracé défini par un <xref:System.Windows.Media.PathGeometry>. La géométrie d’ellipse <xref:System.Windows.Media.EllipseGeometry.Center%2A> propriété, qui prend un <xref:System.Windows.Point> valeur, spécifie sa position ; pour déplacer la géométrie d’ellipse, vous animer sa <xref:System.Windows.Media.EllipseGeometry.Center%2A> propriété. L’exemple utilise un <xref:System.Windows.Media.Animation.PointAnimationUsingPath> pour animer la <xref:System.Windows.Media.EllipseGeometry> l’objet <xref:System.Windows.Media.EllipseGeometry.Center%2A> propriété.  
  
 [!code-xaml[PathAnimationGallery_snippet#PointAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/pointanimationusingpathexample.xaml#pointanimationusingpathwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#PointAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/PointAnimationUsingPathExample.cs#pointanimationusingpathwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#PointAnimationUsingPathWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/PointAnimationUsingPathExample.vb#pointanimationusingpathwholepage)]  
  
 Pour obtenir un exemple complet, consultez [Animation de tracés, exemple](https://go.microsoft.com/fwlink/?LinkID=160028).  
  
 La version du code de l’exemple précédent utilisé un <xref:System.Windows.Media.Animation.Storyboard> pour animer la <xref:System.Windows.Media.EllipseGeometry>, bien qu’une seule animation ait été appliquée. Un <xref:System.Windows.Media.Animation.Storyboard> est souvent le moyen le plus simple d’appliquer plusieurs animations, car ces animations peuvent être contrôlées par le même <xref:System.Windows.Media.Animation.Storyboard>. Toutefois, un moyen plus simple pour appliquer une seule animation à une propriété lors de l’utilisation de code consiste à utiliser le <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> (méthode). Si vous voulez voir un exemple, consultez l’article [Comment : animer une propriété sans utiliser de storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Animation de tracés, exemple](https://go.microsoft.com/fwlink/?LinkID=160028)  
 [Vue d’ensemble de l’animation](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)  
 [Guides pratiques relatifs aux animations de tracés](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)
