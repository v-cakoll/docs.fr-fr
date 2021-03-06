---
title: Conversion des types de données XML
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: a2aa99ba-8239-4818-9281-f1d72ee40bde
ms.openlocfilehash: d8b60428bc129958355ce5b285662847e9e712c3
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84282413"
---
# <a name="conversion-of-xml-data-types"></a>Conversion des types de données XML
La majorité des méthodes présentes dans une classe **XmlConvert** sont utilisées pour convertir des données entre des chaînes et des formats fortement typés. Ces méthodes sont indépendantes des paramètres régionaux. Cela signifie qu'elles ne prennent pas en compte les paramètres régionaux éventuels lors de la conversion.  
  
## <a name="reading-string-as-types"></a>Lecture de chaînes comme des types  
 L'exemple suivant lit une chaîne et la convertit en type **DateTime**.  
  
 En supposant l'entrée XML suivante :  
  
 **Input**  
  
```xml  
<Element>2001-02-27T11:13:23</Element>  
```  
  
 Ce code convertit la chaîne au format **DateTime** :  
  
```vb  
reader.ReadStartElement()  
Dim vDateTime As DateTime = XmlConvert.ToDateTime(reader.ReadString())  
Console.WriteLine(vDateTime)  
```  
  
```csharp  
reader.ReadStartElement();  
DateTime vDateTime = XmlConvert.ToDateTime(reader.ReadString());  
Console.WriteLine(vDateTime);  
```  
  
## <a name="writing-strings-as-types"></a>Écriture de chaînes comme des types  
 L'exemple suivant lit un type **Int32** et le convertit en chaîne.  
  
 En supposant l'entrée XML suivante :  
  
 **Input**  
  
```xml  
<TestInt32>-2147483648</TestInt32>  
```  
  
 Ce code convertit le type **Int32** en type **String**:  
  
```vb  
Dim vInt32 As Int32 = -2147483648  
writer.WriteElementString("TestInt32", XmlConvert.ToString(vInt32))  
```  
  
```csharp  
Int32 vInt32=-2147483648;  
writer.WriteElementString("TestInt32",XmlConvert.ToString(vInt32));  
```  
  
## <a name="see-also"></a>Voir aussi

- [Conversion de chaînes en types de données .NET Framework](converting-strings-to-dotnet-data-types.md)
- [Conversion de types .NET Framework en chaînes](converting-dotnet-types-to-strings.md)
