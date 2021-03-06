---
title: Les paramètres génériques utilisés comme types de paramètres optionnels doivent être contraints par classe
ms.date: 07/20/2015
f1_keywords:
- vbc32124
- bc32124
helpviewer_keywords:
- BC32124
ms.assetid: 55aa8b2a-9ce3-4620-a710-2f9b0feb6143
ms.openlocfilehash: 273ea592e73be5d76a4ffef077e691014a108347
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402925"
---
# <a name="generic-parameters-used-as-optional-parameter-types-must-be-class-constrained"></a>Les paramètres génériques utilisés comme types de paramètres optionnels doivent être contraints par classe
Une procédure est déclarée avec un paramètre facultatif qui utilise un paramètre de type qui n’est pas imposé comme étant un type référence.  
  
 Vous devez toujours fournir une valeur par défaut pour chaque paramètre facultatif. Si le paramètre est d’un type référence, la valeur facultative doit être `Nothing` , qui est une valeur valide pour tout type référence. Toutefois, si le paramètre est d’un type valeur, ce type doit être un type de données élémentaire prédéfini par Visual Basic. Cela est dû au fait qu’un type valeur composite, tel qu’une structure définie par l’utilisateur, n’a pas de valeur par défaut valide.  
  
 Quand vous utilisez un paramètre de type pour un paramètre facultatif, vous devez vous assurer qu’il s’agit d’un type référence pour éviter la possibilité d’un type valeur sans valeur par défaut valide. Cela signifie que vous devez contraindre le paramètre de type avec le `Class` mot clé ou avec le nom d’une classe spécifique.  
  
 **ID d’erreur :** BC32124  
  
## <a name="to-correct-this-error"></a>Pour corriger cette erreur  
  
- Contraindre le paramètre de type à accepter uniquement un type référence ou à ne pas l’utiliser pour le paramètre facultatif.  
  
## <a name="see-also"></a>Voir aussi

- [Generic Types in Visual Basic](../../programming-guide/language-features/data-types/generic-types.md)
- [Type List](../statements/type-list.md)
- [Class (instruction)](../statements/class-statement.md)
- [Paramètres facultatifs](../../programming-guide/language-features/procedures/optional-parameters.md)
- [Structures](../../programming-guide/language-features/data-types/structures.md)
- [Résultat](../nothing.md)
