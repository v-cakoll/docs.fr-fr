---
title: x:Subclass, directive
ms.date: 03/30/2017
f1_keywords:
- Subclass
- xSubclass
- x:Subclass
helpviewer_keywords:
- x:Subclass attribute [XAML Services]
- XAML [XAML Services], x:Subclass attribute
- Subclass attribute in XAML [XAML Services]
ms.assetid: 99f66072-8107-4362-ab99-8171dc83b469
ms.openlocfilehash: e85e0fb5a0e1a865ed84a93767f8152a115bbe5f
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/27/2020
ms.locfileid: "82071366"
---
# <a name="xsubclass-directive"></a><span data-ttu-id="87d10-102">x:Subclass, directive</span><span class="sxs-lookup"><span data-stu-id="87d10-102">x:Subclass Directive</span></span>

<span data-ttu-id="87d10-103">Modifie le comportement de compilation de `x:Class` balisage XAML quand il est également fourni.</span><span class="sxs-lookup"><span data-stu-id="87d10-103">Modifies XAML markup compile behavior when `x:Class` is also provided.</span></span> <span data-ttu-id="87d10-104">Au lieu de créer une `x:Class`classe partielle `x:Class` qui est basée sur , le fourni est créé `x:Class`comme une classe intermédiaire, puis votre classe dérivée fournie devrait être basée sur .</span><span class="sxs-lookup"><span data-stu-id="87d10-104">Instead of creating a partial class that is based on `x:Class`, the provided `x:Class` is created as an intermediate class, and then your provided derived class is expected to be based on `x:Class`.</span></span>

## <a name="xaml-attribute-usage"></a><span data-ttu-id="87d10-105">Utilisation d'attributs XAML</span><span class="sxs-lookup"><span data-stu-id="87d10-105">XAML Attribute Usage</span></span>

```xaml
<object x:Class="namespace.classname" x:Subclass="subclassNamespace.subclassName">
   ...
</object>
```

## <a name="xaml-values"></a><span data-ttu-id="87d10-106">Valeurs XAML</span><span class="sxs-lookup"><span data-stu-id="87d10-106">XAML Values</span></span>

|||
|-|-|
|`namespace`|<span data-ttu-id="87d10-107">facultatif.</span><span class="sxs-lookup"><span data-stu-id="87d10-107">Optional.</span></span> <span data-ttu-id="87d10-108">Spécifie un espace `classname`de nom CLR qui contient .</span><span class="sxs-lookup"><span data-stu-id="87d10-108">Specifies a CLR namespace that contains `classname`.</span></span> <span data-ttu-id="87d10-109">Si `namespace` elle est spécifiée, un `namespace` `classname`point (.) sépare et .</span><span class="sxs-lookup"><span data-stu-id="87d10-109">If `namespace` is specified, a dot (.) separates `namespace` and `classname`.</span></span>|
|`classname`|<span data-ttu-id="87d10-110">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="87d10-110">Required.</span></span> <span data-ttu-id="87d10-111">Spécifie le nom CLR de la classe partielle qui relie le XAML chargé et votre code-derrière pour cela XAML.</span><span class="sxs-lookup"><span data-stu-id="87d10-111">Specifies the CLR name of the partial class that connects the loaded XAML and your code-behind for that XAML.</span></span> <span data-ttu-id="87d10-112">Consultez la section Notes.</span><span class="sxs-lookup"><span data-stu-id="87d10-112">See Remarks.</span></span>|
|`subclassNamespace`|<span data-ttu-id="87d10-113">facultatif.</span><span class="sxs-lookup"><span data-stu-id="87d10-113">Optional.</span></span> <span data-ttu-id="87d10-114">Peut être `namespace` différent de si chaque namespace peut résoudre l’autre.</span><span class="sxs-lookup"><span data-stu-id="87d10-114">Can be different from `namespace` if each namespace can resolve the other.</span></span> <span data-ttu-id="87d10-115">Spécifie un espace `subclassName`de nom CLR qui contient .</span><span class="sxs-lookup"><span data-stu-id="87d10-115">Specifies a CLR namespace that contains `subclassName`.</span></span> <span data-ttu-id="87d10-116">Si `subclassName` elle est spécifiée, un `subclassNamespace` `subclassName`point (.) sépare et .</span><span class="sxs-lookup"><span data-stu-id="87d10-116">If `subclassName` is specified, a dot (.) separates `subclassNamespace` and `subclassName`.</span></span>|
|`subclassName`|<span data-ttu-id="87d10-117">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="87d10-117">Required.</span></span> <span data-ttu-id="87d10-118">Spécifie le nom CLR de la sous-classe.</span><span class="sxs-lookup"><span data-stu-id="87d10-118">Specifies the CLR name of the subclass.</span></span>|

## <a name="dependencies"></a><span data-ttu-id="87d10-119">Les dépendances</span><span class="sxs-lookup"><span data-stu-id="87d10-119">Dependencies</span></span>

<span data-ttu-id="87d10-120">[x:La directive de classe](xclass-directive.md) doit également être fournie sur le même objet, et cet objet doit être l’élément racine de la production XAML.</span><span class="sxs-lookup"><span data-stu-id="87d10-120">[x:Class Directive](xclass-directive.md) must also be provided on the same object, and that object must be the root element of the XAML production.</span></span>

## <a name="remarks"></a><span data-ttu-id="87d10-121">Notes</span><span class="sxs-lookup"><span data-stu-id="87d10-121">Remarks</span></span>

<span data-ttu-id="87d10-122">`x:Subclass`l’utilisation est principalement destinée aux langues qui ne prennent pas en charge les déclarations partielles de classe.</span><span class="sxs-lookup"><span data-stu-id="87d10-122">`x:Subclass` usage is primarily intended for languages that do not support partial class declarations.</span></span>

<span data-ttu-id="87d10-123">La classe utilisée `x:Subclass` comme la classe ne `x:Subclass` peut pas être une classe imbriquée, et doit se référer à l’objet racine comme expliqué dans la section "Dépendances".</span><span class="sxs-lookup"><span data-stu-id="87d10-123">The class used as the `x:Subclass` cannot be a nested class, and `x:Subclass` must refer to the root object as explained in the "Dependencies" section.</span></span>

<span data-ttu-id="87d10-124">Dans le cas `x:Subclass` contraire, le sens conceptuel de est indéfini par une mise en œuvre .NET XAML Services.</span><span class="sxs-lookup"><span data-stu-id="87d10-124">Otherwise, the conceptual meaning of `x:Subclass` is undefined by a .NET XAML Services implementation.</span></span> <span data-ttu-id="87d10-125">C’est parce que le comportement .NET XAML Services ne spécifie pas le modèle de programmation global par lequel le balisage XAML et le code de sauvegarde sont connectés.</span><span class="sxs-lookup"><span data-stu-id="87d10-125">This is because .NET XAML Services behavior does not specify the overall programming model by which XAML markup and backing code are connected.</span></span> <span data-ttu-id="87d10-126">Les implémentations `x:Class` `x:Subclass` d’autres concepts liés à des cadres spécifiques qui utilisent des modèles de programmation ou des modèles d’application pour définir comment relier la balisage XAML, la majoration compilée et le code-derrière.</span><span class="sxs-lookup"><span data-stu-id="87d10-126">Implementations of further concepts related to `x:Class` and `x:Subclass` are performed by specific frameworks that use programming models or application models to define how to connect XAML markup, compiled markup, and CLR-based code-behind.</span></span> <span data-ttu-id="87d10-127">Chaque cadre peut avoir ses propres actions de construction qui permettent une partie du comportement, ou des composants spécifiques qui doivent être inclus dans l’environnement de construction.</span><span class="sxs-lookup"><span data-stu-id="87d10-127">Each framework might have its own build actions that enable some of the behavior, or specific components that must be included in the build environment.</span></span> <span data-ttu-id="87d10-128">Dans un cadre, les actions de construction peuvent également varier en fonction du langage CLR spécifique qui est utilisé pour le code-derrière.</span><span class="sxs-lookup"><span data-stu-id="87d10-128">Within a framework, build actions can also vary based on the specific CLR language that is used for the code-behind.</span></span>

## <a name="wpf-usage-notes"></a><span data-ttu-id="87d10-129">Remarques sur l'utilisation de WPF</span><span class="sxs-lookup"><span data-stu-id="87d10-129">WPF Usage Notes</span></span>

<span data-ttu-id="87d10-130">`x:Subclass`peut être sur une racine <xref:System.Windows.Application> de page ou sur `x:Class`la racine dans la définition d’application, qui a déjà .</span><span class="sxs-lookup"><span data-stu-id="87d10-130">`x:Subclass` can be on a page root or on the <xref:System.Windows.Application> root in the application definition, which already has `x:Class`.</span></span> <span data-ttu-id="87d10-131">Déclarer `x:Subclass` sur tout élément autre qu’une page ou une `x:Class` racine d’application, ou le spécifier là où il n’y en a pas, provoque une erreur de compilation.</span><span class="sxs-lookup"><span data-stu-id="87d10-131">Declaring `x:Subclass` on any element other than a page or application root, or specifying it where no `x:Class` exists, causes a compile-time error.</span></span>

<span data-ttu-id="87d10-132">Créer des classes dérivées `x:Subclass` qui fonctionnent correctement pour le scénario est assez complexe.</span><span class="sxs-lookup"><span data-stu-id="87d10-132">Creating derived classes that work correctly for the `x:Subclass` scenario is fairly complex.</span></span> <span data-ttu-id="87d10-133">Vous devrez peut-être examiner les fichiers intermédiaires (les fichiers .g produits dans le dossier obj de votre projet par balisage compiler, avec des noms qui intègrent les noms de fichiers .xaml).</span><span class="sxs-lookup"><span data-stu-id="87d10-133">You might need to examine the intermediate files (the .g files produced in the obj folder of your project by markup compile, with names that incorporate the .xaml file names).</span></span> <span data-ttu-id="87d10-134">Ces fichiers intermédiaires peuvent vous aider à déterminer l’origine de certaines constructions de programmation dans les classes partielles jointes dans l’application compilée.</span><span class="sxs-lookup"><span data-stu-id="87d10-134">These intermediate files can help you determine the origin of certain programming constructs in the joined partial classes in the compiled application.</span></span>

<span data-ttu-id="87d10-135">Les gestionnaires d’événements de `internal override` `Friend Overrides` la classe dérivée doivent être (dans Microsoft Visual Basic) afin de remplacer les talons pour les manutentionnaires tels qu’ils ont été créés dans la classe intermédiaire pendant la compilation.</span><span class="sxs-lookup"><span data-stu-id="87d10-135">Event handlers in the derived class must be `internal override` (`Friend Overrides` in Microsoft Visual Basic) in order to override the stubs for the handlers as created in the intermediate class during compilation.</span></span> <span data-ttu-id="87d10-136">Dans le cas contraire, les implémentations de classe dérivées cachent (ombre) l’implémentation de classe intermédiaire et les gestionnaires de classe intermédiaire ne sont pas invoqués.</span><span class="sxs-lookup"><span data-stu-id="87d10-136">Otherwise, the derived class implementations hide (shadow) the intermediate class implementation and the intermediate class handlers are not invoked.</span></span>

<span data-ttu-id="87d10-137">Lorsque vous `x:Class` définissez les deux et `x:Subclass`, vous n’avez pas `x:Class`besoin de fournir une implémentation pour la classe qui est référencé par .</span><span class="sxs-lookup"><span data-stu-id="87d10-137">When you define both `x:Class` and `x:Subclass`, you do not need to provide any implementation for the class that is referenced by `x:Class`.</span></span> <span data-ttu-id="87d10-138">Vous n’avez qu’à `x:Class` lui donner un nom via l’attribut de sorte que le compilateur a quelques conseils pour la classe qu’il crée dans les fichiers intermédiaires (le compilateur ne sélectionne pas un nom par défaut dans ce cas).</span><span class="sxs-lookup"><span data-stu-id="87d10-138">You only need to give it a name via the `x:Class` attribute so that the compiler has some guidance for the class that it creates in the intermediate files (the compiler does not select a default name in this case).</span></span> <span data-ttu-id="87d10-139">Vous pouvez `x:Class` donner à la classe une mise en œuvre; cependant, ce n’est pas `x:Class` le `x:Subclass`scénario typique pour l’utilisation des deux et .</span><span class="sxs-lookup"><span data-stu-id="87d10-139">You can give the `x:Class` class an implementation; however, this is not the typical scenario for using both `x:Class` and `x:Subclass`.</span></span>

## <a name="see-also"></a><span data-ttu-id="87d10-140">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="87d10-140">See also</span></span>

- [<span data-ttu-id="87d10-141">x:Class, directive</span><span class="sxs-lookup"><span data-stu-id="87d10-141">x:Class Directive</span></span>](xclass-directive.md)
- [<span data-ttu-id="87d10-142">XAML et classes personnalisées pour WPF</span><span class="sxs-lookup"><span data-stu-id="87d10-142">XAML and Custom Classes for WPF</span></span>](../../framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)