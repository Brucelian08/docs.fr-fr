---
title: "IHostTaskManager::Sleep, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostTaskManager.Sleep
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostTaskManager::Sleep
helpviewer_keywords:
- IHostTaskManager::Sleep method [.NET Framework hosting]
- Sleep method, IHostTaskManager interface [.NET Framework hosting]
ms.assetid: f67d25f3-9199-4c5f-b1e8-1c819243cfd5
topic_type: apiref
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: cc26ca7d226c4529b0bc702567e774f2f98b085d
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="ihosttaskmanagersleep-method"></a><span data-ttu-id="a8897-102">IHostTaskManager::Sleep, méthode</span><span class="sxs-lookup"><span data-stu-id="a8897-102">IHostTaskManager::Sleep Method</span></span>
<span data-ttu-id="a8897-103">Avertit l’hôte que la tâche actuelle est mise en veille.</span><span class="sxs-lookup"><span data-stu-id="a8897-103">Notifies the host that the current task is going to sleep.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="a8897-104">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a8897-104">Syntax</span></span>  
  
```  
HRESULT Sleep (  
    [in] DWORD dwMilliseconds,  
    [in] DWORD option  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="a8897-105">Paramètres</span><span class="sxs-lookup"><span data-stu-id="a8897-105">Parameters</span></span>  
 `dwMilliseconds`  
 <span data-ttu-id="a8897-106">[in] Intervalle de temps, en millisecondes, pendant lequel le thread est en veille.</span><span class="sxs-lookup"><span data-stu-id="a8897-106">[in] The time interval, in milliseconds, that the thread will sleep.</span></span>  
  
 `option`  
 <span data-ttu-id="a8897-107">[in] Parmi les [WAIT_OPTION](../../../../docs/framework/unmanaged-api/hosting/wait-option-enumeration.md) valeurs d’énumération indiquant quelle action l’hôte doit prendre si cette action bloque.</span><span class="sxs-lookup"><span data-stu-id="a8897-107">[in] One of the [WAIT_OPTION](../../../../docs/framework/unmanaged-api/hosting/wait-option-enumeration.md) enumeration values, indicating what action the host should take if this action blocks.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="a8897-108">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="a8897-108">Return Value</span></span>  
  
|<span data-ttu-id="a8897-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="a8897-109">HRESULT</span></span>|<span data-ttu-id="a8897-110">Description</span><span class="sxs-lookup"><span data-stu-id="a8897-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="a8897-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="a8897-111">S_OK</span></span>|<span data-ttu-id="a8897-112">`Sleep`retourné avec succès.</span><span class="sxs-lookup"><span data-stu-id="a8897-112">`Sleep` returned successfully.</span></span>|  
|<span data-ttu-id="a8897-113">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="a8897-113">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="a8897-114">Le common language runtime (CLR) n’a pas été chargé dans un processus ou le CLR est dans un état dans lequel il ne peut pas exécuter du code managé ou traiter l’appel avec succès.</span><span class="sxs-lookup"><span data-stu-id="a8897-114">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="a8897-115">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="a8897-115">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="a8897-116">L’appel a expiré.</span><span class="sxs-lookup"><span data-stu-id="a8897-116">The call timed out.</span></span>|  
|<span data-ttu-id="a8897-117">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="a8897-117">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="a8897-118">L’appelant ne possède pas le verrou.</span><span class="sxs-lookup"><span data-stu-id="a8897-118">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="a8897-119">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="a8897-119">HOST_E_ABANDONED</span></span>|<span data-ttu-id="a8897-120">Un événement a été annulé alors qu’un thread bloqué ou une fibre l’attendait.</span><span class="sxs-lookup"><span data-stu-id="a8897-120">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="a8897-121">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="a8897-121">E_FAIL</span></span>|<span data-ttu-id="a8897-122">Une défaillance grave et inconnue s’est produite.</span><span class="sxs-lookup"><span data-stu-id="a8897-122">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="a8897-123">Lorsqu’une méthode retourne E_FAIL, le CLR n’est plus utilisable dans le processus.</span><span class="sxs-lookup"><span data-stu-id="a8897-123">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="a8897-124">Les appels suivants aux méthodes d’hébergement retournent HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="a8897-124">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="a8897-125">Remarques</span><span class="sxs-lookup"><span data-stu-id="a8897-125">Remarks</span></span>  
 <span data-ttu-id="a8897-126">Le CLR appelle généralement `IHostTaskManager::Sleep` lorsque <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> est appelé à partir du code utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a8897-126">The CLR typically calls `IHostTaskManager::Sleep` when <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> is called from user code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a8897-127">Spécifications</span><span class="sxs-lookup"><span data-stu-id="a8897-127">Requirements</span></span>  
 <span data-ttu-id="a8897-128">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="a8897-128">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a8897-129">**En-tête :** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="a8897-129">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="a8897-130">**Bibliothèque :** inclus en tant que ressource dans MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="a8897-130">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="a8897-131">**Versions du .NET framework :**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a8897-131">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a8897-132">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a8897-132">See Also</span></span>  
 [<span data-ttu-id="a8897-133">ICLRTask (Interface)</span><span class="sxs-lookup"><span data-stu-id="a8897-133">ICLRTask Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)  
 [<span data-ttu-id="a8897-134">ICLRTaskManager (Interface)</span><span class="sxs-lookup"><span data-stu-id="a8897-134">ICLRTaskManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)  
 [<span data-ttu-id="a8897-135">IHostTask (Interface)</span><span class="sxs-lookup"><span data-stu-id="a8897-135">IHostTask Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)  
 [<span data-ttu-id="a8897-136">IHostTaskManager (Interface)</span><span class="sxs-lookup"><span data-stu-id="a8897-136">IHostTaskManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)