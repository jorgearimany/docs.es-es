---
ms.openlocfilehash: 566a3e0455b30e901b09be88b4256ffe67bdc2b5
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59236236"
---
### <a name="workflow-sql-persistence-adds-primary-key-clusters-and-disallows-null-values-in-some-columns"></a>La persistencia SQL de flujo de trabajo agrega clústeres de clave principal y no permite valores NULL en algunas columnas

|   |   |
|---|---|
|Detalles|A partir de .NET Framework 4.7, en las tablas creadas para el almacén de instancias de flujo de trabajo de SQL (SWIS) por el script SqlWorkflowInstanceStoreSchema.sql se usan claves principales en clúster. Por este motivo, las identidades no admiten valores <code>null</code>. El funcionamiento de SWIS no se ve afectado por este cambio. Las actualizaciones se realizaron para admitir la replicación transaccional de SQL Server.|
|Sugerencia|El archivo SQL SqlWorkflowInstanceStoreSchemaUpgrade.sql se debe aplicar a las instalaciones existentes con el fin de experimentar este cambio. Las nuevas instalaciones de base de datos tendrán automáticamente el cambio.|
|Ámbito|Borde|
|Versión|4.7|
|Tipo|Tiempo de ejecución|
