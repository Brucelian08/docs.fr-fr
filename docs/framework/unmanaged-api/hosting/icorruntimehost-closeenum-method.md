---
title: "ICorRuntimeHost::CloseEnum, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorRuntimeHost.CloseEnum
api_location: mscoree.dll
api_type: COM
f1_keywords: ICorRuntimeHost::CloseEnum
helpviewer_keywords:
- CloseEnum method, ICorRuntimeHost interface [.NET Framework hosting]
- ICorRuntimeHost::CloseEnum method [.NET Framework hosting]
ms.assetid: f7ce7e8c-0a3e-4587-a180-063e2b85940e
topic_type: apiref
caps.latest.revision: "8"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: b44797f6efaf8904e3df876e9278a977c912ac6e
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="icorruntimehostcloseenum-method"></a><span data-ttu-id="43a3c-102">ICorRuntimeHost::CloseEnum, méthode</span><span class="sxs-lookup"><span data-stu-id="43a3c-102">ICorRuntimeHost::CloseEnum Method</span></span>
<span data-ttu-id="43a3c-103">Réinitialise un énumérateur de domaine au début de la liste des domaines.</span><span class="sxs-lookup"><span data-stu-id="43a3c-103">Resets a domain enumerator back to the beginning of the domain list.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="43a3c-104">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="43a3c-104">Syntax</span></span>  
  
```  
HRESULT CloseEnum (  
    [in] HCORENUM hEnum  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="43a3c-105">Paramètres</span><span class="sxs-lookup"><span data-stu-id="43a3c-105">Parameters</span></span>  
 `hEnum`  
 <span data-ttu-id="43a3c-106">[in] L’énumérateur à réinitialiser.</span><span class="sxs-lookup"><span data-stu-id="43a3c-106">[in] The enumerator to reset.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="43a3c-107">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="43a3c-107">Return Value</span></span>  
  
|<span data-ttu-id="43a3c-108">HRESULT</span><span class="sxs-lookup"><span data-stu-id="43a3c-108">HRESULT</span></span>|<span data-ttu-id="43a3c-109">Description</span><span class="sxs-lookup"><span data-stu-id="43a3c-109">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="43a3c-110">S_OK</span><span class="sxs-lookup"><span data-stu-id="43a3c-110">S_OK</span></span>|<span data-ttu-id="43a3c-111">L’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="43a3c-111">The operation was successful.</span></span>|  
|<span data-ttu-id="43a3c-112">S_FALSE</span><span class="sxs-lookup"><span data-stu-id="43a3c-112">S_FALSE</span></span>|<span data-ttu-id="43a3c-113">L’opération a échoué.</span><span class="sxs-lookup"><span data-stu-id="43a3c-113">The operation failed to complete.</span></span>|  
|<span data-ttu-id="43a3c-114">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="43a3c-114">E_FAIL</span></span>|<span data-ttu-id="43a3c-115">Une défaillance grave et inconnue s’est produite.</span><span class="sxs-lookup"><span data-stu-id="43a3c-115">An unknown, catastrophic failure occurred.</span></span> <span data-ttu-id="43a3c-116">Si une méthode retourne E_FAIL, le common language runtime (CLR) n’est plus utilisable dans le processus.</span><span class="sxs-lookup"><span data-stu-id="43a3c-116">If a method returns E_FAIL, the common language runtime (CLR) is no longer usable in the process.</span></span> <span data-ttu-id="43a3c-117">Les appels suivants à toute API d’hébergement retournent HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="43a3c-117">Subsequent calls to any hosting APIs return HOST_E_CLRNOTAVAILABLE.</span></span>|  
|<span data-ttu-id="43a3c-118">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="43a3c-118">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="43a3c-119">Le CLR n’a pas été chargé dans un processus ou le CLR est dans un état dans lequel il ne peut pas exécuter du code managé ou traiter l’appel avec succès.</span><span class="sxs-lookup"><span data-stu-id="43a3c-119">The CLR has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="43a3c-120">Spécifications</span><span class="sxs-lookup"><span data-stu-id="43a3c-120">Requirements</span></span>  
 <span data-ttu-id="43a3c-121">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="43a3c-121">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="43a3c-122">**En-tête :** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="43a3c-122">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="43a3c-123">**Bibliothèque :** inclus en tant que ressource dans MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="43a3c-123">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="43a3c-124">**Versions du .NET framework :** 1.0, 1.1</span><span class="sxs-lookup"><span data-stu-id="43a3c-124">**.NET Framework Versions:** 1.0, 1.1</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="43a3c-125">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="43a3c-125">See Also</span></span>  
 [<span data-ttu-id="43a3c-126">CorBindToRuntimeEx (fonction)</span><span class="sxs-lookup"><span data-stu-id="43a3c-126">CorBindToRuntimeEx Function</span></span>](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)  
 [<span data-ttu-id="43a3c-127">ICorRuntimeHost (Interface)</span><span class="sxs-lookup"><span data-stu-id="43a3c-127">ICorRuntimeHost Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md)