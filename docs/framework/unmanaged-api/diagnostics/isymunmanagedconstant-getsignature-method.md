---
title: ISymUnmanagedConstant::GetSignature, méthode
ms.date: 03/30/2017
api_name:
- ISymUnmanagedConstant.GetSignature
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedConstant::GetSignature
helpviewer_keywords:
- GetSignature method, ISymUnmanagedConstant interface [.NET Framework debugging]
- ISymUnmanagedConstant::GetSignature method [.NET Framework debugging]
ms.assetid: 3eb41151-a228-43e3-ba8f-e6dd3ceb8542
topic_type:
- apiref
ms.openlocfilehash: 332d60418c744a9391c7c0afc20248c2239b090c
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83441618"
---
# <a name="isymunmanagedconstantgetsignature-method"></a>ISymUnmanagedConstant::GetSignature, méthode
Obtient la signature de la constante.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT GetSignature(  
    [in]  ULONG32  cSig,  
    [out] ULONG32  *pcSig,  
    [out, size_is(cSig),  
        length_is(*pcSig)] BYTE sig[]);  
```  
  
## <a name="parameters"></a>Paramètres  
 `cSig`  
 dans Longueur de la mémoire tampon vers laquelle `pcSig` pointe le paramètre.  
  
 `pcSig`  
 à Pointeur vers un `ULONG32` qui reçoit la taille, en caractères, de la mémoire tampon requise pour contenir la signature.  
  
 `sig`  
 à Mémoire tampon qui stocke la signature.  
  
## <a name="return-value"></a>Valeur de retour  
 S_OK si la méthode est réussie ; Sinon, E_FAIL ou un autre code d’erreur.  
  
## <a name="requirements"></a>Conditions requises  
 **En-tête :** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Voir aussi

- [ISymUnmanagedConstant, interface](isymunmanagedconstant-interface.md)
- [GetName, méthode](isymunmanagedconstant-getname-method.md)
- [GetValue, méthode](isymunmanagedconstant-getvalue-method.md)
