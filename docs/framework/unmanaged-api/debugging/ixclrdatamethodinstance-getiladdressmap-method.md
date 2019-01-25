---
title: IXCLRDataMethodInstance::GetILAddressMap Method
ms.date: 01/16/2019
api.name:
- IXCLRDataMethodInstance::GetILAddressMap Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataMethodInstance::GetILAddressMap Method
helpviewer.keywords:
- IXCLRDataMethodInstance::GetILAddressMap Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 8442d1373ede241d262ab41928fd5d9924ec9c80
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54567189"
---
# <a name="ixclrdatamethodinstancegetiladdressmap-method"></a><span data-ttu-id="05288-102">IXCLRDataMethodInstance::GetILAddressMap Method</span><span class="sxs-lookup"><span data-stu-id="05288-102">IXCLRDataMethodInstance::GetILAddressMap Method</span></span>

<span data-ttu-id="05288-103">Obtient le langage intermédiaire aux informations de mappage d’adresse.</span><span class="sxs-lookup"><span data-stu-id="05288-103">Gets the IL to address mapping information.</span></span>

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a><span data-ttu-id="05288-104">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="05288-104">Syntax</span></span>

```
HRESULT GetILAddressMap(
    [in] ULONG32                                   mapLen,
    [out] ULONG32                                 *mapNeeded,
    [out, size_is(mapLen)] CLRDATA_IL_ADDRESS_MAP  maps[]
);
```

### <a name="parameters"></a><span data-ttu-id="05288-105">Paramètres</span><span class="sxs-lookup"><span data-stu-id="05288-105">Parameters</span></span>

<span data-ttu-id="05288-106">`mapLen` [in] La longueur du tableau des mappages fournis.</span><span class="sxs-lookup"><span data-stu-id="05288-106">`mapLen` [in] The length of the provided maps array.</span></span>

<span data-ttu-id="05288-107">`mapNeeded` [out] Le nombre d’entrées de mappage dont a besoin de la méthode.</span><span class="sxs-lookup"><span data-stu-id="05288-107">`mapNeeded` [out] The number of map entries that the method needs.</span></span>

<span data-ttu-id="05288-108">`maps` [out, size_is(mapLen)] Le tableau pour stocker les entrées de mappage.</span><span class="sxs-lookup"><span data-stu-id="05288-108">`maps` [out, size_is(mapLen)] The array for storing the map entries.</span></span>

## <a name="remarks"></a><span data-ttu-id="05288-109">Notes</span><span class="sxs-lookup"><span data-stu-id="05288-109">Remarks</span></span>

<span data-ttu-id="05288-110">La méthode fournie fait partie de la `IXCLRDataMethodInstance` interface et correspond à l’emplacement de la table de la méthode virtuelle de 14.</span><span class="sxs-lookup"><span data-stu-id="05288-110">The provided method is part of the `IXCLRDataMethodInstance` interface and corresponds to the 14th slot of the virtual method table.</span></span>

## <a name="requirements"></a><span data-ttu-id="05288-111">Spécifications</span><span class="sxs-lookup"><span data-stu-id="05288-111">Requirements</span></span>

<span data-ttu-id="05288-112">**Plateformes :** Consultez [Configuration requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="05288-112">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
<span data-ttu-id="05288-113">**En-tête :** Aucun.</span><span class="sxs-lookup"><span data-stu-id="05288-113">**Header:** None</span></span>  
<span data-ttu-id="05288-114">**Bibliothèque :** Aucun.</span><span class="sxs-lookup"><span data-stu-id="05288-114">**Library:** None</span></span>  
<span data-ttu-id="05288-115">**Versions du .NET Framework :** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span><span class="sxs-lookup"><span data-stu-id="05288-115">**.NET Framework Versions:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span></span>  

## <a name="see-also"></a><span data-ttu-id="05288-116">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="05288-116">See also</span></span>

- [<span data-ttu-id="05288-117">Débogage</span><span class="sxs-lookup"><span data-stu-id="05288-117">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)
- [<span data-ttu-id="05288-118">Interface de IXCLRDataMethodInstance</span><span class="sxs-lookup"><span data-stu-id="05288-118">IXCLRDataMethodInstance Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/ixclrdatamethodinstance-interface.md)