---
title: CoInitializeEE, fonction
ms.date: 03/30/2017
api_name:
- CoInitializeEE
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- CoInitializeEE
helpviewer_keywords:
- CoInitializeEE function [.NET Framework hosting]
ms.assetid: 7e42a928-5068-4ba6-b8c3-806551a01fa8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8bbd25909e70826f8cd29076c1eb62a4da6779cd
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33435399"
---
# <a name="coinitializeee-function"></a>CoInitializeEE, fonction
Garantit que le moteur d’exécution du common language runtime est chargé dans un processus. Cette fonction est déconseillée dans le [!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)]. Utilisez le [ICLRRuntimeHost::Start](../../../../docs/framework/unmanaged-api/hosting/iclrruntimehost-start-method.md) méthode à la place.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
HRESULT CoInitializeEE (  
   [in] DWORD fFlags  
);  
```  
  
#### <a name="parameters"></a>Paramètres  
 `fFlags`  
 [in] Parmi les [COINITIEE](../../../../docs/framework/unmanaged-api/metadata/coinitiee-enumeration.md) constantes d’énumération.  
  
## <a name="return-value"></a>Valeur de retour  
 Cette méthode retourne des codes d’erreur COM standard, tel que défini dans Winerror.h et les valeurs dans le tableau suivant.  
  
|Code de retour|Description|  
|-----------------|-----------------|  
|S_OK|Le moteur d’exécution a été chargé avec succès.|  
|S_FALSE|Le moteur d’exécution est déjà chargé.|  
|E_FAIL|Le moteur d’exécution n’a pas pu être chargé.|  
  
## <a name="remarks"></a>Notes  
 Cette méthode charge le moteur d’exécution s’il n’a pas été précédemment chargé.  
  
## <a name="requirements"></a>Spécifications  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** Cor.h  
  
 **Bibliothèque :** inclus en tant que ressource dans MsCorEE.dll  
  
 **Versions du .NET framework :** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Voir aussi  
 [Fonctions statiques globales des métadonnées](../../../../docs/framework/unmanaged-api/metadata/metadata-global-static-functions.md)
