---
title: IMetaDataImport::GetMethodSemantics, méthode
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetMethodSemantics
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetMethodSemantics
helpviewer_keywords:
- GetMethodSemantics method [.NET Framework metadata]
- IMetaDataImport::GetMethodSemantics method [.NET Framework metadata]
ms.assetid: 5e018eaa-d60e-4a0b-a2c5-8c36bd09d905
topic_type:
- apiref
ms.openlocfilehash: 2cfb66203d8f2d69ea188f6913a5ef34dd74791e
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503599"
---
# <a name="imetadataimportgetmethodsemantics-method"></a>IMetaDataImport::GetMethodSemantics, méthode
Obtient des indicateurs qui indiquent la relation entre la méthode référencée par le jeton MethodDef spécifié et la propriété et l’événement associés référencés par le jeton EventProp spécifié.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT GetMethodSemantics (  
   [in]  mdMethodDef   mb,  
   [in]  mdToken       tkEventProp,  
   [out] DWORD         *pdwSemanticsFlags  
);  
```  
  
## <a name="parameters"></a>Paramètres  
 `mb`  
 dans Jeton MethodDef représentant la méthode pour laquelle obtenir les informations de rôle sémantique.  
  
 `tkEventProp`  
 dans Jeton représentant la propriété et l’événement associés pour lesquels obtenir le rôle de la méthode.  
  
 `pdwSemanticsFlags`  
 à Pointeur vers les indicateurs de sémantique associés. Cette valeur est un masque de masque de l’énumération [CorMethodSemanticsAttr,](cormethodsemanticsattr-enumeration.md) .  
  
## <a name="remarks"></a>Remarques  
 La méthode [IMetaDataEmit ::D efineproperty](imetadataemit-defineproperty-method.md) définit les indicateurs de sémantique d’une méthode.  
  
## <a name="requirements"></a>Configuration requise  
 **Plateformes :** Consultez [Configuration requise](../../get-started/system-requirements.md).  
  
 **En-tête :** Cor. h  
  
 **Bibliothèque :** Inclus en tant que ressource dans MsCorEE. dll  
  
 **Versions de .NET Framework :**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Voir aussi

- [IMetaDataImport, interface](imetadataimport-interface.md)
- [IMetaDataImport2, interface](imetadataimport2-interface.md)
