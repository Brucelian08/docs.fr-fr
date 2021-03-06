---
title: Exemple Discovery Proxy
ms.date: 03/30/2017
ms.assetid: 1dfa02df-15b1-4e97-9c8e-f5f2772711b0
ms.openlocfilehash: 6fc0680bc6b61a6fe1b4b141c8b1e5081df5a124
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/08/2018
ms.locfileid: "44180395"
---
# <a name="discovery-proxy-sample"></a>Exemple Discovery Proxy
Cet exemple montre comment créer une implémentation d'un proxy de découverte pour stocker des informations sur des services existants et comment des clients peuvent interroger ce proxy afin d'obtenir les informations. Cet exemple est composé de trois projets :  
  
-   **Service**: un simple service de calculatrice de Windows Communication Foundation (WCF) qui s’enregistre avec le proxy de découverte.  
  
-   **Proxy de découverte**: l’implémentation d’un service de proxy de découverte.  
  
-   **Client**: application cliente WCF qui appelle le proxy de découverte pour rechercher des services.  
  
## <a name="demonstrates"></a>Démonstrations  
 Implémentation du proxy de découverte  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur. Recherchez le répertoire (par défaut) suivant avant de continuer.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n’existe pas, accédez à [Windows Communication Foundation (WCF) et des exemples de Windows Workflow Foundation (WF) pour .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) pour télécharger tous les Windows Communication Foundation (WCF) et [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemples. Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Discovery\DiscoveryProxy`  
  
## <a name="discoveryproxy"></a>DiscoveryProxy  
 Dans la méthode `Main` du fichier Program.cs, l'exemple montre comment un service de type <xref:System.ServiceModel.Discovery.DiscoveryProxy> est hébergé. Il expose deux points de terminaison ; l'un de type <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>, l'autre de type <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>. Les points de terminaison utilisent tous deux un transport TCP. L'<xref:System.ServiceModel.Discovery.DiscoveryEndpoint> écoute au niveau de l'URI spécifié par le paramètre `probeEndpointAddress`, là où les clients peuvent envoyer des messages Probe pour interroger le proxy afin d'obtenir ses données. Le <xref:System.ServiceModel.Discovery.AnnouncementEndpoint> écoute au niveau de l'URI spécifié par le paramètre `announcementEndpointAddress`, là où le proxy écoute les annonces. Lorsqu'une annonce en ligne est reçue, le proxy ajoute le service à son cache et lorsqu'une annonce hors connexion est reçue, il supprime le service de son cache.  
  
 Le fichier DiscoveryProxy.cs contient l'implémentation du <xref:System.ServiceModel.Discovery.DiscoveryProxy>. Le proxy doit hériter de la classe <xref:System.Object> et requiert une implémentation d'<xref:System.Runtime.Remoting.Messaging.AsyncResult>. À l'instanciation, le proxy crée un <xref:System.Collections.Generic.Dictionary%602>, qu'il utilise pour stocker les éléments qui lui sont connus.  
  
 Le fichier est divisé en deux régions, l'une pour les méthodes du cache du proxy, l'autre pour l'implémentation de Discovery Proxy. La région des méthodes du cache du proxy contient des méthodes utilisées pour mettre à jour le <xref:System.Collections.Generic.Dictionary%602>, exécuter des requêtes sur le <xref:System.Collections.Generic.Dictionary%602> et imprimer les données pour les utilisateurs. La région de l'implémentation de Discovery Proxy contient les méthodes substituées requises pour les fonctionnalités d'annonce et de sonde. Elles définissent les actions effectuées par un proxy après réception d'une annonce en ligne, d'une annonce hors connexion ou d'un message Probe.  
  
## <a name="service"></a>Service  
 Dans le fichier Program.cs du projet Service, le même URI est utilisé pour le point de terminaison d'annonce et le proxy de découverte. En effet, le service utilise le point de terminaison pour l'envoi des annonces, alors que le proxy l'utilise pour leur réception. Le service utilise le <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> et lui ajoute un point de terminaison d'annonce.  
  
## <a name="client"></a>Client  
 Le projet Client utilise le même URI pour son point de terminaison de sonde et le proxy. En effet, les sondes de ce scénario font également l'objet d'une monodiffusion spécifiquement vers le point de terminaison disponible sur le proxy. Le client se connecte à cette adresse bien connue, puis l'interroge au sujet du service. Une fois qu'il a trouvé le service, il s'y connecte.  
  
#### <a name="to-use-this-sample"></a>Pour utiliser cet exemple  
  
1.  Chargez la solution du projet dans [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] et générez le projet.  
  
2.  En premier lieu, exécutez l'application Discovery Proxy, générée dans [répertoire de base de la solution]\DiscoveryProxy\bin\debug. Discovery Proxy doit s'exécuter en premier, car les points de terminaison d'annonce TCP doivent être en place pour permettre au service d'envoyer ses annonces.  
  
3.  En second lieu, exécutez l'application Service, générée dans [répertoire de base de la solution]\Service\bin\debug. Au démarrage, le service envoie une annonce au point de terminaison d'annonce du proxy de découverte et est inscrit dans le cache du proxy.  
  
4.  Ensuite, exécutez l'application Client, générée dans [répertoire de base de la solution]\Client\bin\debug. Le client interroge le proxy, obtient l'adresse du service, puis s'y connecte.  
  
5.  Enfin, arrêtez le client, le service, puis le proxy. Pour recevoir l'annonce hors connexion du service, le proxy doit être en cours d'exécution.  
  
## <a name="see-also"></a>Voir aussi
