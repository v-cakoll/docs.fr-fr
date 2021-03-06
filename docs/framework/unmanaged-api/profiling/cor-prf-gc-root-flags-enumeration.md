---
title: COR_PRF_GC_ROOT_FLAGS, énumération
ms.date: 03/30/2017
api_name:
- COR_PRF_GC_ROOT_FLAGS
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_GC_ROOT_FLAGS
helpviewer_keywords:
- COR_PRF_GC_ROOT_FLAGS enumeration [.NET Framework profiling]
ms.assetid: 4611ee6f-0f05-4d84-91e1-e83d5e7dd7e4
topic_type:
- apiref
ms.openlocfilehash: bbc163c71b47e6fee0db89284d6e3fd27e882768
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500884"
---
# <a name="cor_prf_gc_root_flags-enumeration"></a>COR_PRF_GC_ROOT_FLAGS, énumération
Indique une propriété d’une racine de garbage collection.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
typedef enum {  
    COR_PRF_GC_ROOT_PINNING = 0x1,  
    COR_PRF_GC_ROOT_WEAKREF = 0x2,  
    COR_PRF_GC_ROOT_INTERIOR = 0x4,  
    COR_PRF_GC_ROOT_REFCOUNTED = 0x8,  
} COR_PRF_GC_ROOT_FLAGS;  
```  
  
## <a name="members"></a>Membres  
  
|Membre|Description|  
|------------|-----------------|  
|`COR_PRF_GC_ROOT_PINNING`|La racine empêche un garbage collection de déplacer l’objet.|  
|`COR_PRF_GC_ROOT_WEAKREF`|La racine n’empêche pas les garbage collection.|  
|`COR_PRF_GC_ROOT_INTERIOR`|La racine fait référence à un champ de l’objet plutôt qu’à l’objet lui-même.|  
|`COR_PRF_GC_ROOT_REFCOUNTED`|La racine empêche garbage collection si le décompte de références de l’objet est une certaine valeur.|  
  
## <a name="remarks"></a>Remarques  
 `COR_PRF_GC_ROOT_FLAGS`est un masque de données qui fournit des informations supplémentaires sur les racines spéciales. Toutefois, toutes les racines ne sont pas spéciales. Par exemple, certaines racines ne sont pas des références faibles, des pointeurs intérieurs, des épinglés ou des références comptées. Pour ces racines, il n’y a aucun indicateur à transmettre. Par conséquent, les méthodes qui utilisent cette énumération, telles que la méthode [ICorProfilerCallback2 :: RootReferences2](icorprofilercallback2-rootreferences2-method.md) , envoient 0 pour le masque de masque des indicateurs, ce qui indique que tous les indicateurs sont désactivés.  
  
## <a name="requirements"></a>Configuration requise  
 **Plateformes :** Consultez [Configuration requise](../../get-started/system-requirements.md).  
  
 **En-tête :** CorProf.idl, CorProf.h  
  
 **Bibliothèque :** CorGuids.lib  
  
 **Versions de .NET Framework :**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Voir aussi

- [Énumérations de profilage](profiling-enumerations.md)
