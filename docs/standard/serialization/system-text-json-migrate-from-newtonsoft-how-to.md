---
title: Migrer de Newtonsoft. JSON vers System. Text. JSON-.NET
author: tdykstra
ms.author: tdykstra
ms.date: 01/10/2020
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 8b3ffc885691264548a19f694d159ce07aba7550
ms.sourcegitcommit: dfad244ba549702b649bfef3bb057e33f24a8fb2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2020
ms.locfileid: "75904683"
---
# <a name="how-to-migrate-from-newtonsoftjson-to-systemtextjson"></a>Comment migrer de Newtonsoft. JSON vers System. Text. JSON

Cet article explique comment effectuer une migration de [Newtonsoft. JSON](https://www.newtonsoft.com/json) vers <xref:System.Text.Json>.

 `System.Text.Json` se concentre principalement sur les performances, la sécurité et la conformité aux normes. Il présente certaines différences clés dans le comportement par défaut et n’a pas pour but d’avoir une parité des fonctionnalités avec `Newtonsoft.Json`. Dans certains scénarios, `System.Text.Json` n’a pas de fonctionnalité intégrée, mais il existe des solutions de contournement recommandées. Pour les autres scénarios, les solutions de contournement ne sont pas pratiques. Si votre application dépend d’une fonctionnalité manquante, envisagez de signaler [un problème](https://github.com/dotnet/runtime/issues/new) pour déterminer si la prise en charge de votre scénario peut être ajoutée.

<!-- For information about which features might be added in future releases, see the [Roadmap](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/roadmap/README.md). [Restore this when the roadmap is updated.]-->

La majeure partie de cet article concerne l’utilisation de l’API <xref:System.Text.Json.JsonSerializer>, mais elle fournit également des conseils sur l’utilisation de l' <xref:System.Text.Json.JsonDocument> (qui représente les types Document Object Model ou DOM), <xref:System.Text.Json.Utf8JsonReader>et <xref:System.Text.Json.Utf8JsonWriter>. L’article est organisé en sections dans l’ordre suivant :

* [Différences dans le comportement de jsonSerializer **par défaut** par rapport à Newtonsoft. JSON](#differences-in-default-jsonserializer-behavior-compared-to-newtonsoftjson)
* [Scénarios utilisant des JsonSerializer qui requièrent des solutions de contournement](#scenarios-using-jsonserializer-that-require-workarounds)
* [Les scénarios que JsonSerializer ne prend pas en charge actuellement](#scenarios-that-jsonserializer-currently-doesnt-support)
* [JsonDocument et JsonElement comparés à JToken (comme JObject, JArray)](#jsondocument-and-jsonelement-compared-to-jtoken-like-jobject-jarray)
* [Utf8JsonReader comparé à JsonTextReader](#utf8jsonreader-compared-to-jsontextreader)
* [Utf8JsonWriter comparé à JsonTextWriter](#utf8jsonwriter-compared-to-jsontextwriter)

## <a name="differences-in-default-jsonserializer-behavior-compared-to-newtonsoftjson"></a>Différences dans le comportement de JsonSerializer par défaut par rapport à Newtonsoft. JSON

<xref:System.Text.Json> est strict par défaut et évite toute estimation ou interprétation au nom de l’appelant, en soulignant le comportement déterministe. La bibliothèque est intentionnellement conçue de cette façon pour les performances et la sécurité. `Newtonsoft.Json` est flexible par défaut. Cette différence fondamentale en matière de conception repose sur la plupart des différences spécifiques suivantes dans le comportement par défaut.

### <a name="case-insensitive-deserialization"></a>Désérialisation non sensible à la casse 

Pendant la désérialisation, `Newtonsoft.Json` ne respecte pas la casse par défaut des noms de propriété qui ne respectent pas la casse. La valeur par défaut de la <xref:System.Text.Json> est sensible à la casse, ce qui offre de meilleures performances, car elle fait une correspondance exacte. Pour plus d’informations sur la façon d’effectuer une correspondance qui ne respecte pas la casse, consultez [correspondance de propriété](system-text-json-how-to.md#case-insensitive-property-matching)ne respectant pas la casse.

Si vous utilisez `System.Text.Json` indirectement à l’aide d’ASP.NET Core, vous n’avez rien à faire pour vous procurer un comportement comme `Newtonsoft.Json`. ASP.NET Core spécifie les paramètres pour les [noms de propriété en casse mixte](system-text-json-how-to.md#use-camel-case-for-all-json-property-names) et la correspondance ne respectant pas la casse lorsqu’il utilise `System.Text.Json`.

### <a name="comments"></a>Comments

Pendant la désérialisation, `Newtonsoft.Json` ignore par défaut les commentaires dans le JSON. La <xref:System.Text.Json> par défaut consiste à lever des exceptions pour les commentaires, car la spécification [RFC 8259](https://tools.ietf.org/html/rfc8259) ne les inclut pas. Pour plus d’informations sur l’autorisation des commentaires, consultez [autoriser les commentaires et les virgules de fin](system-text-json-how-to.md#allow-comments-and-trailing-commas).

### <a name="trailing-commas"></a>Virgules de fin

Au cours de la désérialisation, `Newtonsoft.Json` ignore les virgules de fin par défaut. Elle ignore également plusieurs virgules de fin (par exemple, `[{"Color":"Red"},{"Color":"Green"},,]`). La <xref:System.Text.Json> par défaut consiste à lever des exceptions pour les virgules de fin, car la spécification [RFC 8259](https://tools.ietf.org/html/rfc8259) ne les autorise pas. Pour plus d’informations sur la façon de faire `System.Text.Json` les accepter, consultez [autoriser les commentaires et les virgules de fin](system-text-json-how-to.md#allow-comments-and-trailing-commas). Il n’existe aucun moyen d’autoriser plusieurs virgules de fin.

### <a name="json-strings-property-names-and-string-values"></a>Chaînes JSON (noms de propriété et valeurs de chaîne)

Pendant la désérialisation, `Newtonsoft.Json` accepte les noms de propriété placés entre guillemets doubles, apostrophes ou sans guillemets. Il accepte les valeurs de chaîne entourées de guillemets doubles ou de guillemets simples. Par exemple, `Newtonsoft.Json` accepte le code JSON suivant :

```json
{
  "name1": "value",
  'name2': "value",
  name3: 'value'
}
```

`System.Text.Json` accepte uniquement les noms de propriété et les valeurs de chaîne entre guillemets doubles, car ce format est requis par la spécification [RFC 8259](https://tools.ietf.org/html/rfc8259) et est le seul format considéré comme un JSON valide.

Une valeur placée entre guillemets simples donne un [JsonException](xref:System.Text.Json.JsonException) avec le message suivant :

```
''' is an invalid start of a value.
```

### <a name="non-string-values-for-string-properties"></a>Valeurs qui ne sont pas des chaînes pour les propriétés de chaîne

`Newtonsoft.Json` accepte les valeurs qui ne sont pas des chaînes, telles qu’un nombre ou les littéraux `true` et `false`, pour la désérialisation des propriétés de type String. Voici un exemple de code JSON qui `Newtonsoft.Json` désérialise avec succès vers la classe suivante :

```json
{
  "String1": 1,
  "String2": true,
  "String3": false
}
```

```csharp
public class ExampleClass
{
    public string String1 { get; set; }
    public string String2 { get; set; }
    public string String3 { get; set; }
}
```

`System.Text.Json` ne désérialise pas les valeurs qui ne sont pas des chaînes dans les propriétés de chaîne. Une valeur qui n’est pas une chaîne reçue pour un champ de chaîne génère un [JsonException](xref:System.Text.Json.JsonException) avec le message suivant :

```
The JSON value could not be converted to System.String.
```

### <a name="converter-registration-precedence"></a>Priorité d’inscription du convertisseur

La priorité d’inscription `Newtonsoft.Json` pour les convertisseurs personnalisés est la suivante :

* Attribut sur la propriété
* Attribut sur le type
* [Converters](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonSerializerSettings_Converters.htm) , collection

Dans cet ordre, un convertisseur personnalisé dans la collection `Converters` est substitué par un convertisseur qui est inscrit en appliquant un attribut au niveau du type. Ces deux inscriptions sont remplacées par un attribut au niveau de la propriété.

La priorité d’inscription <xref:System.Text.Json> pour les convertisseurs personnalisés est différente :

* Attribut sur la propriété
* collection <xref:System.Text.Json.JsonSerializerOptions.Converters>
* Attribut sur le type

La différence réside dans le fait qu’un convertisseur personnalisé dans la collection `Converters` remplace un attribut au niveau du type. L’objectif derrière cet ordre de priorité est de faire en sorte que les modifications au moment de l’exécution remplacent les choix au moment de la conception. Il n’existe aucun moyen de modifier la précédence.

Pour plus d’informations sur l’inscription d’un convertisseur personnalisé, consultez [inscrire un convertisseur personnalisé](system-text-json-converters-how-to.md#register-a-custom-converter).

### <a name="character-escaping"></a>Échappement de caractères

Au cours de la sérialisation, `Newtonsoft.Json` est relativement permissif quant à la possibilité de laisser des caractères sans les placer dans une séquence d’échappement. Autrement dit, il ne les remplace pas par `\uxxxx` où `xxxx` est le point de code du caractère. Lorsqu’il les échappe, il émet une `\` avant le caractère (par exemple, `"` devient `\"`). <xref:System.Text.Json> échappe plus de caractères par défaut pour fournir des protections en profondeur contre les attaques de script entre sites (XSS) ou de divulgation d’informations et le fait à l’aide de la séquence de six caractères. `System.Text.Json` échappe par défaut tous les caractères non-ASCII. vous n’avez donc pas besoin de faire quoi que ce soit si vous utilisez `StringEscapeHandling.EscapeNonAscii` dans `Newtonsoft.Json`. par défaut, `System.Text.Json` échappe également aux caractères HTML. Pour plus d’informations sur la façon de substituer le comportement de `System.Text.Json` par défaut, consultez [personnaliser l’encodage de caractères](system-text-json-how-to.md#customize-character-encoding).

### <a name="deserialization-of-object-properties"></a>Désérialisation des propriétés de l’objet

Lorsque `Newtonsoft.Json` désérialise sur `object` propriétés dans POCO ou dans des dictionnaires de type `Dictionary<string, object>`, il :

* Déduit le type de valeurs primitives dans la charge utile JSON (autre que `null`) et retourne le `string`stocké, `long`, `double`, `boolean`ou `DateTime` en tant qu’objet boxed. Les *valeurs primitives* sont des valeurs JSON uniques, telles qu’un nombre JSON, une chaîne, `true`, `false`ou `null`.
* Retourne un `JObject` ou `JArray` pour les valeurs complexes dans la charge utile JSON. Les *valeurs complexes* sont des collections de paires clé-valeur JSON entre accolades (`{}`) ou des listes de valeurs entre crochets (`[]`). Les propriétés et les valeurs entre accolades ou crochets peuvent avoir des propriétés ou des valeurs supplémentaires.
* Retourne une référence Null lorsque la charge utile a le littéral JSON `null`.

<xref:System.Text.Json> stocke un `JsonElement` boxed pour les valeurs primitives et complexes dans la `System.Object` la valeur de la propriété ou du dictionnaire. Toutefois, il traite `null` identique à `Newtonsoft.Json` et retourne une référence Null lorsque la charge utile contient le littéral JSON `null`.

Pour implémenter l’inférence de type pour les propriétés de `object`, créez un convertisseur comme dans l’exemple d' [écriture de convertisseurs personnalisés](system-text-json-converters-how-to.md#deserialize-inferred-types-to-object-properties).

### <a name="maximum-depth"></a>Profondeur maximale

`Newtonsoft.Json` n’a pas de limite de profondeur maximale par défaut. Par <xref:System.Text.Json> il existe une limite par défaut de 64, qui peut être configurée en définissant <xref:System.Text.Json.JsonSerializerOptions.MaxDepth?displayProperty=nameWithType>.

### <a name="stack-type-handling"></a>Gestion des types de pile

Dans <xref:System.Text.Json>, l’ordre du contenu d’une pile est inversé lorsqu’il est sérialisé. Ce comportement s’applique aux types et à l’interface et aux types définis par l’utilisateur suivants qui dérivent de ceux-ci :

* <xref:System.Collections.Stack>
* <xref:System.Collections.Generic.Stack%601>
* <xref:System.Collections.Immutable.ImmutableStack%601>
* <xref:System.Collections.Immutable.IImmutableStack%601>

Un convertisseur personnalisé peut être implémenté pour conserver le contenu de la pile dans le même ordre.

### <a name="omit-null-value-properties"></a>Omettre les propriétés de valeur null

`Newtonsoft.Json` a un paramètre global qui fait que les propriétés de valeur NULL sont exclues de la sérialisation : [NullValueHandling. ignore](https://www.newtonsoft.com/json/help/html/T_Newtonsoft_Json_NullValueHandling.htm). L’option correspondante dans <xref:System.Text.Json> est <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues%2A>.

## <a name="scenarios-using-jsonserializer-that-require-workarounds"></a>Scénarios utilisant des JsonSerializer qui requièrent des solutions de contournement

Les scénarios suivants ne sont pas pris en charge par les fonctionnalités intégrées, mais un exemple de code est fourni pour les solutions de contournement. La plupart des solutions de contournement requièrent l’implémentation de [convertisseurs personnalisés](system-text-json-converters-how-to.md).

### <a name="specify-date-format"></a>Spécifier le format de la date

`Newtonsoft.Json` offre plusieurs moyens de contrôler la sérialisation et la désérialisation des propriétés des types `DateTime` et `DateTimeOffset` :

* Le paramètre `DateTimeZoneHandling` peut être utilisé pour sérialiser toutes les valeurs de `DateTime` en tant que dates UTC.
* Le paramètre `DateFormatString` et les convertisseurs de `DateTime` peuvent être utilisés pour personnaliser le format des chaînes de date.

Dans <xref:System.Text.Json>, le seul format qui offre une prise en charge intégrée est ISO 8601-1:2019, car il est largement adopté, sans ambiguïté, et effectue des allers-retours avec précision. Pour utiliser n’importe quel autre format, créez un convertisseur personnalisé. Pour plus d’informations, consultez [prise en charge des valeurs DateTime et DateTimeOffset dans System. Text. JSON](../datetime/system-text-json-support.md).

### <a name="quoted-numbers"></a>Nombres entre guillemets

`Newtonsoft.Json` pouvez sérialiser ou désérialiser des nombres représentés par des chaînes JSON (entourées de guillemets). Par exemple, il peut accepter : `{"DegreesCelsius":"23"}` au lieu de `{"DegreesCelsius":23}`. Pour activer ce comportement dans <xref:System.Text.Json>, implémentez un convertisseur personnalisé comme dans l’exemple suivant. Le convertisseur gère les propriétés définies en tant que `long`:

* Il les sérialise en tant que chaînes JSON. 
* Il accepte les nombres et nombres JSON dans les guillemets lors de la désérialisation.

[!code-csharp[](~/samples/snippets/core/system-text-json/csharp/LongToStringConverter.cs)]

Inscrivez ce convertisseur personnalisé à [l’aide d’un attribut](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-property) sur des propriétés de `long` individuelles ou en [ajoutant le convertisseur](system-text-json-converters-how-to.md#registration-sample---converters-collection) à la collection de <xref:System.Text.Json.JsonSerializerOptions.Converters>.

### <a name="dictionary-with-non-string-key"></a>Dictionnaire avec clé non-chaîne

`Newtonsoft.Json` prend en charge les collections de type `Dictionary<TKey, TValue>`. La prise en charge intégrée pour les collections de dictionnaires dans <xref:System.Text.Json> est limitée à `Dictionary<string, TValue>`. Autrement dit, la clé doit être une chaîne.

Pour prendre en charge un dictionnaire avec un entier ou un autre type en tant que clé, créez un convertisseur comme l’exemple dans [Comment écrire des convertisseurs personnalisés](system-text-json-converters-how-to.md#support-dictionary-with-non-string-key).

### <a name="polymorphic-serialization"></a>Sérialisation polymorphe

`Newtonsoft.Json` effectue automatiquement la sérialisation polymorphe. Pour plus d’informations sur les fonctionnalités de sérialisation polymorphes limitées de <xref:System.Text.Json>, consultez [sérialisation des propriétés de classes dérivées](system-text-json-how-to.md#serialize-properties-of-derived-classes).

La solution de contournement décrite consiste à définir des propriétés qui peuvent contenir des classes dérivées comme `object`de type. Si cela n’est pas possible, une autre option consiste à créer un convertisseur avec une méthode de `Write` pour l’ensemble de la hiérarchie des types d’héritage, comme dans l’exemple de la rubrique [Comment écrire des convertisseurs personnalisés](system-text-json-converters-how-to.md#support-polymorphic-deserialization).

### <a name="polymorphic-deserialization"></a>Désérialisation polymorphe

`Newtonsoft.Json` a un paramètre `TypeNameHandling` qui ajoute des métadonnées de nom de type au JSON lors de la sérialisation. Elle utilise les métadonnées lors de la désérialisation pour effectuer une désérialisation polymorphe. <xref:System.Text.Json> pouvez effectuer une plage limitée de [sérialisation polymorphe](system-text-json-how-to.md#serialize-properties-of-derived-classes) , mais pas de désérialisation polymorphe.

Pour prendre en charge la désérialisation polymorphe, créez un convertisseur comme l’exemple dans [Comment écrire des convertisseurs personnalisés](system-text-json-converters-how-to.md#support-polymorphic-deserialization).

### <a name="required-properties"></a>Propriétés requises

Pendant la désérialisation, <xref:System.Text.Json> ne lève pas d’exception si aucune valeur n’est reçue dans le JSON pour l’une des propriétés du type cible. Par exemple, si vous avez une classe `WeatherForecast` :

[!code-csharp[](~/samples/snippets/core/system-text-json/csharp/WeatherForecast.cs?name=SnippetWF)]

Le code JSON suivant est désérialisé sans erreur :

```json
{
    "TemperatureCelsius": 25,
    "Summary": "Hot"
}
```

Pour faire échouer la désérialisation si aucune propriété `Date` n’est dans le JSON, implémentez un convertisseur personnalisé. L’exemple de code de convertisseur suivant lève une exception si la propriété `Date` n’est pas définie une fois que la désérialisation est terminée :

[!code-csharp[](~/samples/snippets/core/system-text-json/csharp/WeatherForecastRequiredPropertyConverter.cs)]

Inscrivez ce convertisseur personnalisé à l' [aide d’un attribut sur la classe POCO](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-type) ou en [ajoutant le convertisseur](system-text-json-converters-how-to.md#registration-sample---converters-collection) à la collection <xref:System.Text.Json.JsonSerializerOptions.Converters>.

Si vous suivez ce modèle, ne transmettez pas l’objet options lorsque vous appelez de manière récursive <xref:System.Text.Json.JsonSerializer.Serialize%2A> ou <xref:System.Text.Json.JsonSerializer.Deserialize%2A>. L’objet d’options contient la collection <xref:System.Text.Json.JsonSerializerOptions.Converters%2A>. Si vous le transmettez à `Serialize` ou `Deserialize`, le convertisseur personnalisé s’appelle lui-même, en effectuant une boucle infinie qui entraîne une exception de dépassement de capacité de la pile. Si les options par défaut ne sont pas réalisables, créez une nouvelle instance des options avec les paramètres dont vous avez besoin. Cette approche est lente puisque chaque nouvelle instance est mise en cache de façon indépendante.

Le code de convertisseur précédent est un exemple simplifié. Une logique supplémentaire est nécessaire si vous avez besoin de gérer des attributs (tels que [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) ou des options différentes (telles que des encodeurs personnalisés). En outre, l’exemple de code ne gère pas les propriétés pour lesquelles une valeur par défaut est définie dans le constructeur. Cette approche ne fait pas la différence entre les scénarios suivants :

* Une propriété est absente du JSON.
* Une propriété pour un type non Nullable est présente dans le JSON, mais la valeur est la valeur par défaut pour le type, par exemple zéro pour un `int`.
* Une propriété pour un type Nullable est présente dans le JSON, mais la valeur est null.

### <a name="deserialize-null-to-non-nullable-type"></a>Désérialiser la valeur null en type non Nullable 

`Newtonsoft.Json` ne lève pas d’exception dans le scénario suivant :

* `NullValueHandling` est défini sur `Ignore`et
* Pendant la désérialisation, le JSON contient une valeur null pour un type non Nullable.

Dans le même scénario, <xref:System.Text.Json> lève une exception. (Le paramètre de gestion null correspondant est <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues?displayProperty=nameWithType>.)

Si vous êtes propriétaire du type de cible, la meilleure solution consiste à rendre la propriété en question Nullable (par exemple, modifier `int` en `int?`).

Une autre solution consiste à créer un convertisseur pour le type, comme dans l’exemple suivant qui gère les valeurs NULL pour les types de `DateTimeOffset` :

[!code-csharp[](~/samples/snippets/core/system-text-json/csharp/DateTimeOffsetNullHandlingConverter.cs)]

Inscrivez ce convertisseur personnalisé à l' [aide d’un attribut sur la propriété](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-property) ou en [ajoutant le convertisseur](system-text-json-converters-how-to.md#registration-sample---converters-collection) à la collection <xref:System.Text.Json.JsonSerializerOptions.Converters>.

**Remarque :** Le convertisseur précédent **gère les valeurs NULL différemment** de `Newtonsoft.Json` pour les poco qui spécifient des valeurs par défaut. Par exemple, supposons que le code suivant représente votre objet cible :

[!code-csharp[](~/samples/snippets/core/system-text-json/csharp/WeatherForecast.cs?name=SnippetWFWithDefault)]

Et supposons que le code JSON suivant est désérialisé à l’aide du convertisseur précédent :

```json
{
  "Date": null,
  "TemperatureCelsius": 25,
  "Summary": null
}
```

Après la désérialisation, la propriété `Date` a 1/1/0001 (`default(DateTimeOffset)`), autrement dit, la valeur définie dans le constructeur est remplacée. Étant donné les mêmes POCO et JSON, `Newtonsoft.Json` la désérialisation laisse 1/1/2001 dans la propriété `Date`.

### <a name="deserialize-to-immutable-classes-and-structs"></a>Désérialiser en classes et structs immuables

`Newtonsoft.Json` pouvez désérialiser des classes et des structs immuables, car ils peuvent utiliser des constructeurs qui ont des paramètres. <xref:System.Text.Json> prend en charge uniquement les constructeurs sans paramètre public. En guise de solution de contournement, vous pouvez appeler un constructeur avec des paramètres dans un convertisseur personnalisé.

Voici un struct immuable avec plusieurs paramètres de constructeur :

[!code-csharp[](~/samples/snippets/core/system-text-json/csharp/ImmutablePoint.cs#ImmutablePoint)]

Et voici un convertisseur qui sérialise et désérialise ce struct :

[!code-csharp[](~/samples/snippets/core/system-text-json/csharp/ImmutablePointConverter.cs)]

Inscrivez ce convertisseur personnalisé en [ajoutant le convertisseur](system-text-json-converters-how-to.md#registration-sample---converters-collection) à la collection <xref:System.Text.Json.JsonSerializerOptions.Converters>.

Pour obtenir un exemple de convertisseur similaire qui gère les propriétés génériques ouvertes, consultez le [convertisseur intégré pour les paires clé-valeur](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters/JsonValueConverterKeyValuePair.cs).

### <a name="specify-constructor-to-use"></a>Spécifier le constructeur à utiliser

L’attribut `Newtonsoft.Json` `[JsonConstructor]` vous permet de spécifier le constructeur à appeler lors de la désérialisation vers un POCO. <xref:System.Text.Json> prend en charge uniquement les constructeurs sans paramètre. En guise de solution de contournement, vous pouvez appeler le constructeur dont vous avez besoin dans un convertisseur personnalisé. Consultez l’exemple pour [désérialiser des classes et des structs immuables](#deserialize-to-immutable-classes-and-structs).

### <a name="conditionally-ignore-a-property"></a>Ignorer une propriété de façon conditionnelle

`Newtonsoft.Json` dispose de plusieurs méthodes pour ignorer de manière conditionnelle une propriété lors de la sérialisation ou de la désérialisation :

* `DefaultContractResolver` vous permet de sélectionner les propriétés à inclure ou exclure, en fonction de critères arbitraires. 
* Les paramètres `NullValueHandling` et `DefaultValueHandling` sur `JsonSerializerSettings` vous permettent de spécifier que toutes les propriétés de valeur null ou de valeur par défaut doivent être ignorées.
* Les paramètres `NullValueHandling` et `DefaultValueHandling` de l’attribut `[JsonProperty]` vous permettent de spécifier des propriétés individuelles qui doivent être ignorées lorsque la valeur est null ou la valeur par défaut.

<xref:System.Text.Json> fournit les méthodes suivantes pour omettre des propriétés lors de la sérialisation :

* L’attribut [[JsonIgnore]](system-text-json-how-to.md#exclude-individual-properties) sur une propriété provoque l’omission de la propriété du JSON pendant la sérialisation.
* L’option [IgnoreNullValues](system-text-json-how-to.md#exclude-all-null-value-properties) global vous permet d’exclure toutes les propriétés de valeur null.
* L’option [IgnoreReadOnlyProperties](system-text-json-how-to.md#exclude-all-read-only-properties) global vous permet d’exclure toutes les propriétés en lecture seule.

Ces options **ne** vous permettent pas de :

* Ignore toutes les propriétés qui ont la valeur par défaut pour le type.
* Ignorer les propriétés sélectionnées qui ont la valeur par défaut pour le type.
* Ignorer les propriétés sélectionnées si leur valeur est null.
* Ignorer les propriétés sélectionnées en fonction de critères arbitraires évalués au moment de l’exécution. 

Pour cette fonctionnalité, vous pouvez écrire un convertisseur personnalisé. Voici un exemple de modèle POCO et un convertisseur personnalisé qui illustre cette approche :

[!code-csharp[](~/samples/snippets/core/system-text-json/csharp/WeatherForecast.cs?name=SnippetWF)]

[!code-csharp[](~/samples/snippets/core/system-text-json/csharp/WeatherForecastRuntimeIgnoreConverter.cs)]

Le convertisseur fait en sorte que la propriété `Summary` soit omise de la sérialisation si sa valeur est null, une chaîne vide ou « N/A ». 

Inscrivez ce convertisseur personnalisé à l' [aide d’un attribut sur la classe](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-type) ou en [ajoutant le convertisseur](system-text-json-converters-how-to.md#registration-sample---converters-collection) à la collection <xref:System.Text.Json.JsonSerializerOptions.Converters>.

Cette approche nécessite une logique supplémentaire dans les cas suivants :

* Le POCO comprend des propriétés complexes.
* Vous devez gérer des attributs tels que des `[JsonIgnore]` ou des options telles que des encodeurs personnalisés.

### <a name="callbacks"></a>Rappels

`Newtonsoft.Json` vous permet d’exécuter du code personnalisé à plusieurs points dans le processus de sérialisation ou de désérialisation :

* OnDeserializing (au début de la désérialisation d’un objet)
* OnDeserialized (à la fin de la désérialisation d’un objet)
* OnSerializing (au début de la sérialisation d’un objet)
* OnSerialized (à la fin de la sérialisation d’un objet)

Dans <xref:System.Text.Json>, vous pouvez simuler des rappels en écrivant un convertisseur personnalisé. L’exemple suivant montre un convertisseur personnalisé pour un POCO. Le convertisseur comprend du code qui affiche un message à chaque point qui correspond à un rappel `Newtonsoft.Json`.

[!code-csharp[](~/samples/snippets/core/system-text-json/csharp/WeatherForecastCallbacksConverter.cs)]

Inscrivez ce convertisseur personnalisé à l' [aide d’un attribut sur la classe](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-type) ou en [ajoutant le convertisseur](system-text-json-converters-how-to.md#registration-sample---converters-collection) à la collection <xref:System.Text.Json.JsonSerializerOptions.Converters>.

Si vous utilisez un convertisseur personnalisé qui suit l’exemple précédent :

* Le code `OnDeserializing` n’a pas accès à la nouvelle instance POCO. Pour manipuler la nouvelle instance POCO au début de la désérialisation, placez ce code dans le constructeur POCO.
* Ne transmettez pas l’objet d’options lorsque vous appelez `Serialize` ou `Deserialize`de manière récursive. L’objet d’options contient la collection `Converters`. Si vous le transmettez à `Serialize` ou `Deserialize`, le convertisseur sera utilisé, en effectuant une boucle infinie qui entraîne une exception de dépassement de capacité de la pile.

## <a name="scenarios-that-jsonserializer-currently-doesnt-support"></a>Les scénarios que JsonSerializer ne prend pas en charge actuellement

Les solutions de contournement sont possibles pour les scénarios suivants, mais certaines d’entre elles sont relativement difficiles à implémenter. Cet article ne fournit pas d’exemples de code pour les solutions de contournement pour ces scénarios.

Il ne s’agit pas d’une liste exhaustive des fonctionnalités de `Newtonsoft.Json` qui n’ont pas d’équivalents dans `System.Text.Json`. La liste comprend un grand nombre des scénarios qui ont été demandés dans les [problèmes GitHub](https://github.com/dotnet/runtime/issues?q=is%3Aopen+is%3Aissue+label%3Aarea-System.Text.Json) ou les publications [StackOverflow](https://stackoverflow.com/questions/tagged/system.text.json) .

Si vous implémentez une solution de contournement pour l’un de ces scénarios et que vous pouvez partager le code, sélectionnez le bouton «**cette page**» en bas de la page. Cela crée un problème GitHub et l’ajoute aux problèmes répertoriés au bas de la page.

### <a name="types-without-built-in-support"></a>Types sans prise en charge intégrée

<xref:System.Text.Json> ne fournit pas de prise en charge intégrée pour les types suivants :

* <xref:System.Data.DataTable> et types associés
* F#types, tels que les [unions discriminées](../../fsharp/language-reference/discriminated-unions.md), les [types d’enregistrements](../../fsharp/language-reference/records.md)et les types d' [enregistrements anonymes](../../fsharp/language-reference/anonymous-records.md).
* Types de collections dans l’espace de noms <xref:System.Collections.Specialized>
* <xref:System.Dynamic.ExpandoObject>
* <xref:System.TimeZoneInfo>
* <xref:System.Numerics.BigInteger>
* <xref:System.TimeSpan>
* <xref:System.DBNull>
* <xref:System.Type>
* <xref:System.ValueTuple> et ses types génériques associés

Les convertisseurs personnalisés peuvent être implémentés pour les types qui n’ont pas de prise en charge intégrée.

### <a name="public-and-non-public-fields"></a>Champs publics et non publics

`Newtonsoft.Json` pouvez sérialiser et désérialiser des champs ainsi que des propriétés. <xref:System.Text.Json> fonctionne uniquement avec les propriétés publiques. Les convertisseurs personnalisés peuvent fournir cette fonctionnalité.

### <a name="internal-and-private-property-setters-and-getters"></a>Accesseurs set et getters de propriétés internes et privées

`Newtonsoft.Json` pouvez utiliser des accesseurs set et des accesseurs set de propriété privés et internes via l’attribut `JsonProperty`. <xref:System.Text.Json> prend en charge uniquement les accesseurs set publics. Les convertisseurs personnalisés peuvent fournir cette fonctionnalité.

### <a name="preserve-object-references-and-handle-loops"></a>Conserver les références d’objet et gérer les boucles

Par défaut, `Newtonsoft.Json` sérialise par valeur. Par exemple, si un objet contient deux propriétés qui contiennent une référence au même objet `Person`, les valeurs des propriétés de cet objet `Person` sont dupliquées dans le JSON.

`Newtonsoft.Json` a un paramètre `PreserveReferencesHandling` sur `JsonSerializerSettings` qui vous permet de sérialiser par référence :

* Les métadonnées d’identificateur sont ajoutées au JSON créé pour le premier objet `Person`.
* Le JSON créé pour le deuxième `Person` objet contient une référence à cet identificateur à la place des valeurs de propriété.

`Newtonsoft.Json` a également un paramètre `ReferenceLoopHandling` qui vous permet d’ignorer les références circulaires au lieu de lever une exception.

<xref:System.Text.Json> prend en charge uniquement la sérialisation par valeur et lève une exception pour les références circulaires.

### <a name="systemruntimeserialization-attributes"></a>Attributs System. Runtime. Serialization

<xref:System.Text.Json> ne prend pas en charge les attributs de l’espace de noms `System.Runtime.Serialization`, tels que `DataMemberAttribute` et `IgnoreDataMemberAttribute`.

### <a name="octal-numbers"></a>Nombres octaux

`Newtonsoft.Json` traite les nombres avec un zéro non significatif comme des nombres octaux. <xref:System.Text.Json> n’autorise pas les zéros non significatifs, car la spécification [RFC 8259](https://tools.ietf.org/html/rfc8259) ne les autorise pas.

### <a name="populate-existing-objects"></a>Remplir les objets existants

La méthode `JsonConvert.PopulateObject` dans `Newtonsoft.Json` désérialise un document JSON en une instance existante d’une classe, au lieu de créer une nouvelle instance. <xref:System.Text.Json> crée toujours une nouvelle instance du type cible à l’aide du constructeur sans paramètre public par défaut. Les convertisseurs personnalisés peuvent être désérialisés en une instance existante.

### <a name="reuse-rather-than-replace-properties"></a>Réutiliser plutôt que remplacer les propriétés

Le paramètre `Newtonsoft.Json` `ObjectCreationHandling` vous permet de spécifier que les objets dans les propriétés doivent être réutilisés au lieu d’être remplacés lors de la désérialisation. <xref:System.Text.Json> remplace toujours les objets dans les propriétés.  Les convertisseurs personnalisés peuvent fournir cette fonctionnalité.

### <a name="add-to-collections-without-setters"></a>Ajouter aux collections sans Setters

Pendant la désérialisation, `Newtonsoft.Json` ajoute des objets à une collection même si la propriété n’a pas d’accesseur Set. <xref:System.Text.Json> ignore les propriétés qui n’ont pas de méthode setter. Les convertisseurs personnalisés peuvent fournir cette fonctionnalité.

### <a name="missingmemberhandling"></a>MissingMemberHandling

`Newtonsoft.Json` peut être configuré pour lever des exceptions pendant la désérialisation si le JSON comprend des propriétés qui sont manquantes dans le type cible. <xref:System.Text.Json> ignore les propriétés supplémentaires dans JSON, sauf lorsque vous utilisez l' [attribut [JsonExtensionData]](system-text-json-how-to.md#handle-overflow-json). Il n’existe aucune solution de contournement pour la fonctionnalité de membre manquant.

### <a name="tracewriter"></a>TraceWriter

`Newtonsoft.Json` vous permet de déboguer à l’aide d’un `TraceWriter` pour afficher les journaux qui sont générés par la sérialisation ou la désérialisation. <xref:System.Text.Json> n’effectue pas de journalisation.

## <a name="jsondocument-and-jsonelement-compared-to-jtoken-like-jobject-jarray"></a>JsonDocument et JsonElement comparés à JToken (comme JObject, JArray)

<xref:System.Text.Json.JsonDocument?displayProperty=fullName> offre la possibilité d’analyser et de générer un Document Object Model **en lecture seule** à partir de charges utiles JSON existantes. Le DOM fournit un accès aléatoire aux données dans une charge utile JSON. Les éléments JSON qui composent la charge utile sont accessibles via le type de <xref:System.Text.Json.JsonElement>. Le type de `JsonElement` fournit des API pour convertir du texte JSON en types .NET courants. `JsonDocument` expose une propriété <xref:System.Text.Json.JsonDocument.RootElement>.

### <a name="jsondocument-is-idisposable"></a>JsonDocument est IDisposable

`JsonDocument` crée une vue en mémoire des données dans une mémoire tampon regroupée. Par conséquent, contrairement à `JObject` ou `JArray` à partir de `Newtonsoft.Json`, le type de `JsonDocument` implémente `IDisposable` et doit être utilisé à l’intérieur d’un bloc using. 

Retournez uniquement une `JsonDocument` à partir de votre API si vous souhaitez transférer la propriété de la durée de vie et supprimer la responsabilité de l’appelant. Dans la plupart des scénarios, ce n’est pas nécessaire. Si l’appelant doit travailler avec l’ensemble du document JSON, retournez le <xref:System.Text.Json.JsonElement.Clone%2A> du <xref:System.Text.Json.JsonDocument.RootElement%2A>, qui est un <xref:System.Text.Json.JsonElement>. Si l’appelant doit travailler avec un élément particulier dans le document JSON, retournez le <xref:System.Text.Json.JsonElement.Clone%2A> de ce <xref:System.Text.Json.JsonElement>. Si vous retournez l' `RootElement` ou un sous-élément directement sans créer de `Clone`, l’appelant ne pourra pas accéder au `JsonElement` retourné une fois que le `JsonDocument` qui le possède est supprimé.

Voici un exemple qui vous oblige à créer une `Clone`:

```csharp
public JsonElement LookAndLoad(JsonElement source)
{
    string json = File.ReadAllText(source.GetProperty("fileName").GetString());
   
    using (JsonDocument doc = JsonDocument.Parse(json))
    {
        return doc.RootElement.Clone();
    }
}
```

Le code précédent attend un `JsonElement` qui contient une propriété `fileName`. Il ouvre le fichier JSON et crée un `JsonDocument`. La méthode suppose que l’appelant souhaite travailler avec l’ensemble du document, de sorte qu’il retourne le `Clone` du `RootElement`. 

Si vous recevez une `JsonElement` et retournent un sous-élément, il n’est pas nécessaire de retourner une `Clone` du sous-élément. L’appelant est chargé de conserver le `JsonDocument` auquel appartient le `JsonElement` passé. Par exemple :

```csharp
public JsonElement ReturnFileName(JsonElement source)
{
   return source.GetProperty("fileName");
}
```

### <a name="jsondocument-is-read-only"></a>JsonDocument est en lecture seule

Le DOM <xref:System.Text.Json> ne peut pas ajouter, supprimer ou modifier des éléments JSON. Cette méthode est conçue pour les performances et pour réduire les allocations pour l’analyse des tailles de charge utile JSON courantes (c’est-à-dire < 1 Mo). Si votre scénario utilise actuellement un modèle DOM modifiable, l’une des solutions de contournement suivantes peut être possible :

* Pour créer une `JsonDocument` à partir de zéro (autrement dit, sans passer une charge utile JSON existante à la méthode `Parse`), écrivez le texte JSON à l’aide de la `Utf8JsonWriter` et analysez la sortie de celle-ci pour créer un `JsonDocument`.
* Pour modifier une `JsonDocument`existante, utilisez-la pour écrire du texte JSON, apporter des modifications pendant l’écriture et analyser la sortie de celle-ci pour créer une nouvelle `JsonDocument`.
* Pour fusionner les documents JSON existants, équivalents aux API `JObject.Merge` ou `JContainer.Merge` à partir `Newtonsoft.Json`, consultez [ce problème GitHub](https://github.com/dotnet/corefx/issues/42466#issuecomment-570475853).

### <a name="jsonelement-is-a-union-struct"></a>JsonElement est un struct d’Union

`JsonDocument` expose le `RootElement` en tant que propriété de type <xref:System.Text.Json.JsonElement>, qui est une Union, type struct qui englobe tout élément JSON. `Newtonsoft.Json` utilise des types hiérarchiques dédiés comme `JObject`,`JArray`, `JToken`, etc. `JsonElement` est ce que vous pouvez rechercher et énumérer, et vous pouvez utiliser `JsonElement` pour matérialiser des éléments JSON dans des types .NET.

### <a name="how-to-search-a-jsondocument-and-jsonelement-for-sub-elements"></a>Comment rechercher des sous-éléments dans un JsonDocument et JsonElement

Recherche des jetons JSON à l’aide d' `JObject` ou d' `JArray` à partir de `Newtonsoft.Json` tendance à être relativement rapide car il s’agit de recherches dans un dictionnaire. Par comparaison, les recherches sur `JsonElement` requièrent une recherche séquentielle des propriétés et sont donc relativement lentes (par exemple, lors de l’utilisation de `TryGetProperty`). <xref:System.Text.Json> est conçu pour réduire le temps d’analyse initial plutôt que le temps de recherche. Par conséquent, utilisez les approches suivantes pour optimiser les performances lors de la recherche dans un objet `JsonDocument` :

* Utilisez les énumérateurs intégrés (<xref:System.Text.Json.JsonElement.EnumerateArray%2A> et <xref:System.Text.Json.JsonElement.EnumerateObject%2A>) au lieu d’effectuer votre propre indexation ou boucles.
* N’effectuez pas de recherche séquentielle sur l’ensemble du `JsonDocument` par le biais de chaque propriété à l’aide de `RootElement`. Au lieu de cela, recherchez des objets JSON imbriqués en fonction de la structure connue des données JSON. Par exemple, si vous recherchez une propriété `Grade` dans `Student` objets, effectuez une boucle sur les objets `Student` et récupérez la valeur de `Grade` pour chaque objet, plutôt que de rechercher dans tous les objets `JsonElement` recherchant des propriétés `Grade`. Si vous procédez ainsi, vous obtiendrez des passes inutiles sur les mêmes données.

Pour obtenir un exemple de code, consultez [utiliser JsonDocument pour accéder aux données](system-text-json-how-to.md#use-jsondocument-for-access-to-data).

## <a name="utf8jsonreader-compared-to-jsontextreader"></a>Utf8JsonReader comparé à JsonTextReader

<xref:System.Text.Json.Utf8JsonReader?displayProperty=fullName> est un lecteur haute performance, à faible allocation et en avant uniquement pour le texte JSON encodé en UTF-8, lit à partir d’un [ReadOnlySpan\<byte >](xref:System.ReadOnlySpan%601) ou [ReadOnlySequence\<Byte >](xref:System.Buffers.ReadOnlySequence%601). Le `Utf8JsonReader` est un type de bas niveau qui peut être utilisé pour créer des analyseurs et des désérialiseurs personnalisés.

Les sections suivantes expliquent les modèles de programmation recommandés pour l’utilisation de `Utf8JsonReader`.

### <a name="utf8jsonreader-is-a-ref-struct"></a>Utf8JsonReader est un struct Ref

Étant donné que le type de `Utf8JsonReader` est un *struct de référence*, il présente [certaines limitations](../../csharp/language-reference/keywords/ref.md#ref-struct-types). Par exemple, il ne peut pas être stocké en tant que champ sur une classe ou un struct autre qu’un struct Ref. Pour obtenir des performances élevées, ce type doit être un `ref struct` dans la mesure où il doit mettre en cache l’entrée [ReadOnlySpan\<byte >](xref:System.ReadOnlySpan%601), qui est lui-même un struct Ref. En outre, ce type est mutable puisqu’il contient l’État. Par conséquent, **transmettez-le par référence** plutôt que par valeur. Le fait de le passer par valeur génère une copie de struct et les modifications d’État ne sont pas visibles par l’appelant. Cela diffère de `Newtonsoft.Json` dans la mesure où le `Newtonsoft.Json` `JsonTextReader` est une classe. Pour plus d’informations sur l’utilisation des structs de référence, consultez [écriture de C# code sécurisé et efficace](../../csharp/write-safe-efficient-code.md).

### <a name="read-utf-8-text"></a>Lire du texte UTF-8

Pour obtenir les meilleures performances possibles lors de l’utilisation de la `Utf8JsonReader`, lisez les charges utiles JSON déjà encodées en tant que texte UTF-8 plutôt qu’en tant que chaînes UTF-16. Pour obtenir un exemple de code, consultez [Filtrer les données à l’aide de Utf8JsonReader](system-text-json-how-to.md#filter-data-using-utf8jsonreader).

### <a name="read-with-a-stream-or-pipereader"></a>Lire avec un flux ou un PipeReader

Le `Utf8JsonReader` prend en charge la lecture à partir d’un > codé en UTF-8 [ReadOnlySpan\<byte >](xref:System.ReadOnlySpan%601) ou [ReadOnlySequence\<Byte <xref:System.IO.Pipelines.PipeReader>](xref:System.Buffers.ReadOnlySequence%601) (qui est le résultat de la lecture à partir d’un).

Pour la lecture synchrone, vous pouvez lire la charge utile JSON jusqu’à la fin du flux dans un tableau d’octets et la passer dans le lecteur. Pour lire à partir d’une chaîne (qui est encodée au format UTF-16), appelez <xref:System.Text.Encoding.UTF8>.<xref:System.Text.Encoding.GetBytes%2A> pour tout d’abord transcoder la chaîne en un tableau d’octets encodé en UTF-8. Ensuite, transmettez-le à la `Utf8JsonReader`. 

Étant donné que le `Utf8JsonReader` considère que l’entrée est du texte JSON, une marque d’ordre d’octet (BOM) UTF-8 est considérée comme un JSON non valide. L’appelant doit filtrer ce dernier avant de passer les données au lecteur.

Pour obtenir des exemples de code, consultez [use Utf8JsonReader](system-text-json-how-to.md#use-utf8jsonreader).

### <a name="read-with-multi-segment-readonlysequence"></a>Lecture avec ReadOnlySequence à plusieurs segments

Si votre entrée JSON est un [ReadOnlySpan\<octet >](xref:System.ReadOnlySpan%601), chaque élément JSON est accessible à partir de la propriété `ValueSpan` sur le lecteur à mesure que vous parcourez la boucle de lecture. Toutefois, si votre entrée est un [ReadOnlySequence\<byte >](xref:System.Buffers.ReadOnlySequence%601) (qui est le résultat de la lecture à partir d’un <xref:System.IO.Pipelines.PipeReader>), certains éléments JSON peuvent chevaucher plusieurs segments de l’objet `ReadOnlySequence<byte>`. Ces éléments ne sont pas accessibles à partir de <xref:System.Text.Json.Utf8JsonReader.ValueSpan%2A> dans un bloc de mémoire contigu. Au lieu de cela, chaque fois que vous avez un `ReadOnlySequence<byte>` à plusieurs segments comme entrée, interrogez la propriété <xref:System.Text.Json.Utf8JsonReader.HasValueSequence%2A> sur le lecteur pour déterminer comment accéder à l’élément JSON actuel. Voici un modèle recommandé :

```csharp
while (reader.Read())
{
    switch (reader.TokenType)
    {
        // ...
        ReadOnlySpan<byte> jsonElement = reader.HasValueSequence ?
            reader.ValueSequence.ToArray() :
            reader.ValueSpan;
        // ...
    }
}
```

### <a name="use-valuetextequals-for-property-name-lookups"></a>Utiliser ValueTextEquals pour les recherches de nom de propriété

N’utilisez pas <xref:System.Text.Json.Utf8JsonReader.ValueSpan%2A> pour effectuer des comparaisons octet par octet en appelant <xref:System.MemoryExtensions.SequenceEqual%2A> pour les recherches de nom de propriété. Appelez à la place <xref:System.Text.Json.Utf8JsonReader.ValueTextEquals%2A>, car cette méthode annule l’échappement des caractères échappés dans le JSON. Voici un exemple qui montre comment rechercher une propriété nommée « Name » :

[!code-csharp[](~/samples/snippets/core/system-text-json/csharp/ValueTextEqualsExample.cs?name=SnippetDefineUtf8Var)]

[!code-csharp[](~/samples/snippets/core/system-text-json/csharp/ValueTextEqualsExample.cs?name=SnippetUseUtf8Var&highlight=11)]

### <a name="read-null-values-into-nullable-value-types"></a>Lire les valeurs NULL dans les types valeur Nullable

`Newtonsoft.Json` fournit des API qui retournent des <xref:System.Nullable%601>, telles que `ReadAsBoolean`, qui gère une `TokenType` `Null` pour vous en retournant un `bool?`. Les API de `System.Text.Json` intégrées retournent uniquement des types valeur n’acceptant pas les valeurs NULL. Par exemple, <xref:System.Text.Json.Utf8JsonReader.GetBoolean%2A?displayProperty=nameWithType> retourne une `bool`. Elle lève une exception si elle trouve `Null` dans le JSON. Les exemples suivants illustrent deux façons de gérer les valeurs NULL, l’une en retournant un type valeur Nullable et l’autre en retournant la valeur par défaut :

```csharp
public bool? ReadAsNullableBoolean()
{
    _reader.Read();
    if (_reader.TokenType == JsonTokenType.Null)
    {
        return null;
    }
    if (_reader.TokenType != JsonTokenType.True && _reader.TokenType != JsonTokenType.False)
    {
        throw new JsonException();
    }
    return _reader.GetBoolean();
}
```

```csharp
public bool ReadAsBoolean(bool defaultValue)
{
    _reader.Read();
    if (_reader.TokenType == JsonTokenType.Null)
    {
        return defaultValue;
    }
    if (_reader.TokenType != JsonTokenType.True && _reader.TokenType != JsonTokenType.False)
    {
        throw new JsonException();
    }
    return _reader.GetBoolean();
}
```

### <a name="multi-targeting"></a>Multi-ciblage

Si vous devez continuer à utiliser `Newtonsoft.Json` pour certains frameworks cibles, vous pouvez effectuer plusieurs cibles et avoir deux implémentations. Toutefois, cette opération n’est pas évidente et nécessiterait des `#ifdefs` et une duplication source. Une façon de partager autant de code que possible consiste à créer un wrapper `ref struct` autour de `Utf8JsonReader` et `Newtonsoft.Json` `JsonTextReader`. Ce wrapper unifie la surface d’exposition publique tout en isolant les différences de comportement. Cela vous permet d’isoler les modifications principalement à la construction du type, ainsi que de passer le nouveau type par référence. Il s’agit du modèle que la bibliothèque [Microsoft. extensions. DependencyModel](https://www.nuget.org/packages/Microsoft.Extensions.DependencyModel/3.1.0/) suit :

* [UnifiedJsonReader.JsonTextReader.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonReader.JsonTextReader.cs)
* [UnifiedJsonReader.Utf8JsonReader.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonReader.Utf8JsonReader.cs)

## <a name="utf8jsonwriter-compared-to-jsontextwriter"></a>Utf8JsonWriter comparé à JsonTextWriter

<xref:System.Text.Json.Utf8JsonWriter?displayProperty=fullName> est une méthode très performante pour écrire du texte JSON encodé en UTF-8 à partir de types .NET courants comme `String`, `Int32`et `DateTime`. Le writer est un type de bas niveau qui peut être utilisé pour créer des sérialiseurs personnalisés.

Les sections suivantes expliquent les modèles de programmation recommandés pour l’utilisation de `Utf8JsonWriter`.

### <a name="write-with-utf-8-text"></a>Écrire avec du texte UTF-8

Pour obtenir les meilleures performances possibles lors de l’utilisation de la `Utf8JsonWriter`, écrivez les charges utiles JSON déjà encodées en tant que texte UTF-8 plutôt qu’en tant que chaînes UTF-16. Utilisez <xref:System.Text.Json.JsonEncodedText> pour mettre en cache et précoder des noms et des valeurs de propriété de chaîne connus comme statiques, et les transmettre au writer, plutôt que d’utiliser des littéraux de chaîne UTF-16. Cela est plus rapide que la mise en cache et l’utilisation des tableaux d’octets UTF-8.

Cette approche fonctionne également si vous devez effectuer des séquences d’échappement personnalisées. `System.Text.Json` ne vous permet pas de désactiver l’échappement lors de l’écriture d’une chaîne. Toutefois, vous pouvez transmettre votre propre <xref:System.Text.Encodings.Web.JavaScriptEncoder> personnalisé en tant qu’option au writer, ou créer votre propre `JsonEncodedText` qui utilise votre `JavascriptEncoder` pour effectuer l’échappement, puis écrire le `JsonEncodedText` à la place de la chaîne. Pour plus d’informations, consultez [personnaliser l’encodage des caractères](system-text-json-how-to.md#customize-character-encoding).

### <a name="write-raw-values"></a>Écrire des valeurs brutes

La méthode `Newtonsoft.Json` `WriteRawValue` écrit un JSON brut dans lequel une valeur est attendue. <xref:System.Text.Json> n’a pas d’équivalent direct, mais voici une solution de contournement qui garantit que seul le JSON valide est écrit :

```csharp
using JsonDocument doc = JsonDocument.Parse(string);
doc.WriteTo(writer);
```

### <a name="customize-character-escaping"></a>Personnaliser l’échappement des caractères

Le paramètre [StringEscapeHandling](https://www.newtonsoft.com/json/help/html/T_Newtonsoft_Json_StringEscapeHandling.htm) de `JsonTextWriter` offre des options permettant d’échapper tous les caractères non-ASCII **ou** les caractères HTML. Par défaut, `Utf8JsonWriter` place dans une séquence d’échappement tous les caractères non-ASCII **et** html. Cette séquence d’échappement est effectuée pour des raisons de sécurité de défense en profondeur. Pour spécifier une autre stratégie d’échappement, créez un <xref:System.Text.Encodings.Web.JavaScriptEncoder> et définissez <xref:System.Text.Json.JsonWriterOptions.Encoder?displayProperty=nameWithType>. Pour plus d’informations, consultez [personnaliser l’encodage des caractères](system-text-json-how-to.md#customize-character-encoding).

### <a name="customize-json-format"></a>Personnaliser le format JSON

`JsonTextWriter` inclut les paramètres suivants, pour lesquels `Utf8JsonWriter` n’a pas d’équivalent :

* [Mise en retrait](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_Indentation.htm) : spécifie le nombre de caractères à mettre en retrait. `Utf8JsonWriter` effectue toujours une mise en retrait de 2 caractères.
* [IndentChar](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_IndentChar.htm) : spécifie le caractère à utiliser pour la mise en retrait.  `Utf8JsonWriter` utilise toujours l’espace blanc.
* [QuoteChar](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_QuoteChar.htm) : spécifie le caractère à utiliser pour entourer les valeurs de chaîne.  `Utf8JsonWriter` utilise toujours des guillemets doubles.
* [QUOTENAME](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_QuoteName.htm) : spécifie si les noms de propriété doivent être placés entre guillemets.  `Utf8JsonWriter` les entoure toujours de guillemets.

Il n’existe aucune solution de contournement qui vous permettrait de personnaliser le JSON généré par `Utf8JsonWriter` de la façon suivante.

### <a name="write-null-values"></a>Écrire des valeurs null

Pour écrire des valeurs NULL à l’aide de `Utf8JsonWriter`, appelez :

* <xref:System.Text.Json.Utf8JsonWriter.WriteNull%2A> d’écrire une paire clé-valeur avec une valeur NULL comme valeur.
* <xref:System.Text.Json.Utf8JsonWriter.WriteNullValue%2A> d’écrire la valeur null en tant qu’élément d’un tableau JSON.

Pour une propriété de type chaîne, si la chaîne est null, <xref:System.Text.Json.Utf8JsonWriter.WriteString%2A> et <xref:System.Text.Json.Utf8JsonWriter.WriteStringValue%2A> sont équivalents à `WriteNull` et `WriteNullValue`.

### <a name="write-timespan-uri-or-char-values"></a>Écrire les valeurs TimeSpan, Uri ou char

`JsonTextWriter` fournit `WriteValue` méthodes pour les valeurs [TimeSpan](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonTextWriter_WriteValue_18.htm), [URI](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonTextWriter_WriteValue_22.htm)et [char](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonTextWriter_WriteValue_3.htm) . `Utf8JsonWriter` n’a pas de méthode équivalente. Au lieu de cela, mettez en forme ces valeurs en tant que chaînes (en appelant `ToString()`, par exemple) et appelez <xref:System.Text.Json.Utf8JsonWriter.WriteStringValue%2A>.

### <a name="multi-targeting"></a>Multi-ciblage

Si vous devez continuer à utiliser `Newtonsoft.Json` pour certains frameworks cibles, vous pouvez effectuer plusieurs cibles et avoir deux implémentations. Toutefois, cette opération n’est pas évidente et nécessiterait des `#ifdefs` et une duplication source. Une façon de partager autant de code que possible consiste à créer un wrapper autour de `Utf8JsonWriter` et `Newtonsoft` `JsonTextWriter`. Ce wrapper unifie la surface d’exposition publique tout en isolant les différences de comportement. Cela vous permet d’isoler les modifications principalement de la construction du type. La bibliothèque [Microsoft. extensions. DependencyModel](https://www.nuget.org/packages/Microsoft.Extensions.DependencyModel/3.1.0/) est la suivante :

* [UnifiedJsonWriter.JsonTextWriter.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonWriter.JsonTextWriter.cs)
* [UnifiedJsonWriter.Utf8JsonWriter.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonWriter.Utf8JsonWriter.cs)

## <a name="additional-resources"></a>Ressources supplémentaires

<!-- * [System.Text.Json roadmap](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/roadmap/README.md)[Restore this when the roadmap is updated.]-->
* [Vue d’ensemble de System. Text. JSON](system-text-json-overview.md)
* [Utilisation de System. Text. JSON](system-text-json-how-to.md)
* [Comment écrire des convertisseurs personnalisés](system-text-json-converters-how-to.md)
* [Prise en charge des valeurs DateTime et DateTimeOffset dans System. Text. JSON](../datetime/system-text-json-support.md)
* [Informations de référence sur l’API System. Text. JSON](xref:System.Text.Json)
* [Informations de référence sur l’API System. Text. JSON. Serialization](xref:System.Text.Json.Serialization)