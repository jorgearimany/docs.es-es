---
title: Extensibilidad de la distribución
ms.date: 03/30/2017
ms.assetid: 4d941175-74a2-4b15-81b3-086e8a95d25f
ms.openlocfilehash: 226ea682d8b17a818e6d5be2097a19315d106bda
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59170812"
---
# <a name="syndication-extensibility"></a>Extensibilidad de la distribución
La API de distribución está diseñada para proporcionar un modelo de programación neutral frente al formato que permita escribir el contenido distribuido en la conexión en una variedad de formatos. El modelo de datos abstracto está compuesto por las siguientes clases:  
  
-   <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
 Estas clases asignan estrechamente a las estructuras definidas en la especificación Atom 1.0, aunque algunos de los nombres son diferentes.  
  
 Una característica clave de los protocolos de distribución es la extensibilidad. Atom 1.0 y RSS 2.0 agregan atributos y elementos a las fuentes de distribución que no están definidas en las especificaciones. El modelo de programación de distribución de Windows Communication Foundation (WCF) proporciona las siguientes formas de trabajar con atributos personalizados y extensiones, acceso fuertemente tipado y derivar una clase nueva.  
  
## <a name="loosely-typed-access"></a>Access escrito de manera imprecisa  
 Para agregar extensiones derivando una nueva clase, es necesario escribir código adicional. Otra opción obtener acceso a extensiones de manera imprecisa. Todos los tipos definidos en el modelo de datos abstracto de distribución contienen propiedades denominadas `AttributeExtensions` y `ElementExtensions` (con una excepción, <xref:System.ServiceModel.Syndication.SyndicationContent> tiene una propiedad `AttributeExtensions` pero ninguna propiedad `ElementExtensions`). Estas propiedades son colecciones de extensiones no procesadas por los métodos `TryParseAttribute` y `TryParseElement`, respectivamente. Puede tener acceso a estas extensiones no procesadas llamando al método <xref:System.ServiceModel.Syndication.SyndicationElementExtensionCollection.ReadElementExtensions%2A?displayProperty=nameWithType> de la propiedad `ElementExtensions` de <xref:System.ServiceModel.Syndication.SyndicationFeed>, <xref:System.ServiceModel.Syndication.SyndicationItem>, <xref:System.ServiceModel.Syndication.SyndicationLink>, <xref:System.ServiceModel.Syndication.SyndicationPerson>y <xref:System.ServiceModel.Syndication.SyndicationCategory>. Este conjunto de métodos encuentra todas las extensiones con el nombre y espacio de nombres especificado, las deserializa individualmente en instancias de `TExtension` y las devuelve como una colección de objetos `TExtension`.  
  
## <a name="deriving-a-new-class"></a>Derivación de una nueva clase  
 Puede derivar una nueva clase de cualquiera de las clases del modelo de datos abstracto existentes. Haga esto al implementar una aplicación en la que la mayoría de las fuentes con las que está trabajando tienen una extensión determinada. En este tema, la mayoría de las fuentes con las que el programa trabaja contienen una extensión `MyExtension`. Para proporcionar una experiencia de programación mejorada, realice los siguientes pasos:  
  
-   Cree una clase para retener los datos de las extensión. En este caso, cree una clase llamada MyExtension.  
  
-   Derive una clase llamada MyExtensionItem desde <xref:System.ServiceModel.Syndication.SyndicationItem> para exponer una propiedad de tipo MyExtension a efectos de la capacidad de programación.  
  
-   Invalide <xref:System.ServiceModel.Syndication.SyndicationItem.TryParseElement%28System.Xml.XmlReader%2CSystem.String%29> en la clase MyExtensionItem para crear instancias de una nueva instancia de MyExtension cuando se lee una MyExtension.  
  
-   Invalide <xref:System.ServiceModel.Syndication.SyndicationItem.WriteElementExtensions%28System.Xml.XmlWriter%2CSystem.String%29> en la clase MyExtensionItem para escribir el contenido de la propiedad MyExtension en un sistema de escritura de XML.  
  
-   Derive una clase llamada MyExtensionFeed desde <xref:System.ServiceModel.Syndication.SyndicationFeed>.  
  
-   Invalide <xref:System.ServiceModel.Syndication.SyndicationFeed.CreateItem> en la clase MyExtensionFeed para crear instancias de MyExtensionItem en lugar del <xref:System.ServiceModel.Syndication.SyndicationItem>predeterminado. Una serie de métodos se define en <xref:System.ServiceModel.Syndication.SyndicationFeed> y <xref:System.ServiceModel.Syndication.SyndicationItem> que pueden crear <xref:System.ServiceModel.Syndication.SyndicationLink>, <xref:System.ServiceModel.Syndication.SyndicationCategory>y objetos <xref:System.ServiceModel.Syndication.SyndicationPerson> (por ejemplo, <xref:System.ServiceModel.Syndication.SyndicationFeed.CreateLink>, <xref:System.ServiceModel.Syndication.SyndicationFeed.CreateCategory>y <xref:System.ServiceModel.Syndication.SyndicationFeed.CreatePerson>). Todos los cuales se puede invalidar para crear una clase derivada personalizada.  
  
## <a name="see-also"></a>Vea también

- [Información general de redifusión en WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md)
- [Arquitectura de redifusión](../../../../docs/framework/wcf/feature-details/architecture-of-syndication.md)
