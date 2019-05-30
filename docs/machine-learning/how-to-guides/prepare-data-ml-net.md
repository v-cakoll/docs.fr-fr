---
title: Préparer les données
description: Découvrez comment utiliser des transformations dans ML.NET pour manipuler et préparer des données en vue d’effectuer un traitement supplémentaire ou de générer un modèle.
author: luisquintanilla
ms.author: luquinta
ms.date: 05/03/2019
ms.custom: mvc, how-to
ms.openlocfilehash: 461a00c6ecc1d9a8b9caaca79f9d7905d2bb7528
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65063464"
---
# <a name="prepare-data"></a><span data-ttu-id="70db1-103">Préparer les données</span><span class="sxs-lookup"><span data-stu-id="70db1-103">Prepare Data</span></span>

<span data-ttu-id="70db1-104">Découvrez comment utiliser ML.NET pour préparer des données en vue d’effectuer un traitement supplémentaire ou de générer un modèle.</span><span class="sxs-lookup"><span data-stu-id="70db1-104">Learn how to use ML.NET to prepare data for additional processing or building a model.</span></span>

<span data-ttu-id="70db1-105">Les données sont souvent dans un format incorrect et disséminées.</span><span class="sxs-lookup"><span data-stu-id="70db1-105">Data is often unclean and sparse.</span></span> <span data-ttu-id="70db1-106">De plus, les algorithmes de machine Learning ML.NET s’attendent à ce que l’entrée ou les caractéristiques se trouvent dans un vecteur numérique unique.</span><span class="sxs-lookup"><span data-stu-id="70db1-106">Additionally, ML.NET machine learning algorithms expect input or features to be in a single numerical vector.</span></span> <span data-ttu-id="70db1-107">Ainsi, un des objectifs de la préparation des données consiste à obtenir les données dans le format attendu par les algorithmes ML.NET.</span><span class="sxs-lookup"><span data-stu-id="70db1-107">Therefore one of the goals of data preparation is to get the data into the format expected by ML.NET algorithms.</span></span> 

## <a name="filter-data"></a><span data-ttu-id="70db1-108">Filtrer les données</span><span class="sxs-lookup"><span data-stu-id="70db1-108">Filter data</span></span>

<span data-ttu-id="70db1-109">Parfois, toutes les données d’un jeu de données ne sont pas appropriées pour l’analyse.</span><span class="sxs-lookup"><span data-stu-id="70db1-109">Sometimes, not all data in a dataset is relevant for analysis.</span></span> <span data-ttu-id="70db1-110">Une approche pour supprimer les données non pertinentes consiste à effectuer un filtrage.</span><span class="sxs-lookup"><span data-stu-id="70db1-110">An approach to remove irrelevant data is filtering.</span></span> <span data-ttu-id="70db1-111">Le [`DataOperationsCatalog`](xref:Microsoft.ML.DataOperationsCatalog) comporte un ensemble d’opérations de filtre qui acceptent un [`IDataView`](xref:Microsoft.ML.IDataView) contenant toutes les données et retournent un [IDataView](xref:Microsoft.ML.IDataView) contenant uniquement les points de données d’intérêt.</span><span class="sxs-lookup"><span data-stu-id="70db1-111">The [`DataOperationsCatalog`](xref:Microsoft.ML.DataOperationsCatalog) contains a set of filter operations that take in an [`IDataView`](xref:Microsoft.ML.IDataView) containing all of the data and return an [IDataView](xref:Microsoft.ML.IDataView) containing only the data points of interest.</span></span> <span data-ttu-id="70db1-112">Il est important de noter que les opérations de filtre, qui ne sont pas un [`IEstimator`](xref:Microsoft.ML.IEstimator%601) ou [`ITransformer`](xref:Microsoft.ML.ITransformer) comme dans le [`TransformsCatalog`](xref:Microsoft.ML.TransformsCatalog), ne peuvent pas être incluses dans le cadre d’un pipeline de préparation des données [`EstimatorChain`](xref:Microsoft.ML.Data.EstimatorChain%601) ou [`TransformerChain`](xref:Microsoft.ML.Data.TransformerChain%601).</span><span class="sxs-lookup"><span data-stu-id="70db1-112">It's important to note that because filter operations are not an [`IEstimator`](xref:Microsoft.ML.IEstimator%601) or [`ITransformer`](xref:Microsoft.ML.ITransformer) like those in the [`TransformsCatalog`](xref:Microsoft.ML.TransformsCatalog), they cannot be included as part of an [`EstimatorChain`](xref:Microsoft.ML.Data.EstimatorChain%601) or [`TransformerChain`](xref:Microsoft.ML.Data.TransformerChain%601) data preparation pipeline.</span></span> 

<span data-ttu-id="70db1-113">Supposons que nous utilisons les données d’entrée suivantes qui sont chargées dans un [`IDataView`](xref:Microsoft.ML.IDataView) :</span><span class="sxs-lookup"><span data-stu-id="70db1-113">Using the following input data which is loaded into an [`IDataView`](xref:Microsoft.ML.IDataView):</span></span>

```csharp
HomeData[] homeDataList = new HomeData[]
{
    new HomeData
    {
        NumberOfBedrooms=1f,
        Price=100000f
    },
    new HomeData
    {
        NumberOfBedrooms=2f,
        Price=300000f
    },
    new HomeData
    {
        NumberOfBedrooms=6f,
        Price=600000f
    }
};
```

<span data-ttu-id="70db1-114">Pour filtrer les données en fonction de la valeur d’une colonne, utilisez la méthode [`FilterRowsByColumn`](xref:Microsoft.ML.DataOperationsCatalog.FilterRowsByColumn*).</span><span class="sxs-lookup"><span data-stu-id="70db1-114">To filter data based on the value of a column, use the [`FilterRowsByColumn`](xref:Microsoft.ML.DataOperationsCatalog.FilterRowsByColumn*) method.</span></span>

```csharp
// Apply filter
IDataView filteredData = mlContext.Data.FilterRowsByColumn(data, "Price", lowerBound: 200000, upperBound: 1000000);
```

<span data-ttu-id="70db1-115">L’exemple ci-dessus prend les lignes dans le jeu de données ayant un prix entre 200 000 et 1 000 000.</span><span class="sxs-lookup"><span data-stu-id="70db1-115">The sample above takes rows in the dataset with a price between 200000 and 1000000.</span></span> <span data-ttu-id="70db1-116">L’application de ce filtre retourne uniquement les deux dernières lignes dans les données et exclut la première ligne, car son prix, 1 00 000, n’appartient pas à la plage spécifiée.</span><span class="sxs-lookup"><span data-stu-id="70db1-116">The result of applying this filter would return only the last two rows in the data and exclude the first row because its price is 100000 and not between the specified range.</span></span>

## <a name="replace-missing-values"></a><span data-ttu-id="70db1-117">Remplacer les valeurs manquantes</span><span class="sxs-lookup"><span data-stu-id="70db1-117">Replace missing values</span></span>

<span data-ttu-id="70db1-118">Les valeurs manquantes sont courantes dans les jeux de données.</span><span class="sxs-lookup"><span data-stu-id="70db1-118">Missing values are a common occurrence in datasets.</span></span> <span data-ttu-id="70db1-119">Pour traiter les valeurs manquantes, une approche consiste à les remplacer par la valeur par défaut du type donné éventuel ou par une autre valeur significative telle que la valeur moyenne dans les données.</span><span class="sxs-lookup"><span data-stu-id="70db1-119">One approach to dealing with missing values is to replace them with the default value for the given type if any or another meaningful value such as the mean value in the data.</span></span> 

<span data-ttu-id="70db1-120">Supposons que nous utilisons les données d’entrée suivantes qui sont chargées dans un [`IDataView`](xref:Microsoft.ML.IDataView) :</span><span class="sxs-lookup"><span data-stu-id="70db1-120">Using the following input data which is loaded into an [`IDataView`](xref:Microsoft.ML.IDataView):</span></span>

```csharp
HomeData[] homeDataList = new HomeData[]
{
    new HomeData
    {
        NumberOfBedrooms=1f,
        Price=100000f
    },
    new HomeData
    {
        NumberOfBedrooms=2f,
        Price=300000f
    },
    new HomeData
    {
        NumberOfBedrooms=6f,
        Price=float.NaN
    }
};
```

<span data-ttu-id="70db1-121">Notez que le dernier élément dans notre liste a une valeur manquante pour `Price`.</span><span class="sxs-lookup"><span data-stu-id="70db1-121">Notice that the last element in our list has a missing value for `Price`.</span></span> <span data-ttu-id="70db1-122">Pour remplacer la valeur manquante dans la colonne `Price`, utilisez la méthode [`ReplaceMissingValues`](xref:Microsoft.ML.ExtensionsCatalog.ReplaceMissingValues*) afin de remplir cette valeur manquante.</span><span class="sxs-lookup"><span data-stu-id="70db1-122">To replace the missing values in the `Price` column, use the [`ReplaceMissingValues`](xref:Microsoft.ML.ExtensionsCatalog.ReplaceMissingValues*) method to fill in that missing value.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70db1-123">[`ReplaceMissingValue`](xref:Microsoft.ML.ExtensionsCatalog.ReplaceMissingValues*) fonctionne uniquement avec des données numériques.</span><span class="sxs-lookup"><span data-stu-id="70db1-123">[`ReplaceMissingValue`](xref:Microsoft.ML.ExtensionsCatalog.ReplaceMissingValues*) only works with numerical data.</span></span>

```csharp
// Define replacement estimator
var replacementEstimator = mlContext.Transforms.ReplaceMissingValues("Price", replacementMode: MissingValueReplacingEstimator.ReplacementMode.Mean);

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
ITransformer replacementTransformer = replacementEstimator.Fit(data);

// Transform data
IDataView transformedData = replacementTransformer.Transform(data);
```

<span data-ttu-id="70db1-124">ML.NET prend en charge divers [modes de remplacement](xref:Microsoft.ML.Transforms.MissingValueReplacingEstimator.ReplacementMode).</span><span class="sxs-lookup"><span data-stu-id="70db1-124">ML.NET supports various [replacement modes](xref:Microsoft.ML.Transforms.MissingValueReplacingEstimator.ReplacementMode).</span></span> <span data-ttu-id="70db1-125">L’exemple ci-dessus utilise le mode de remplacement `Mean`, qui remplit la valeur manquante avec la valeur moyenne de la colonne concernée.</span><span class="sxs-lookup"><span data-stu-id="70db1-125">The sample above uses the `Mean` replacement mode which will fill in the missing value with that column's average value.</span></span> <span data-ttu-id="70db1-126">Le remplacement se traduit par le remplissage de la propriété `Price` pour le dernier élément dans les données avec la valeur 200 000, soit la moyenne de 100 000 et 300 000.</span><span class="sxs-lookup"><span data-stu-id="70db1-126">The replacement 's result fills in the `Price` property for the last element in our data with 200,000 since it's the average of 100,000 and 300,000.</span></span> 

## <a name="use-normalizers"></a><span data-ttu-id="70db1-127">Utiliser des normaliseurs</span><span class="sxs-lookup"><span data-stu-id="70db1-127">Use normalizers</span></span>

<span data-ttu-id="70db1-128">La [normalisation](https://en.wikipedia.org/wiki/Feature_scaling) est une technique de prétraitement des données utilisée pour normaliser les caractéristiques qui ne sont pas sur la même échelle, ce qui permet aux algorithmes de converger plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="70db1-128">[Normalization](https://en.wikipedia.org/wiki/Feature_scaling) is a data pre-processing technique used to standardize features that are not on the same scale which helps algorithms converge faster.</span></span> <span data-ttu-id="70db1-129">Par exemple, les plages de valeurs telles que l’âge et le revenu varient de façon importante, l’âge étant généralement compris entre 0 et 100 et le revenu entre zéro et plusieurs milliers.</span><span class="sxs-lookup"><span data-stu-id="70db1-129">For example, the ranges for values like age and income vary significantly with age generally being in the range of 0-100 and income generally being in the range of zero to thousands.</span></span> <span data-ttu-id="70db1-130">Consultez la [page sur les transformations](../resources/transforms.md) pour obtenir une liste et une description plus détaillées des transformations de normalisation.</span><span class="sxs-lookup"><span data-stu-id="70db1-130">Visit the [transforms page](../resources/transforms.md) for a more detailed list and description of normalization transforms.</span></span> 

### <a name="min-max-normalization"></a><span data-ttu-id="70db1-131">Normalisation min-max</span><span class="sxs-lookup"><span data-stu-id="70db1-131">Min-Max normalization</span></span>

<span data-ttu-id="70db1-132">Supposons que nous utilisons les données d’entrée suivantes qui sont chargées dans un [`IDataView`](xref:Microsoft.ML.IDataView) :</span><span class="sxs-lookup"><span data-stu-id="70db1-132">Using the following input data which is loaded into an [`IDataView`](xref:Microsoft.ML.IDataView):</span></span>

```csharp
HomeData[] homeDataList = new HomeData[]
{
    new HomeData
    {
        NumberOfBedrooms = 2f,
        Price = 200000f
    },
    new HomeData
    {
        NumberOfBedrooms = 1f,
        Price = 100000f
    }
};
```

<span data-ttu-id="70db1-133">Normalisez les données à l’aide de la normalisation min-max en utilisant la méthode [`NormalizeMinMax`](xref:Microsoft.ML.NormalizationCatalog.NormalizeMinMax*).</span><span class="sxs-lookup"><span data-stu-id="70db1-133">Normalize the data using min-max normalization using the [`NormalizeMinMax`](xref:Microsoft.ML.NormalizationCatalog.NormalizeMinMax*) method.</span></span>

```csharp
// Define min-max estimator
var minMaxEstimator = mlContext.Transforms.NormalizeMinMax("Price");

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
ITransformer minMaxTransformer = minMaxEstimator.Fit(data);

// Transform data
IDataView transformedData = minMaxTransformer.Transform(data);
```

<span data-ttu-id="70db1-134">Les valeurs de prix d’origine `[200000,100000]` sont converties en `[ 1, 0.5 ]` à l’aide de la formule de normalisation `MinMax`, qui génère des valeurs de sortie appartenant à la plage 0-1.</span><span class="sxs-lookup"><span data-stu-id="70db1-134">The original price values `[200000,100000]` are converted to `[ 1, 0.5 ]` using the `MinMax` normalization formula which generates output values in the range of 0-1.</span></span>

### <a name="binning"></a><span data-ttu-id="70db1-135">Quantification</span><span class="sxs-lookup"><span data-stu-id="70db1-135">Binning</span></span>

<span data-ttu-id="70db1-136">La [quantification](https://en.wikipedia.org/wiki/Data_binning) convertit des valeurs continues en une représentation discrète de l’entrée.</span><span class="sxs-lookup"><span data-stu-id="70db1-136">[Binning](https://en.wikipedia.org/wiki/Data_binning) converts continuous values into a discrete representation of the input.</span></span> <span data-ttu-id="70db1-137">Par exemple, supposons qu’une de vos caractéristiques est l’âge.</span><span class="sxs-lookup"><span data-stu-id="70db1-137">For example, suppose one of your features is age.</span></span> <span data-ttu-id="70db1-138">Au lieu d’utiliser la valeur de l’âge réel, la quantification crée des plages pour cette valeur.</span><span class="sxs-lookup"><span data-stu-id="70db1-138">Instead of using the actual age value,  binning creates ranges for that value.</span></span> <span data-ttu-id="70db1-139">0-18 pourrait être une cellule, de même que 19-35, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="70db1-139">0-18 could be one bin, another could be 19-35 and so on.</span></span> 

<span data-ttu-id="70db1-140">Supposons que nous utilisons les données d’entrée suivantes qui sont chargées dans un [`IDataView`](xref:Microsoft.ML.IDataView) :</span><span class="sxs-lookup"><span data-stu-id="70db1-140">Using the following input data which is loaded into an [`IDataView`](xref:Microsoft.ML.IDataView):</span></span>

```csharp
HomeData[] homeDataList = new HomeData[]
{
    new HomeData
    {
        NumberOfBedrooms=1f,
        Price=100000f
    },
    new HomeData
    {
        NumberOfBedrooms=2f,
        Price=300000f
    },
    new HomeData
    {
        NumberOfBedrooms=6f,
        Price=600000f
    }
};
```

<span data-ttu-id="70db1-141">Normalisez les données en cellules à l’aide de la méthode [`NormalizeBinning`](xref:Microsoft.ML.NormalizationCatalog.NormalizeBinning*).</span><span class="sxs-lookup"><span data-stu-id="70db1-141">Normalize the data into bins using the [`NormalizeBinning`](xref:Microsoft.ML.NormalizationCatalog.NormalizeBinning*) method.</span></span> <span data-ttu-id="70db1-142">Le paramètre `maximumBinCount` vous permet de spécifier le nombre de cellules nécessaires pour classifier vos données.</span><span class="sxs-lookup"><span data-stu-id="70db1-142">The `maximumBinCount` parameter enables you to specify the number of bins needed to classify your data.</span></span> <span data-ttu-id="70db1-143">Dans cet exemple, les données sont placées dans deux cellules.</span><span class="sxs-lookup"><span data-stu-id="70db1-143">In this example, data will be put into two bins.</span></span>  

```csharp
// Define binning estimator
var binningEstimator = mlContext.Transforms.NormalizeBinning("Price", maximumBinCount: 2);

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
var binningTransformer = binningEstimator.Fit(data);

// Transform Data
IDataView transformedData = binningTransformer.Transform(data);
```

<span data-ttu-id="70db1-144">La quantification crée des bornes de cellule de `[0,200000,Infinity]`.</span><span class="sxs-lookup"><span data-stu-id="70db1-144">The result of binning creates bin bounds of `[0,200000,Infinity]`.</span></span> <span data-ttu-id="70db1-145">Ainsi, les cellules obtenues sont `[0,1,1]`, car la première observation est comprise entre 0 et 200 000, et les autres sont supérieures à 200 000 mais inférieures à l’infini.</span><span class="sxs-lookup"><span data-stu-id="70db1-145">Therefore the resulting bins are `[0,1,1]` because the first observation is between 0-200000 and the others are greater than 200000 but less than infinity.</span></span>

## <a name="work-with-categorical-data"></a><span data-ttu-id="70db1-146">Utiliser des données de catégorie</span><span class="sxs-lookup"><span data-stu-id="70db1-146">Work with categorical data</span></span>

<span data-ttu-id="70db1-147">Les données de catégorie non numériques doivent être converties en nombre avant d’être utilisées pour générer un modèle Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="70db1-147">Non-numeric categorical data needs to be converted to a number before being used to build a machine learning model.</span></span> 

<span data-ttu-id="70db1-148">Supposons que nous utilisons les données d’entrée suivantes qui sont chargées dans un [`IDataView`](xref:Microsoft.ML.IDataView) :</span><span class="sxs-lookup"><span data-stu-id="70db1-148">Using the following input data which is loaded into an [`IDataView`](xref:Microsoft.ML.IDataView):</span></span>

```csharp
CarData[] cars = new CarData[] 
{
    new CarData
    {
        Color="Red",
        VehicleType="SUV"
    },
    new CarData
    {
        Color="Blue",
        VehicleType="Sedan"
    },
    new CarData
    {
        Color="Black",
        VehicleType="SUV"
    }
};
```

<span data-ttu-id="70db1-149">La propriété `VehicleType` de catégorie peut être convertie en un nombre à l’aide de la méthode [`OneHotEncoding`](xref:Microsoft.ML.CategoricalCatalog.OneHotEncoding*).</span><span class="sxs-lookup"><span data-stu-id="70db1-149">The categorical `VehicleType` property can be converted into a number using the [`OneHotEncoding`](xref:Microsoft.ML.CategoricalCatalog.OneHotEncoding*) method.</span></span> 

```csharp
// Define categorical transform estimator
var categoricalEstimator = mlContext.Transforms.Categorical.OneHotEncoding("VehicleType");

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
ITransformer categoricalTransformer = categoricalEstimator.Fit(data);

// Transform Data
IDataView transformedData = categoricalTransformer.Transform(data);
```

<span data-ttu-id="70db1-150">La transformation qui en résulte convertit la valeur de texte de `VehicleType` en un nombre.</span><span class="sxs-lookup"><span data-stu-id="70db1-150">The resulting transform converts the text value of `VehicleType` to a number.</span></span> <span data-ttu-id="70db1-151">Les entrées de la colonne `VehicleType` deviennent les suivantes quand la transformation est appliquée :</span><span class="sxs-lookup"><span data-stu-id="70db1-151">The entries in the `VehicleType` column become the following when the transform is applied:</span></span> 

```text
[
    1, // SUV
    2, // Sedan
    1 // SUV
]
```

## <a name="work-with-text-data"></a><span data-ttu-id="70db1-152">Utiliser des données texte</span><span class="sxs-lookup"><span data-stu-id="70db1-152">Work with text data</span></span>

<span data-ttu-id="70db1-153">Les données texte doivent être transformées en nombres avant d’être utilisées pour générer un modèle Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="70db1-153">Text data needs to be transformed into numbers before using it to build a machine learning model.</span></span> <span data-ttu-id="70db1-154">Consultez la [page sur les transformations](../resources/transforms.md) pour obtenir une liste et une description plus détaillées des transformations de texte.</span><span class="sxs-lookup"><span data-stu-id="70db1-154">Visit the [transforms page](../resources/transforms.md) for a more detailed list and description of text transforms.</span></span>

<span data-ttu-id="70db1-155">Supposons que nous utilisons des données telles que celles ci-dessous qui ont été chargées dans un [`IDataView`](xref:Microsoft.ML.IDataView) :</span><span class="sxs-lookup"><span data-stu-id="70db1-155">Using data like the data below that has been loaded into an [`IDataView`](xref:Microsoft.ML.IDataView):</span></span>

```csharp
ReviewData[] reviews = new ReviewData[]
{
    new ReviewData
    {
        Description="This is a good product",
        Rating=4.7f
    },
    new ReviewData
    {
        Description="This is a bad product",
        Rating=2.3f
    }
};
```

<span data-ttu-id="70db1-156">L’étape minimale pour convertir du texte en une représentation sous forme de vecteur numérique consiste à utiliser la méthode [`FeaturizeText`](xref:Microsoft.ML.TextCatalog.FeaturizeText*).</span><span class="sxs-lookup"><span data-stu-id="70db1-156">The minimum step to convert text to a numerical vector representation is to use the [`FeaturizeText`](xref:Microsoft.ML.TextCatalog.FeaturizeText*) method.</span></span> <span data-ttu-id="70db1-157">À l’aide de la transformation [`FeaturizeText`](xref:Microsoft.ML.TextCatalog.FeaturizeText*), une série de transformations est appliquée à la colonne de texte d’entrée, ce qui engendre un vecteur numérique représentant les n-grammes de mot et de caractère à la norme IP.</span><span class="sxs-lookup"><span data-stu-id="70db1-157">By using the [`FeaturizeText`](xref:Microsoft.ML.TextCatalog.FeaturizeText*) transform, a series of transformations is applied to the input text column resulting in a numerical vector representing the lp-normalized word and character ngrams.</span></span> 

```csharp
// Define text transform estimator
var textEstimator  = mlContext.Transforms.Text.FeaturizeText("Description");

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
ITransformer textTransformer = textEstimator.Fit(data);

// Transform data
IDataView transformedData = textTransformer.Transform(data);
```

<span data-ttu-id="70db1-158">La transformation qui en résulte convertit les valeurs de texte dans la colonne `Description` en un vecteur numérique qui ressemble à la sortie ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="70db1-158">The resulting transform would convert the text values in the `Description` column to a numerical vector that looks similar to the output below:</span></span>

```text
[ 0.2041241, 0.2041241, 0.2041241, 0.4082483, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0, 0, 0, 0, 0.4472136, 0.4472136, 0.4472136, 0.4472136, 0.4472136, 0 ]
```

<span data-ttu-id="70db1-159">Vous pouvez combiner des étapes de traitement de texte complexes en un [`EstimatorChain`](xref:Microsoft.ML.Data.EstimatorChain%601) pour supprimer le bruit et potentiellement réduire la quantité de ressources de traitement requises.</span><span class="sxs-lookup"><span data-stu-id="70db1-159">Combine complex text processing steps into an [`EstimatorChain`](xref:Microsoft.ML.Data.EstimatorChain%601) to remove noise and potentially reduce the amount of required processing resources as needed.</span></span>

```csharp
// Define text transform estimator
var textEstimator = mlContext.Transforms.Text.NormalizeText("Description")
    .Append(mlContext.Transforms.Text.TokenizeIntoWords("Description"))
    .Append(mlContext.Transforms.Text.RemoveDefaultStopWords("Description"))
    .Append(mlContext.Transforms.Conversion.MapValueToKey("Description"))
    .Append(mlContext.Transforms.Text.ProduceNgrams("Description"))
    .Append(mlContext.Transforms.NormalizeLpNorm("Description"));
```

<span data-ttu-id="70db1-160">`textEstimator` contient un sous-ensemble des opérations effectuées par la méthode [`FeaturizeText`](xref:Microsoft.ML.TextCatalog.FeaturizeText*).</span><span class="sxs-lookup"><span data-stu-id="70db1-160">`textEstimator` contains a subset of operations performed by the [`FeaturizeText`](xref:Microsoft.ML.TextCatalog.FeaturizeText*) method.</span></span> <span data-ttu-id="70db1-161">L’avantage d’un pipeline plus complexe est qu’il procure une visibilité et un contrôle des transformations appliquées aux données.</span><span class="sxs-lookup"><span data-stu-id="70db1-161">The benefit of a more complex pipeline is control and visibility over the transformations applied to the data.</span></span> 

<span data-ttu-id="70db1-162">Si, par exemple, nous utilisons la première entrée, voici une description détaillée des résultats produits par les étapes de transformation définies par `textEstimator` :</span><span class="sxs-lookup"><span data-stu-id="70db1-162">Using the first entry as an example, the following is a detailed description of the results produced by the transformation steps defined by `textEstimator`:</span></span>

<span data-ttu-id="70db1-163">**Texte d’origine : This is a good product**</span><span class="sxs-lookup"><span data-stu-id="70db1-163">**Original Text: This is a good product**</span></span>

|<span data-ttu-id="70db1-164">Transformer</span><span class="sxs-lookup"><span data-stu-id="70db1-164">Transform</span></span> | <span data-ttu-id="70db1-165">Description</span><span class="sxs-lookup"><span data-stu-id="70db1-165">Description</span></span> | <span data-ttu-id="70db1-166">Résultat</span><span class="sxs-lookup"><span data-stu-id="70db1-166">Result</span></span>
|--|--|--|
|<span data-ttu-id="70db1-167">1. NormalizeText</span><span class="sxs-lookup"><span data-stu-id="70db1-167">1. NormalizeText</span></span> | <span data-ttu-id="70db1-168">Convertit toutes les lettres en minuscules par défaut</span><span class="sxs-lookup"><span data-stu-id="70db1-168">Converts all letters to lowercase by default</span></span> | <span data-ttu-id="70db1-169">this is a good product</span><span class="sxs-lookup"><span data-stu-id="70db1-169">this is a good product</span></span>
|<span data-ttu-id="70db1-170">2. TokenizeWords</span><span class="sxs-lookup"><span data-stu-id="70db1-170">2. TokenizeWords</span></span> | <span data-ttu-id="70db1-171">Fractionne la chaîne en mots individuels</span><span class="sxs-lookup"><span data-stu-id="70db1-171">Splits string into individual words</span></span> | <span data-ttu-id="70db1-172">["this","is","a","good","product"]</span><span class="sxs-lookup"><span data-stu-id="70db1-172">["this","is","a","good","product"]</span></span>
|<span data-ttu-id="70db1-173">3. RemoveDefaultStopWords</span><span class="sxs-lookup"><span data-stu-id="70db1-173">3. RemoveDefaultStopWords</span></span> | <span data-ttu-id="70db1-174">Supprime les mots vides comme *is* et *a*.</span><span class="sxs-lookup"><span data-stu-id="70db1-174">Removes stopwords like *is* and *a*.</span></span> | <span data-ttu-id="70db1-175">["good","product"]</span><span class="sxs-lookup"><span data-stu-id="70db1-175">["good","product"]</span></span>
|<span data-ttu-id="70db1-176">4. MapValueToKey</span><span class="sxs-lookup"><span data-stu-id="70db1-176">4. MapValueToKey</span></span> | <span data-ttu-id="70db1-177">Mappe les valeurs sur des clés (catégories) en fonction des données d’entrée</span><span class="sxs-lookup"><span data-stu-id="70db1-177">Maps the values to keys (categories) based on the input data</span></span> |  <span data-ttu-id="70db1-178">[1,2]</span><span class="sxs-lookup"><span data-stu-id="70db1-178">[1,2]</span></span>
|<span data-ttu-id="70db1-179">5. ProduceNGrams</span><span class="sxs-lookup"><span data-stu-id="70db1-179">5. ProduceNGrams</span></span> | <span data-ttu-id="70db1-180">Transforme le texte en une séquence de mots consécutifs</span><span class="sxs-lookup"><span data-stu-id="70db1-180">Transforms text into sequence of consecutive words</span></span> | <span data-ttu-id="70db1-181">[1,1,1,0,0]</span><span class="sxs-lookup"><span data-stu-id="70db1-181">[1,1,1,0,0]</span></span>
|<span data-ttu-id="70db1-182">6. NormalizeLpNorm</span><span class="sxs-lookup"><span data-stu-id="70db1-182">6. NormalizeLpNorm</span></span> | <span data-ttu-id="70db1-183">Applique une mise à l’échelle aux entrées d’après leur norme IP</span><span class="sxs-lookup"><span data-stu-id="70db1-183">Scale inputs by their lp-norm</span></span> | <span data-ttu-id="70db1-184">[ 0.577350529, 0.577350529, 0.577350529, 0, 0 ]</span><span class="sxs-lookup"><span data-stu-id="70db1-184">[ 0.577350529, 0.577350529, 0.577350529, 0, 0 ]</span></span>