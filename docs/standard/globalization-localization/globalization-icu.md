---
title: Globalisation et ICU
ms.date: 05/21/2020
ms.technology: dotnet-standard
helpviewer_keywords:
- globalization [.NET Framework], about globalization
- global applications, globalization
- international applications [.NET Framework], globalization
- world-ready applications, globalization
- application development [.NET Framework], globalization
- culture, globalization
- icu, icu on windows, ms-icu
ms.openlocfilehash: 6ea848d4a60069e6702b9d60fd90a55f572fb043
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83842526"
---
# <a name="net-globalization-and-icu"></a>Globalisation et ICU .NET

Dans le passé, les API de globalisation .NET utilisaient des bibliothèques sous-jacentes différentes sur différentes plateformes. Sur UNIX, les API utilisaient les [composants internationaux pour Unicode (ICU)](http://site.icu-project.org/home)et sur Windows, ils utilisaient le [service NLS (National Language Support)](/windows/win32/intl/national-language-support). Cela a entraîné certaines différences de comportement dans une poignée d’API de globalisation lors de l’exécution d’applications sur différentes plateformes. Les différences de comportement étaient évidentes dans les domaines suivants :

- Cultures et données de culture
- Casse des chaînes
- Tri et recherche de chaînes
- Trier les clés
- Normalisation des chaînes
- Prise en charge des IDN (Internationalized Domain Names)
- Nom d’affichage du fuseau horaire sur Linux

À compter de .NET 5,0, les développeurs ont plus de contrôle sur la bibliothèque sous-jacente utilisée, ce qui permet aux applications d’éviter les différences entre les plateformes.

## <a name="icu-on-windows"></a>ICU sur Windows

La mise à jour de Windows 10 mai 2019 et les versions ultérieures incluent [ICU. dll](/windows/win32/intl/international-components-for-unicode--icu-) dans le cadre du système d’exploitation et .net 5,0 et versions ultérieures utilisent ICU par défaut. Lors de l’exécution sous Windows, .NET 5,0 et versions ultérieures essaient de charger `icu.dll` et, s’il est disponible, les utilise pour l’implémentation de la globalisation.  Si cette bibliothèque est introuvable ou ne peut pas être chargée, par exemple lors de l’exécution sur des versions antérieures de Windows, .NET 5,0 et versions ultérieures reviennent à l’implémentation basée sur NLS.

> [!NOTE]
> Même quand vous utilisez ICU, `CurrentCulture` les `CurrentUICulture` membres, et `CurrentRegion` continuent d’utiliser les API du système d’exploitation Windows pour honorer les paramètres utilisateur.

### <a name="using-nls-instead-of-icu"></a>Utilisation de NLS au lieu d’ICU

L’utilisation de ICU au lieu de NLS peut entraîner des différences de comportement avec certaines opérations liées à la globalisation. Pour revenir à l’utilisation de NLS, un développeur peut refuser l’implémentation de la bibliothèque ICU. Les applications peuvent activer le mode NLS de l’une des manières suivantes :

- Dans le fichier projet :

```xml
<ItemGroup>
  <RuntimeHostConfigurationOption Include="System.Globalization.UseNls" Value="true" />
</ItemGroup>
```

- Dans le fichier `runtimeconfig.json` :

```json
{
  "runtimeOptions": {
     "configProperties": {
       "System.Globalization.UseNls": true
      }
  }
}
```

- En affectant à la variable `DOTNET_SYSTEM_GLOBALIZATION_USENLS` d’environnement la valeur `true` ou `1` .

> [!NOTE]
> Une valeur définie dans le projet ou dans le `runtimeconfig.json` fichier est prioritaire sur la variable d’environnement.

Pour plus d’informations, consultez [paramètres de configuration au moment](../../core/run-time-config/globalization.md#nls)de l’exécution.

## <a name="app-local-icu"></a>Bibliothèque ICU locale d’application

Chaque version d’ICU peut apporter des correctifs de bogues, ainsi que des données de référentiel de données locales (CLDR) mises à jour qui décrivent les langues du monde. Passer d’une version à une autre peut avoir un impact subtil sur le comportement des applications lorsqu’il s’agit d’opérations liées à la globalisation.  Pour aider les développeurs d’applications à garantir la cohérence de tous les déploiements, .NET 5,0 et versions ultérieures permettent aux applications sur Windows et UNIX de transporter et d’utiliser leur propre copie d’ICU.

Les applications peuvent s’abonner à un mode d’implémentation ICU local d’application de l’une des manières suivantes :

- Dans le fichier projet :

```xml
<ItemGroup>
  <RuntimeHostConfigurationOption Include="System.Globalization.AppLocalIcu" Value="<suffix>:<version> or <version>" />
</ItemGroup>
```

- Dans le fichier `runtimeconfig.json` :

```json
{
  "runtimeOptions": {
     "configProperties": {
       "System.Globalization.AppLocalIcu": "<suffix>:<version> or <version>"
      }
  }
}
```

- En affectant à la variable `DOTNET_SYSTEM_GLOBALIZATION_APPLOCALICU` d’environnement la valeur `<suffix>:<version>` ou `<version>` .

`<suffix>`: Le suffixe facultatif d’une longueur inférieure à 36 caractères, conformément aux conventions d’empaquetage ICU publiques. Lorsque vous créez une bibliothèque ICU personnalisée, vous pouvez la personnaliser pour produire les noms lib et les noms de symboles exportés pour contenir un suffixe, par exemple, `libicuucmyapp` , où `myapp` est le suffixe.

`<version>`: Version ICU valide, par exemple 67,1. Cette version est utilisée pour charger les binaires et pour récupérer les symboles exportés.

Pour charger ICU lorsque le commutateur local de l’application est défini, .NET utilise la <xref:System.Runtime.InteropServices.NativeLibrary.TryLoad%2A?displayProperty=nameWithType> méthode, qui sonde plusieurs chemins d’accès. La méthode essaie d’abord de trouver la bibliothèque dans la `NATIVE_DLL_SEARCH_DIRECTORIES` propriété, qui est créée par l’hôte dotnet en fonction du `deps.json` fichier de l’application. Pour plus d’informations, consultez [détection par défaut](../../core/dependency-loading/default-probing.md).

Pour les applications autonomes, aucune action spéciale n’est requise de la part de l’utilisateur, à l’exception de l’utilisation de la bibliothèque ICU dans le répertoire de l’application (pour les applications autonomes, le répertoire de travail est défini par défaut sur `NATIVE_DLL_SEARCH_DIRECTORIES` ).

Si vous utilisez ICU via un package NuGet, cela fonctionne dans les applications dépendantes du Framework. NuGet résout les ressources natives et les comprend dans le `deps.json` fichier et dans le répertoire de sortie de l’application sous le `runtimes` répertoire. .NET le charge à partir de là.

Pour les applications dépendantes du Framework (non autonomes) où ICU est consommé à partir d’une build locale, vous devez effectuer des étapes supplémentaires. Le kit de développement logiciel (SDK) .NET ne dispose pas encore d’une fonctionnalité pour les fichiers binaires natifs « libres » à incorporer dans `deps.json` (consultez [ce problème du SDK](https://github.com/dotnet/sdk/issues/11373)). Au lieu de cela, vous pouvez l’activer en ajoutant des informations supplémentaires dans le fichier projet de l’application. Par exemple :

```xml
<ItemGroup>
  <IcuAssemblies Include="icu\*.so*" />
  <RuntimeTargetsCopyLocalItems Include="@(IcuAssemblies)" AssetType="native" CopyLocal="true" DestinationSubDirectory="runtimes/linux-x64/native/" DestinationSubPath="%(FileName)%(Extension)" RuntimeIdentifier="linux-x64" NuGetPackageId="System.Private.Runtime.UnicodeData" />
</ItemGroup>
```

Cela doit être fait pour tous les fichiers binaires ICU pour les runtimes pris en charge. En outre, les `NuGetPackageId` métadonnées dans le `RuntimeTargetsCopyLocalItems` groupe d’éléments doivent correspondre à un package NuGet auquel le projet fait référence.

### <a name="macos-behavior"></a>comportement macOS

`macOS`a un comportement différent pour la résolution des bibliothèques dynamiques dépendantes à partir des commandes de chargement spécifiées dans le `match-o` fichier que le chargeur Linux. Dans le chargeur Linux, .NET peut essayer `libicudata` , `libicuuc` et `libicui18n` (dans cet ordre) pour satisfaire le graphique de dépendance ICU. Toutefois, sur macOS, cela ne fonctionne pas. Lors de la création d’une ICU sur macOS, vous pouvez, par défaut, obtenir une bibliothèque dynamique avec ces commandes de chargement dans `libicuuc` . Par exemple :

```sh
~/ % otool -L /Users/santifdezm/repos/icu-build/icu/install/lib/libicuuc.67.1.dylib
/Users/santifdezm/repos/icu-build/icu/install/lib/libicuuc.67.1.dylib:
 libicuuc.67.dylib (compatibility version 67.0.0, current version 67.1.0)
 libicudata.67.dylib (compatibility version 67.0.0, current version 67.1.0)
 /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1281.100.1)
 /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 902.1.0)
```

Ces commandes font simplement référence au nom des bibliothèques dépendantes pour les autres composants d’ICU. Le chargeur effectue la recherche en respectant les `dlopen` conventions, ce qui implique de disposer de ces bibliothèques dans les répertoires système ou de définir les `LD_LIBRARY_PATH` variables env, ou d’avoir une bibliothèque ICU au niveau de l’application. Si vous ne pouvez pas définir `LD_LIBRARY_PATH` ou vous assurer que les fichiers binaires ICU se trouvent au niveau de l’application, vous devrez effectuer des tâches supplémentaires.

Certaines directives pour le chargeur, comme `@loader_path` , indiquent au chargeur de rechercher cette dépendance dans le même répertoire que le fichier binaire de cette commande de chargement. Il existe deux moyens de parvenir à cet objectif :

- `install_name_tool -change`

  Exécutez les commandes suivantes :

```bash
install_name_tool -change "libicudata.67.dylib" "@loader_path/libicudata.67.dylib" /path/to/libicuuc.67.1.dylib
install_name_tool -change "libicudata.67.dylib" "@loader_path/libicudata.67.dylib" /path/to/libicui18n.67.1.dylib
install_name_tool -change "libicuuc.67.dylib" "@loader_path/libicuuc.67.dylib" /path/to/libicui18n.67.1.dylib
```

- Mise à jour corrective de la bibliothèque pour produire les noms d’installation`@loader_path`

  Avant d’exécuter autoconf ( `./runConfigureICU` ), remplacez [ces lignes](https://github.com/unicode-org/icu/blob/ef91cc3673d69a5e00407cda94f39fcda3131451/icu4c/source/config/mh-darwin#L32-L37) par :

```
LD_SONAME = -Wl,-compatibility_version -Wl,$(SO_TARGET_VERSION_MAJOR) -Wl,-current_version -Wl,$(SO_TARGET_VERSION) -install_name @loader_path/$(notdir $(MIDDLE_SO_TARGET))
```
