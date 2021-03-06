---
title: 'Expressions conditionnelles : if... puis... tierce'
description: Apprenez à écrire des expressions conditionnelles F# dans pour exécuter différentes branches de code.
ms.date: 05/16/2016
ms.openlocfilehash: d9763f37cd9170c42e968282b54a3ce925e92591
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71083032"
---
# <a name="conditional-expressions-ifthenelse"></a>Expressions conditionnelles :`if...then...else`

L' `if...then...else` expression exécute différentes branches de code et prend également une valeur différente selon l’expression booléenne donnée.

## <a name="syntax"></a>Syntaxe

```fsharp
if boolean-expression then expression1 [ else expression2 ]
```

## <a name="remarks"></a>Notes

Dans la syntaxe précédente, *expression1* s’exécute lorsque l’expression booléenne prend `true`la valeur ; sinon, *Expression2* s’exécute.

Contrairement à d’autres langages `if...then...else` , la construction est une expression, et non une instruction. Cela signifie qu’elle génère une valeur, qui est la valeur de la dernière expression dans la branche qui s’exécute. Les types des valeurs produites dans chaque branche doivent correspondre. S’il n’existe aucune `else` branche explicite, son type `unit`est. Par conséquent, si le type de `then` la branche est un type autre `unit`que, il doit exister `else` une branche avec le même type de retour. Lors du Chaînage `if...then...else` d’expressions, vous pouvez utiliser le mot `elif` clé à `else if`la place de ; ils sont équivalents.

## <a name="example"></a>Exemple

L’exemple suivant illustre l’utilisation de l' `if...then...else` expression.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4501.fs)]

```console
10 is less than 20
What is your name? John
How old are you? 9
You are only 9 years old and already learning F#? Wow!
```

## <a name="see-also"></a>Voir aussi

- [Informations de référence du langage F#](index.md)
