---
title: "Comment : animer la position et la direction d'une caméra dans une scène 3D"
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], camera position in 3-D scenes
- camera direction [WPF], animating in 3-D scenes
- 3-D scenes [WPF], animating camera position
- 3-D scenes [WPF], animating camera direction
- camera position [WPF], animating in 3-D scenes
- animation [WPF], camera direction in 3-D scenes
ms.assetid: 480224b7-a5e5-4165-ba7f-ef760ddff94a
ms.openlocfilehash: 429139da809a78474f4f6a082fb6e3c08c72d431
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33558876"
---
# <a name="how-to-animate-camera-position-and-direction-in-a-3d-scene"></a>Comment : animer la position et la direction d'une caméra dans une scène 3D
L’exemple suivant montre comment animer la position d’une caméra et animer la direction qu’il pointe dans une scène 3D. Il incombe à l’aide de <xref:System.Windows.Media.Animation.Point3DAnimation> et <xref:System.Windows.Media.Animation.Vector3DAnimation> pour animer la <xref:System.Windows.Media.Media3D.ProjectionCamera.Position%2A> et <xref:System.Windows.Media.Media3D.ProjectionCamera.LookDirection%2A> propriétés respectivement de la <xref:System.Windows.Media.Media3D.PerspectiveCamera>. Vous pouvez utiliser une animation comme suit pour modifier la vue du spectateur d’une scène en réponse à un événement.  
  
## <a name="example"></a>Exemple  
 [!code-xaml[Animation3DGallery_snip#PointVector3DAnimationExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/PointVector3DAnimationExample.xaml#pointvector3danimationexamplewholepage)]  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Windows.Media.Animation.Vector3DAnimation>  
 <xref:System.Windows.Media.Animation.Point3DAnimation>  
 [Animer la position et la direction de la caméra à l’aide d’images clés](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-camera-position-and-direction-using-key-frames.md)  
 [Vue d’ensemble des graphiques 3D](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)
