---
title: Asignaciones de tipos personalizadas entre SQL y CLR
ms.date: 03/30/2017
ms.assetid: d916c7fb-4b56-4214-acbe-5e23365047b2
ms.openlocfilehash: bc92d54cad6a977268ef3f000c684d5f195a933d
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59140418"
---
# <a name="sql-clr-custom-type-mappings"></a>Asignaciones de tipos personalizadas entre SQL y CLR
La asignación de tipos entre SQL Server y Common Language Runtime (CLR) se especifica automáticamente al usar la herramienta de línea de comandos SQLMetal, Object Relational Designer.  
  
 Cuando no se realiza ninguna asignación personalizada, estas herramientas asignan predeterminada asignaciones de tipos como se describe en [asignación de tipos SQL-CLR](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md). Si desea que las asignaciones de tipos sean distintas de las predeterminadas, tendrá que hacer alguna personalización de ellas.  
  
 Al personalizar las asignaciones de tipos, el enfoque recomendado es realizar los cambios en un archivo DBML intermedio. Después, el archivo DBML personalizado se debe usar al crear los archivos de código y de asignación con SQLMetal u Object Relational Designer.  
  
 Una vez creada una instancia del objeto <xref:System.Data.Linq.DataContext> desde los archivos de código y de asignación, el método <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> crea una base de datos basándose en las asignaciones de tipos especificadas. Si no hay atributos `type` de CLR especificados en las asignaciones, se usarán las asignaciones de tipos predeterminadas.  
  
## <a name="customization-with-sqlmetal-or-or-designer"></a>Personalización con SQLMetal o con Object Relational Designer  
 Con SQLMetal o con Object Relational Designer puede crear automáticamente un modelo de objetos que incluye información de asignación dentro o fuera del archivo de código. Dado que SQLMetal o con Object Relational Designer sobrescribe estos archivos, cada vez que vuelve a crear las asignaciones, el método recomendado para especificar las asignaciones de tipos personalizadas es personalizar un archivo DBML.  
  
 Para personalizar las asignaciones de tipos con SQLMetal o con Object Relational Designer, primero genere un archivo DBML. Luego, antes de generar el archivo de código o el archivo de asignación, modifique el archivo DBML para identificar las asignaciones de tipos deseadas. Con SQLMetal, tiene que cambiar manualmente los atributos `Type` y `DbType` del archivo DBML para hacer las personalizaciones de asignación de tipos. Con Object Relational Designer, puede hacer los cambios en el Diseñador. Para obtener más información sobre cómo usar el Object Relational Designer, vea [LINQ to SQL Tools en Visual Studio](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2).  
  
> [!NOTE]
>  Algunas asignaciones de tipos pueden tener como resultado excepciones de desbordamiento o de pérdida de datos mientras se convierten a la base de datos o desde ella. Revise cuidadosamente la matriz de comportamiento de tiempo de ejecución de asignación de tipos en [asignación de tipos de CLR de SQL](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md) antes de realizar las personalizaciones.  
  
 Para que SQLMetal o bien Object Relational Designer reconozcan las personalizaciones de asignación de tipos, tiene que asegurarse de que estas herramientas se proporcionan con la ruta de acceso del archivo DBML personalizado al generar el archivo de código o el archivo de asignación externa. Aunque no es necesario para la personalización de la asignación de tipos, se recomienda que siempre separe la información de asignación de tipos del archivo de código y genere el archivo de asignación de tipos externa adicional. Con esto permitirá alguna flexibilidad al no necesitar que se recompile el archivo de código.  
  
## <a name="incorporating-database-changes"></a>Incorporación de cambios en la base de datos  
 Cuando la base de datos cambia, tendrá que actualizar el archivo DBML para reflejar esos cambios. Uno modo de hacer esto es crear automáticamente un archivo DBML nuevo y, a continuación, volver a efectuar las personalizaciones de asignación de tipos. Como alternativa, podría comparar las diferencias entre el archivo DBML nuevo y el archivo DBML personalizado y actualizar el archivo DBML personalizado para reflejar el cambio en la base de datos.  
  
## <a name="see-also"></a>Vea también

- [Asignación de tipos entre CLR y SQL](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)
- [Generación de código en LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md)
