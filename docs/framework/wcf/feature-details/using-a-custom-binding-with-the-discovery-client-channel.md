---
title: Utilisation d’une liaison personnalisée avec le canal client de découverte
ms.date: 03/30/2017
ms.assetid: 36f95e75-04f7-44f3-a995-a0d623624d7f
ms.openlocfilehash: 4ef85b4c52c1f27b333413e2b6178452142d313f
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33498356"
---
# <a name="using-a-custom-binding-with-the-discovery-client-channel"></a>Utilisation d’une liaison personnalisée avec le canal client de découverte
Lorsque vous utilisez une liaison personnalisée avec l'élément <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>, vous devez définir un objet <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider> qui crée des instances <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>.  
  
## <a name="creating-a-discoveryendpointprovider"></a>Création d'un DiscoveryEndpointProvider  
 Le <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider> est responsable de la création de <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> instances à la demande. Pour définir un fournisseur de points de terminaison de découverte, dérivez une classe à partir de <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider>, substituez la méthode <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider.GetDiscoveryEndpoint%2A> et retournez un nouveau point de terminaison de découverte. L'exemple suivant indique comment créer un fournisseur de points de terminaison de découverte.  
  
```  
// Extend DiscoveryEndpointProvider class to change the default DiscoveryEndpoint  
// to the DiscoveryClientBindingElement. The Discovery ClientChannel   
// uses this endpoint to send Probe message.  
public class UdpDiscoveryEndpointProvider : DiscoveryEndpointProvider  
{  
   public override DiscoveryEndpoint GetDiscoveryEndpoint()  
   {  
      return new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscoveryApril2005);  
   }  
}  
```  
  
 Une fois que vous avez défini le fournisseur de points de terminaison de découverte, vous pouvez créer une liaison personnalisée et ajouter l'objet <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>, qui référence le fournisseur de points de terminaison de découverte, comme indiqué dans l'exemple suivant.  
  
```  
DiscoveryClientBindingElement discoveryBindingElement = new DiscoveryClientBindingElement();  
  
// Provide the search criteria and the endpoint over which the probe is sent.  
discoveryBindingElement.FindCriteria = new FindCriteria(typeof(ICalculatorService));  
discoveryBindingElement.DiscoveryEndpointProvider = new UdpDiscoveryEndpointProvider();  
  
CustomBinding customBinding = new CustomBinding(new NetTcpBinding());  
// Insert DiscoveryClientBindingElement at the top of the BindingElement stack.  
// An exception is thrown if this binding element is not at the top.  
customBinding.Elements.Insert(0, discoveryBindingElement);  
```  
  
 Pour plus d’informations sur l’utilisation du canal client de découverte, consultez [à l’aide du canal Client de découverte](../../../../docs/framework/wcf/feature-details/using-the-discovery-client-channel.md). Pour obtenir un exemple de code complet, consultez [exemple Discovery Binding Element](../../../../docs/framework/wcf/samples/discovery-binding-element-sample.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Vue d’ensemble de la découverte WCF](../../../../docs/framework/wcf/feature-details/wcf-discovery-overview.md)  
 [Utilisation du canal client de découverte](../../../../docs/framework/wcf/feature-details/using-the-discovery-client-channel.md)  
 [Exemple d’élément de liaison de découverte](../../../../docs/framework/wcf/samples/discovery-binding-element-sample.md)
