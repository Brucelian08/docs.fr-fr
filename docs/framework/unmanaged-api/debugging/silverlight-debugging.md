---
title: Débogage Silverlight
ms.date: 03/30/2017
helpviewer_keywords:
- debugging API [Silverlight]
- Silverlight, debugging
ms.assetid: 5e903e04-17d0-4014-ac9a-a43330ec8b1c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 80cee666a05432099a380a5ac547a5ca28698c31
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33436031"
---
# <a name="silverlight-debugging"></a>Débogage Silverlight
Les rubriques de cette section décrivent l'environnement et les interfaces fournis par le Common Language Runtime (CLR) pour prendre en charge le débogage des applications Silverlight qui s'exécutent sur le système d'exploitation Windows ou sur la plateforme Macintosh.  
  
## <a name="in-this-section"></a>Dans cette section  
 [EnumerateCLRs, fonction](../../../../docs/framework/unmanaged-api/debugging/enumerateclrs-function.md)  
 Fournit un mécanisme pour énumérer les CLR dans un processus.  
  
 [CloseCLREnumeration, fonction](../../../../docs/framework/unmanaged-api/debugging/closeclrenumeration-function.md)  
 Ferme tous les événements de continuer-démarrage CLR valides situés dans un tableau de handles retourné par le [fonction EnumerateCLRs](../../../../docs/framework/unmanaged-api/debugging/enumerateclrs-function.md)et libère la mémoire pour les tableaux de chemin d’accès de handles et de chaînes.  
  
 [CreateCoreClrDebugTarget, fonction](../../../../docs/framework/unmanaged-api/debugging/createcoreclrdebugtarget-function.md)  
 Crée une connexion à une cible distante pour l'énumération des processus et du runtime.  
  
 [CreateCordbObject, fonction](../../../../docs/framework/unmanaged-api/debugging/createcordbobject-function.md)  
 Crée une interface de débogueur qui fournit les fonctionnalités d'instanciation d'une session de débogage managée sur un processus distant.  
  
 [CreateVersionStringFromModule, fonction](../../../../docs/framework/unmanaged-api/debugging/createversionstringfrommodule-function.md)  
 Crée une chaîne de version à partir d’un chemin d’accès au CLR dans un processus cible.  
  
 [CreateDebuggingInterfaceFromVersion, fonction](../../../../docs/framework/unmanaged-api/debugging/createdebugginginterfacefromversion-function-for-silverlight.md)  
 Accepte une chaîne de version CLR retournée à partir de [fonction CreateVersionStringFromModule](../../../../docs/framework/unmanaged-api/debugging/createversionstringfrommodule-function.md), la fonction et retourne une interface de débogueur correspondante.  
  
 [CoreClrDebugProcInfo, structure](../../../../docs/framework/unmanaged-api/debugging/coreclrdebugprocinfo-structure.md)  
 Représente un processus qui s'exécute sur un ordinateur distant.  
  
 [CoreClrDebugRuntimeInfo, structure](../../../../docs/framework/unmanaged-api/debugging/coreclrdebugruntimeinfo-structure.md)  
 Représente une instance du CLR qui est chargée dans un processus sur un ordinateur distant.  
  
 [GetStartupNotificationEvent, fonction](../../../../docs/framework/unmanaged-api/debugging/getstartupnotificationevent-function.md)  
 Crée ou ouvre un gestionnaire d'événements qui sera signalé par un Common Language Runtime (CLR) qui est chargé dans le processus cible spécifié.  
  
 [ICoreClrDebugTarget, interface](../../../../docs/framework/unmanaged-api/debugging/icoreclrdebugtarget-interface.md)  
 Crée une connexion à une cible distante pour l'énumération des processus et du runtime.  
  
 [InitDbgTransportManager, fonction](../../../../docs/framework/unmanaged-api/debugging/initdbgtransportmanager-function.md)  
 Initialise le gestionnaire de transport pour se connecter à une cible distante pour l'énumération des processus et du runtime.  
  
 [ShutdownDbgTransportManager, fonction](../../../../docs/framework/unmanaged-api/debugging/shutdowndbgtransportmanager-function.md)  
 Arrête le gestionnaire de transport pour une connexion à un ordinateur cible distant.  
  
## <a name="see-also"></a>Voir aussi  
 [Coclasses de débogage](../../../../docs/framework/unmanaged-api/debugging/debugging-coclasses.md)  
 [Interfaces de débogage](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
 [Fonctions statiques globales de débogage](../../../../docs/framework/unmanaged-api/debugging/debugging-global-static-functions.md)  
 [Énumérations de débogage](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)  
 [Structures de débogage](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)
