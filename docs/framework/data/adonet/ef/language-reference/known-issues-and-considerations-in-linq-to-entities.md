---
title: Problemas conocidos y consideraciones en LINQ to Entities
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: acd71129-5ff0-4b4e-b266-c72cc0c53601
ms.openlocfilehash: 3945d4fc92bea2c4212da0507618203603ae8aba
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59191333"
---
# <a name="known-issues-and-considerations-in-linq-to-entities"></a>Problemas conocidos y consideraciones en LINQ to Entities
En esta sección se ofrece información sobre los problemas conocidos relacionados con las consultas de [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)].  
  
-   [Consultas LINQ que no se puede almacenar en caché](#LINQQueriesThatAreNotCached)  
  
-   [Pérdida de información de ordenación](#OrderingInfoLost)  
  
-   [Enteros sin signo no admitidos](#UnsignedIntsUnsupported)  
  
-   [Errores de conversión de tipo](#TypeConversionErrors)  
  
-   [Hacer referencia a Variables no escalares no admitidas](#RefNonScalarClosures)  
  
-   [Pueden producir un error de las consultas anidadas con SQL Server 2000](#NestedQueriesSQL2000)  
  
-   [Proyectar un tipo anónimo](#ProjectToAnonymousType)  
  
<a name="LINQQueriesThatAreNotCached"></a>   
## <a name="linq-queries-that-cannot-be-cached"></a>Consultas LINQ que no se pueden almacenar en memoria caché  
 A partir de .NET Framework 4.0.5, las consultas LINQ to Entities se almacenan automáticamente en memoria caché. Sin embargo, as consultas LINQ to Entities que aplican el operador `Enumerable.Contains` a colecciones en memoria no se almacenan en memoria caché automáticamente. Tampoco se permite parametrizar colecciones en memoria en consultas LINQ compiladas.  
  
<a name="OrderingInfoLost"></a>   
## <a name="ordering-information-lost"></a>Pérdida de información de ordenación  
 La proyección de columnas en un tipo anónimo provocará la pérdida de información de ordenación en algunas consultas que se ejecuten en un conjunto de base de datos de [!INCLUDE[ssVersion2005](../../../../../../includes/ssversion2005-md.md)] con un nivel de la compatibilidad de "80".  Esto se produce cuando un nombre de columna en la lista ORDER BY coincide con un nombre de columna en el selector, como se muestra en el ejemplo siguiente:  
  
 [!code-csharp[DP L2E Conceptual Examples#SBUDT543840](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#sbudt543840)]
 [!code-vb[DP L2E Conceptual Examples#SBUDT543840](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#sbudt543840)]  
  
<a name="UnsignedIntsUnsupported"></a>   
## <a name="unsigned-integers-not-supported"></a>Enteros sin signo no admitidos  
 La especificación de un tipo entero sin signo en una consulta de [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] no se admite porque [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] no admite enteros sin signo. Si especifica un entero sin signo, un <xref:System.ArgumentException> excepción se producirá durante la conversión de expresión de consulta, como se muestra en el ejemplo siguiente. En este ejemplo se consulta un pedido cuyo número de identificación (Id.) es 48000.  
  
 [!code-csharp[DP L2E Conceptual Examples#UIntAsQueryParam](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#uintasqueryparam)]
 [!code-vb[DP L2E Conceptual Examples#UIntAsQueryParam](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#uintasqueryparam)]  
  
<a name="TypeConversionErrors"></a>   
## <a name="type-conversion-errors"></a>Errores de la conversión de tipos  
 En Visual Basic, cuando se asigna una propiedad a una columna de tipo bit de SQL Server con un valor de 1 utilizando la función `CByte`, se produce una excepción <xref:System.Data.SqlClient.SqlException> con el mensaje "Error de desbordamiento aritmético". En el ejemplo siguiente se consulta la columna `Product.MakeFlag` en la base de datos de ejemplo AdventureWorks y se produce una excepción cuando tiene lugar una iteración en los resultados de la consulta.  
  
 [!code-vb[DP L2E Conceptual Examples#SBUDT544355](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#sbudt544355)]  
  
<a name="RefNonScalarClosures"></a>   
## <a name="referencing-non-scalar-variables-not-supported"></a>Referencia a variables no escalares no admitida  
 En una consulta no se puede hacer referencia a variables no escalares, tales como una entidad. Cuando este tipo de consulta se ejecuta, se genera una excepción <xref:System.NotSupportedException> con un mensaje que indica "No se puede crear un valor constante de tipo `EntityType`". Sólo los tipos primitivos ('como Int32, String y Guid') se admiten en este contexto.".  
  
> [!NOTE]
>  Permite hacer referencia a una colección de variables escalares.  
  
 [!code-csharp[DP L2E Conceptual Examples#SBUDT555877](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#sbudt555877)]
 [!code-vb[DP L2E Conceptual Examples#SBUDT555877](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#sbudt555877)]  
  
<a name="NestedQueriesSQL2000"></a>   
## <a name="nested-queries-may-fail-with-sql-server-2000"></a>Se puede producir un error en consultas anidadas con SQL Server 2000  
 Con SQL Server 2000, se puede producir un error en consultas LINQ to Entities si se generan consultas Transact-SQL anidadas con tres o más niveles de profundidad.  
  
<a name="ProjectToAnonymousType"></a>   
## <a name="projecting-to-an-anonymous-type"></a>Proyectar a un tipo anónimo  
 Si define su ruta de acceso de consultas inicial para incluir objetos relacionados utilizando el método <xref:System.Data.Objects.ObjectQuery%601.Include%2A> sobre <xref:System.Data.Objects.ObjectQuery%601> y, a continuación, utiliza LINQ para proyectar los objetos devueltos sobre un tipo anónimo, los objetos especificados en el método de inclusión no se incluyen en los resultados de la consulta.  
  
 [!code-csharp[DP L2E Conceptual Examples#ProjToAnonType1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#projtoanontype1)]
 [!code-vb[DP L2E Conceptual Examples#ProjToAnonType1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#projtoanontype1)]  
  
 Para obtener objetos relacionados, no proyecte los tipos devueltos sobre un tipo anónimo.  
  
 [!code-csharp[DP L2E Conceptual Examples#ProjToAnonType2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#projtoanontype2)]
 [!code-vb[DP L2E Conceptual Examples#ProjToAnonType2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#projtoanontype2)]  
  
## <a name="see-also"></a>Vea también

- [LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md)
