---
title: Fabrique de canaux
ms.date: 03/30/2017
ms.assetid: 09b53aa1-b13c-476c-a461-e82fcacd2a8b
ms.openlocfilehash: 6bf0668c6b846671db12dc20465ee70137d70b35
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43528870"
---
# <a name="channel-factory"></a>Fabrique de canaux
Cet exemple montre comment une application cliente peut créer un canal avec la classe <xref:System.ServiceModel.ChannelFactory> au lieu d'un client généré. Cet exemple est basé sur le [mise en route](../../../../docs/framework/wcf/samples/getting-started-sample.md) qui implémente un service de calculatrice.  
  
> [!NOTE]
>  La procédure d'installation ainsi que les instructions de génération relatives à cet exemple figurent à la fin de cette rubrique.  
  
 Cet exemple utilise la classe <xref:System.ServiceModel.ChannelFactory%601> pour créer un canal à un point de terminaison de service. En règle générale, pour créer un canal à un point de terminaison de service vous générer un client avec le [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) et créez une instance du type généré. Vous pouvez également créer un canal en utilisant la classe <xref:System.ServiceModel.ChannelFactory%601>, comme le montre cet exemple. Le service créé par l’exemple de code suivant est identique au service dans le [mise en route](../../../../docs/framework/wcf/samples/getting-started-sample.md).  
  
```csharp  
EndpointAddress address = new EndpointAddress("http://localhost/servicemodelsamples/service.svc");  
WSHttpBinding binding = new WSHttpBinding();  
ChannelFactory<ICalculator> factory = new   
                    ChannelFactory<ICalculator>(binding, address);  
ICalculator channel = factory.CreateChannel();  
```  
  
> [!IMPORTANT]
>  Si vous exécutez cet exemple dans un scénario à plusieurs ordinateurs, vous devez remplacer « localhost » dans le code précédent par le nom qualifié complet de l'ordinateur qui exécute le service. Cet exemple n'utilise pas de configuration pour définir l'adresse de point de terminaison, donc cela doit être fait dans le code.  
  
 Une fois le canal créé, les opérations de service peuvent être appelées comme pour un client généré.  
  
```csharp  
// Call the Add service operation.  
double value1 = 100.00D;  
double value2 = 15.99D;  
double result = channel.Add(value1, value2);  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
```  
  
 Pour fermer le canal, il faut d'abord le caster en une interface <xref:System.ServiceModel.IClientChannel>. Cela est dû au fait que le canal, tel que généré, est déclaré dans l'application cliente à l'aide de l'interface `ICalculator`, qui possède des méthodes comme `Add` et `Subtract` mais pas `Close`. La méthode `Close` provient de l'interface <xref:System.ServiceModel.ICommunicationObject>.  
  
```csharp  
// Close the channel.  
 ((IClientChannel)client).Close();  
```  
  
 Lorsque vous exécutez l'exemple, les demandes et réponses d'opération s'affichent dans la fenêtre de console du client. Appuyez sur ENTER dans la fenêtre de l'application pour fermer l'application cliente.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Pour configurer, générer et exécuter l'exemple  
  
1.  Vérifiez que vous avez effectué la [procédure d’installation unique pour les exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Pour générer l’édition C# ou Visual Basic .NET de la solution, conformez-vous aux instructions figurant dans [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md). Notez que cet exemple n'active pas la publication des métadonnées. Vous devez d'abord activer la publication des métadonnées pour cet exemple pour régénérer le type de client.  
  
3.  Pour exécuter l’exemple dans une configuration unique ou plusieurs ordinateurs, suivez les instructions de [en cours d’exécution les exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
### <a name="to-run-the-sample-cross-machine"></a>Pour exécuter l'exemple sur plusieurs ordinateurs  
  
1.  Remplacez « localhost » dans le code suivant par le nom qualifié complet de l'ordinateur qui exécute le service.  
  
    ```csharp  
    EndpointAddress address = new EndpointAddress("http://localhost/servicemodelsamples/service.svc");  
    ```  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur. Recherchez le répertoire (par défaut) suivant avant de continuer.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n’existe pas, accédez à [Windows Communication Foundation (WCF) et des exemples de Windows Workflow Foundation (WF) pour .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) pour télécharger tous les Windows Communication Foundation (WCF) et [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemples. Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Client\ChannelFactory`  
  
## <a name="see-also"></a>Voir aussi
