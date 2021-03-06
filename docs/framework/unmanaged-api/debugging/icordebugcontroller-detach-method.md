---
title: ICorDebugController::Detach, méthode
ms.date: 03/30/2017
api_name:
- ICorDebugController.Detach
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::Detach
helpviewer_keywords:
- Detach method, ICorDebugController interface [.NET Framework debugging]
- ICorDebugController::Detach method [.NET Framework debugging]
ms.assetid: 06fae364-f2c6-4a50-aa7e-3da9f2684dc3
topic_type:
- apiref
ms.openlocfilehash: 480fec4897dac73594515ba8bc0f0e96ceb79ace
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82892916"
---
# <a name="icordebugcontrollerdetach-method"></a>ICorDebugController::Detach, méthode
Détache le débogueur du processus ou du domaine d’application.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT Detach ();  
```  
  
## <a name="remarks"></a>Notes   
 Le processus ou le domaine d’application continue l’exécution normalement, mais l’objet « ICorDebugProcess » ou « ICorDebugAppDomain » n’est plus valide et aucun autre rappel ne se produit.  
  
 Dans la version de .NET Framework 2,0, si le débogage non managé est activé, cette méthode échouera en raison des limitations du système d’exploitation.  
  
## <a name="requirements"></a>Spécifications  
 **Plateformes :** Consultez [Configuration requise](../../get-started/system-requirements.md).  
  
 **En-tête :** CorDebug.idl, CorDebug.h  
  
 **Bibliothèque :** CorGuids.lib  
  
 **Versions de .NET Framework :**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Voir aussi
