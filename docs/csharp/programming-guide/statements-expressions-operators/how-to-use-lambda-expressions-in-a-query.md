---
title: Comment utiliser les expressions lambda dans une requête - Guide de programmation C
ms.date: 07/20/2015
helpviewer_keywords:
- lambda expressions [C#], in LINQ
ms.assetid: 3cac4d25-d11f-4abd-9e7c-0f02e97ae06d
ms.openlocfilehash: 92bdbf842c5c30b2f32e06f622f3e08f3c7a878f
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2020
ms.locfileid: "75711959"
---
# <a name="how-to-use-lambda-expressions-in-a-query-c-programming-guide"></a>Comment utiliser les expressions lambda dans une requête (Guide de programmation C)
Vous n’utilisez pas d’expressions lambda directement dans la syntaxe de requête, mais vous les utilisez dans les appels de méthode qui peuvent être contenus dans des expressions de requête. En effet, certaines opérations de requête ne peuvent être exprimées que dans une syntaxe de méthode. Pour plus d’informations sur la différence entre la syntaxe de requête et la syntaxe de méthode, consultez [Syntaxe de requête et syntaxe de méthode dans LINQ](../concepts/linq/query-syntax-and-method-syntax-in-linq.md).  
  
## <a name="example"></a> Exemple  
 L’exemple suivant montre comment utiliser une expression lambda dans une requête fondée sur une méthode à l’aide de l’opérateur de requête standard <xref:System.Linq.Enumerable.Where%2A?displayProperty=nameWithType>. Notez que la méthode <xref:System.Linq.Enumerable.Where%2A> de cet exemple a un paramètre d’entrée du type délégué <xref:System.Func%602>, et que ce délégué prend un entier comme entrée et retourne une valeur booléenne. L’expression lambda peut être convertie en ce délégué. S’il s’agissait d’une requête [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] utilisant la méthode <xref:System.Linq.Queryable.Where%2A?displayProperty=nameWithType>, le type de paramètre serait un `Expression<Func<int,bool>>`, mais l’expression lambda serait exactement la même. Pour plus d’informations sur le type Expression, consultez <xref:System.Linq.Expressions.Expression?displayProperty=nameWithType>.  
  
 [!code-csharp[csProgGuideLINQ#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csrefLINQHowTos.cs#1)]  
  
## <a name="example"></a> Exemple  
 L’exemple suivant montre comment utiliser une expression lambda dans un appel de méthode d’une expression de requête. L’expression lambda est nécessaire, car l’opérateur de requête standard <xref:System.Linq.Enumerable.Sum%2A> ne peut pas être appelé à l’aide de la syntaxe de requête.  
  
 La requête regroupe d’abord les étudiants selon leurs notes, comme défini dans l’enum `GradeLevel`. Ensuite, pour chaque groupe, elle ajoute la note totale obtenue par chaque étudiant. Cela nécessite deux opérations `Sum`. Le `Sum` interne calcule la note totale obtenue par chaque étudiant, et le `Sum` externe obtient un total combiné de tous les étudiants du groupe.  
  
 [!code-csharp[csProgGuideLINQ#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csrefLINQHowTos.cs#2)]  
  
## <a name="compiling-the-code"></a>Compilation du code  
 Pour exécuter ce code, copier et `StudentClass` coller la méthode dans le qui est fourni `Main` dans Requête une collection [d’objets](../../linq/query-a-collection-of-objects.md) et l’appeler à partir de la méthode.
  
## <a name="see-also"></a>Voir aussi

- [Expressions lambda](./lambda-expressions.md)
- [Arborescences d’expressions (C#)](../concepts/expression-trees/index.md)
