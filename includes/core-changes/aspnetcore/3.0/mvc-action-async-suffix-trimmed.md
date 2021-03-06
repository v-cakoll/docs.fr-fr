---
ms.openlocfilehash: 58b1190e3e6a3168d35700eed655f6756e076a29
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2020
ms.locfileid: "75901803"
---
### <a name="mvc-async-suffix-trimmed-from-controller-action-names"></a>MVC : suffixe Async tronqué à partir des noms d’action du contrôleur

Dans le cadre de l’adressage [dotnet/aspnetcore # 4849](https://github.com/dotnet/aspnetcore/issues/4849), ASP.net Core MVC supprime le `Async` suffixe des noms d’action par défaut. À compter de ASP.NET Core 3,0, cette modification affecte à la fois le routage et la génération de liens.

#### <a name="version-introduced"></a>Version introduite

3.0

#### <a name="old-behavior"></a>Ancien comportement

Considérez les ASP.NET Core contrôleur MVC suivants :

```csharp
public class ProductController : Controller
{
    public async IActionResult ListAsync()
    {
        var model = await DbContext.Products.ToListAsync();
        return View(model);
    }
}
```

L’action peut être routable `Product/ListAsync`via. La génération de liens requiert `Async` la spécification du suffixe. Par exemple :

```cshtml
<a asp-controller="Product" asp-action="ListAsync">List</a>
```

#### <a name="new-behavior"></a>Nouveau comportement

Dans ASP.NET Core 3,0, l’action est routable via `Product/List`. Le code de génération de lien `Async` doit omettre le suffixe. Par exemple :

```cshtml
<a asp-controller="Product" asp-action="List">List</a>
```

Cette modification n’affecte pas les noms spécifiés à l’aide de l' `[ActionName]` attribut. Le nouveau comportement peut être désactivé en affectant `false` à `Startup.ConfigureServices`la valeur `MvcOptions.SuppressAsyncSuffixInActionNames` dans :

```csharp
services.AddMvc(options =>
{
   options.SuppressAsyncSuffixInActionNames = false;
});
```

#### <a name="reason-for-change"></a>Motif de modification

Par Convention, les méthodes .NET asynchrones sont suivies d' `Async`un suffixe. Toutefois, lorsqu’une méthode définit une action MVC, il n’est pas souhaitable d’utiliser `Async` le suffixe.

#### <a name="recommended-action"></a>Action recommandée

Si votre application dépend d’actions MVC qui conservent le `Async` suffixe du nom, choisissez l’une des solutions de contournement suivantes :

- Utilisez l' `[ActionName]` attribut pour conserver le nom d’origine.
- Désactivez entièrement le changement de `MvcOptions.SuppressAsyncSuffixInActionNames` nom `false` en `Startup.ConfigureServices`définissant sur dans :

```csharp
services.AddMvc(options =>
{
   options.SuppressAsyncSuffixInActionNames = false;
});
```

#### <a name="category"></a>Category

ASP.NET Core

#### <a name="affected-apis"></a>API affectées

Aucun

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
