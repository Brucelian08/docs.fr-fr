---
title: "ICorDebugController::Stop, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugController.Stop
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugController::Stop
helpviewer_keywords:
- Stop method, ICorDebugController interface [.NET Framework debugging]
- ICorDebugController::Stop method [.NET Framework debugging]
ms.assetid: c34e79be-a7fb-479e-8dec-d126a4c330e5
topic_type: apiref
caps.latest.revision: "13"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 4b92d07f8d162123d20c6861d204d73789060906
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugcontrollerstop-method"></a><span data-ttu-id="a1d5f-102">ICorDebugController::Stop, méthode</span><span class="sxs-lookup"><span data-stu-id="a1d5f-102">ICorDebugController::Stop Method</span></span>
<span data-ttu-id="a1d5f-103">Effectue un arrêt coopératif sur tous les threads qui exécutent du code managé dans le processus.</span><span class="sxs-lookup"><span data-stu-id="a1d5f-103">Performs a cooperative stop on all threads that are running managed code in the process.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="a1d5f-104">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a1d5f-104">Syntax</span></span>  
  
```  
HRESULT Stop (  
    [in] DWORD dwTimeoutIgnored  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="a1d5f-105">Paramètres</span><span class="sxs-lookup"><span data-stu-id="a1d5f-105">Parameters</span></span>  
 `dwTimeoutIgnored`  
 <span data-ttu-id="a1d5f-106">Non utilisé.</span><span class="sxs-lookup"><span data-stu-id="a1d5f-106">Not used.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="a1d5f-107">Remarques</span><span class="sxs-lookup"><span data-stu-id="a1d5f-107">Remarks</span></span>  
 <span data-ttu-id="a1d5f-108">`Stop`effectue un arrêt coopératif sur tous les threads en cours d’exécution code managé dans le processus.</span><span class="sxs-lookup"><span data-stu-id="a1d5f-108">`Stop` performs a cooperative stop on all threads running managed code in the process.</span></span> <span data-ttu-id="a1d5f-109">Pendant une session de débogage managé uniquement, les threads non managés peuvent continuer à exécuter (mais sera bloqué lors de la tentative d’appel de code managé).</span><span class="sxs-lookup"><span data-stu-id="a1d5f-109">During a managed-only debugging session, unmanaged threads may continue to run (but will be blocked when trying to call managed code).</span></span> <span data-ttu-id="a1d5f-110">Pendant une session de débogage d’interopérabilité, les threads non managés seront également arrêtés.</span><span class="sxs-lookup"><span data-stu-id="a1d5f-110">During an interop debugging session, unmanaged threads will also be stopped.</span></span> <span data-ttu-id="a1d5f-111">Le `dwTimeoutIgnored` valeur est actuellement ignorée et traitée comme infini (-1).</span><span class="sxs-lookup"><span data-stu-id="a1d5f-111">The `dwTimeoutIgnored` value is currently ignored and treated as INFINITE (-1).</span></span> <span data-ttu-id="a1d5f-112">Si l’arrêt coopératif échoue en raison d’un blocage, tous les threads sont suspendus et E_TIMEOUT est retourné.</span><span class="sxs-lookup"><span data-stu-id="a1d5f-112">If the cooperative stop fails due to a deadlock, all threads are suspended and E_TIMEOUT is returned.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="a1d5f-113">`Stop`est la seule méthode synchrone dans l’API de débogage.</span><span class="sxs-lookup"><span data-stu-id="a1d5f-113">`Stop` is the only synchronous method in the debugging API.</span></span> <span data-ttu-id="a1d5f-114">Lorsque `Stop` retourne S_OK, le processus est arrêté.</span><span class="sxs-lookup"><span data-stu-id="a1d5f-114">When `Stop` returns S_OK, the process is stopped.</span></span> <span data-ttu-id="a1d5f-115">Aucun rappel n’est donné pour notifier les écouteurs de l’arrêt.</span><span class="sxs-lookup"><span data-stu-id="a1d5f-115">No callback is given to notify listeners of the stop.</span></span> <span data-ttu-id="a1d5f-116">Le débogueur doit appeler [ICorDebugController::Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md) pour autoriser la reprise du processus.</span><span class="sxs-lookup"><span data-stu-id="a1d5f-116">The debugger must call [ICorDebugController::Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md) to allow the process to resume.</span></span>  
  
 <span data-ttu-id="a1d5f-117">Le débogueur gère un compteur d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="a1d5f-117">The debugger maintains a stop counter.</span></span> <span data-ttu-id="a1d5f-118">Lorsque le compteur atteint zéro, le contrôleur est repris.</span><span class="sxs-lookup"><span data-stu-id="a1d5f-118">When the counter goes to zero, the controller is resumed.</span></span> <span data-ttu-id="a1d5f-119">Chaque appel à `Stop` ou chaque rappel distribué incrémente le compteur.</span><span class="sxs-lookup"><span data-stu-id="a1d5f-119">Each call to `Stop` or each dispatched callback increments the counter.</span></span> <span data-ttu-id="a1d5f-120">Chaque appel à `ICorDebugController::Continue` décrémente le compteur.</span><span class="sxs-lookup"><span data-stu-id="a1d5f-120">Each call to `ICorDebugController::Continue` decrements the counter.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a1d5f-121">Spécifications</span><span class="sxs-lookup"><span data-stu-id="a1d5f-121">Requirements</span></span>  
 <span data-ttu-id="a1d5f-122">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="a1d5f-122">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a1d5f-123">**En-tête :** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="a1d5f-123">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="a1d5f-124">**Bibliothèque :** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="a1d5f-124">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a1d5f-125">**Versions du .NET framework :**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a1d5f-125">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a1d5f-126">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a1d5f-126">See Also</span></span>  
 