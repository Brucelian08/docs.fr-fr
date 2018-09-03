---
title: '&lt;ajouter&gt; élément pour &lt;schemaImporterExtensions&gt;'
ms.date: 03/30/2017
helpviewer_keywords:
- XML serialization, configuration
- <add> element for <schemaImporterExtensions> element
ms.assetid: c828a558-094b-441e-9065-790b87315fa0
ms.openlocfilehash: 3d3c72fd64042032d44c49ebde867d111ce03b94
ms.sourcegitcommit: efff8f331fd9467f093f8ab8d23a203d6ecb5b60
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/01/2018
ms.locfileid: "43453087"
---
# <a name="ltaddgt-element-for-ltschemaimporterextensionsgt"></a><span data-ttu-id="79877-102">&lt;ajouter&gt; élément pour &lt;schemaImporterExtensions&gt;</span><span class="sxs-lookup"><span data-stu-id="79877-102">&lt;add&gt; Element for &lt;schemaImporterExtensions&gt;</span></span>
<span data-ttu-id="79877-103">Ajoute des types utilisés par <xref:System.Xml.Serialization.XmlSchemaImporter> pour mapper des types XSD en types .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="79877-103">Adds types used by the <xref:System.Xml.Serialization.XmlSchemaImporter> for mapping XSD types to .NET Framework types.</span></span> <span data-ttu-id="79877-104">Pour plus d’informations sur les fichiers de configuration, consultez [Schéma des fichiers de configuration](../../../docs/framework/configure-apps/file-schema/index.md).</span><span class="sxs-lookup"><span data-stu-id="79877-104">For more information about configuration files, see [Configuration File Schema](../../../docs/framework/configure-apps/file-schema/index.md).</span></span>  
  
 <span data-ttu-id="79877-105">\<configuration></span><span class="sxs-lookup"><span data-stu-id="79877-105">\<configuration></span></span>  
<span data-ttu-id="79877-106">\<system.xml.serialization></span><span class="sxs-lookup"><span data-stu-id="79877-106">\<system.xml.serialization></span></span>  
<span data-ttu-id="79877-107">\<schemaImporterExtensions></span><span class="sxs-lookup"><span data-stu-id="79877-107">\<schemaImporterExtensions></span></span>  
<span data-ttu-id="79877-108">\<add></span><span class="sxs-lookup"><span data-stu-id="79877-108">\<add></span></span>  
  
## <a name="syntax"></a><span data-ttu-id="79877-109">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="79877-109">Syntax</span></span>  
  
```xml  
<add name = "typeName" type="fully qualified type [,Version=version number] [,Culture=culture] [,PublicKeyToken= token]"/>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="79877-110">Attributs et éléments</span><span class="sxs-lookup"><span data-stu-id="79877-110">Attributes and Elements</span></span>  
 <span data-ttu-id="79877-111">Les sections suivantes décrivent des attributs, des éléments enfants et des éléments parents.</span><span class="sxs-lookup"><span data-stu-id="79877-111">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="79877-112">Attributs</span><span class="sxs-lookup"><span data-stu-id="79877-112">Attributes</span></span>  
  
|<span data-ttu-id="79877-113">Attribut</span><span class="sxs-lookup"><span data-stu-id="79877-113">Attribute</span></span>|<span data-ttu-id="79877-114">Description</span><span class="sxs-lookup"><span data-stu-id="79877-114">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="79877-115">**name**</span><span class="sxs-lookup"><span data-stu-id="79877-115">**name**</span></span>|<span data-ttu-id="79877-116">Nom simple utilisé pour rechercher l'instance.</span><span class="sxs-lookup"><span data-stu-id="79877-116">A simple name that is used to find the instance.</span></span>|  
|<span data-ttu-id="79877-117">**type**</span><span class="sxs-lookup"><span data-stu-id="79877-117">**type**</span></span>|<span data-ttu-id="79877-118">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="79877-118">Required.</span></span> <span data-ttu-id="79877-119">Spécifie la classe d'extension de schéma à ajouter.</span><span class="sxs-lookup"><span data-stu-id="79877-119">Specifies the schema  extension class to add.</span></span> <span data-ttu-id="79877-120">La valeur d’attribut **type** doit figurer sur une ligne et inclure le nom complet du type.</span><span class="sxs-lookup"><span data-stu-id="79877-120">The **type** attribute value must be on one line, and include the fully qualified type name.</span></span> <span data-ttu-id="79877-121">Lorsque l'assembly est placé dans le Global Assembly Cache (GAC), il doit également inclure la version, la culture et le jeton de clé publique de l'assembly signé.</span><span class="sxs-lookup"><span data-stu-id="79877-121">When the assembly is placed in the Global Assembly Cache (GAC), it must also include the version, culture, and public key token of the signed assembly.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="79877-122">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="79877-122">Child Elements</span></span>  
 <span data-ttu-id="79877-123">Aucun.</span><span class="sxs-lookup"><span data-stu-id="79877-123">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="79877-124">Éléments parents</span><span class="sxs-lookup"><span data-stu-id="79877-124">Parent Elements</span></span>  
  
|<span data-ttu-id="79877-125">Élément</span><span class="sxs-lookup"><span data-stu-id="79877-125">Element</span></span>|<span data-ttu-id="79877-126">Description</span><span class="sxs-lookup"><span data-stu-id="79877-126">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="79877-127">\<schemaImporterExtensions></span><span class="sxs-lookup"><span data-stu-id="79877-127">\<schemaImporterExtensions></span></span>|<span data-ttu-id="79877-128">Contient les types utilisés par <xref:System.Xml.Serialization.XmlSchemaImporter>.</span><span class="sxs-lookup"><span data-stu-id="79877-128">Contains the types that are used by the <xref:System.Xml.Serialization.XmlSchemaImporter>.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="79877-129">Exemple</span><span class="sxs-lookup"><span data-stu-id="79877-129">Example</span></span>  
 <span data-ttu-id="79877-130">L'exemple de code suivant ajoute un type d'extension que XmlSchemaImporter peut utiliser lors du mappage de types.</span><span class="sxs-lookup"><span data-stu-id="79877-130">The following code example adds an extension type that the XmlSchemaImporter can use when mapping types.</span></span>  
  
```xml  
<configuration>  
  <system.xml.serialization>  
    <schemaImporterExtensions>  
       <add name="contoso" type="System.Web.Mobile.MobileCapabilities,   
       System.Web.Mobile, Version=2.0.0.0, Culture=neutral,   
       PublicKeyToken=b03f5f7f11d50a3a" />   
    </schemaImporterExtensions>  
  </system.xml.serialization>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="79877-131">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="79877-131">See Also</span></span>  
 <xref:System.Xml.Serialization.XmlSchemaImporter>  
 [<span data-ttu-id="79877-132">\<system.xml.serialization>, élément</span><span class="sxs-lookup"><span data-stu-id="79877-132">\<system.xml.serialization> Element</span></span>](../../../docs/standard/serialization/system-xml-serialization-element.md)  
 [<span data-ttu-id="79877-133">\<schemaImporterExtensions>, élément</span><span class="sxs-lookup"><span data-stu-id="79877-133">\<schemaImporterExtensions> Element</span></span>](../../../docs/standard/serialization/schemaimporterextensions-element.md)