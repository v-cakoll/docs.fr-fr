---
title: Assistant Débogage managé raceOnRCWCleanup
description: Passez en revue l’Assistant Débogage managé (MDA) raceOnRCWCleanup, qui est activé si le wrapper RCW est en cours d’utilisation sur un autre thread ou sur la pile de threads de libération dans .NET.
ms.date: 03/30/2017
helpviewer_keywords:
- RCW
- managed debugging assistants (MDAs), RCWs
- race on RCW cleanup
- MDAs (managed debugging assistants), RCWs
- RaceOnRCWCleanup MDA
- runtime callable wrappers
ms.assetid: bee1e9b1-50a8-4c89-9cd9-7dd6b2458187
ms.openlocfilehash: e86ef96bebb648c7927ae5fec8b68fc4429b268b
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85803649"
---
# <a name="raceonrcwcleanup-mda"></a>Assistant Débogage managé raceOnRCWCleanup
L’Assistant Débogage managé (MDA) `raceOnRCWCleanup` est activé quand le Common Language Runtime (CLR) détecte qu’un [wrapper RCW](../../standard/native-interop/runtime-callable-wrapper.md) est en cours d’utilisation au moment où un appel visant à le libérer est effectué à l’aide d’une commande telle que la méthode <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A?displayProperty=nameWithType>.  
  
## <a name="symptoms"></a>Symptômes  
 Violations d'accès ou altération de la mémoire pendant ou après la libération d'un RCW à l'aide de <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A> ou d'une méthode similaire.  
  
## <a name="cause"></a>Cause  
 Le RCW est en cours d'utilisation sur un autre thread ou sur la pile des threads de libération,  et ne peut donc pas être libéré.  
  
## <a name="resolution"></a>Résolution  
 Ne libérez pas un RCW qui pourrait être utilisé dans le thread actuel ou dans d'autres threads.  
  
## <a name="effect-on-the-runtime"></a>Effet sur le runtime  
 Cet Assistant Débogage managé n'a aucun effet sur le CLR.  
  
## <a name="output"></a>Output  
 Message décrivant l'erreur.  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <raceOnRCWCleanup/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Voir aussi

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Diagnostic d’erreurs avec les Assistants Débogage managé](diagnosing-errors-with-managed-debugging-assistants.md)
- [Marshaling d’interopérabilité](../interop/interop-marshaling.md)
