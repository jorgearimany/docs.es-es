---
title: Funciones canónicas bit a bit
ms.date: 03/30/2017
ms.assetid: 993868ca-16e3-47b6-9915-c29cd63b0a21
ms.openlocfilehash: 67d78e8d31f0bc3564a0a111b9bc71cbd0e14f5c
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59127808"
---
# <a name="bitwise-canonical-functions"></a>Funciones canónicas bit a bit
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] incluye funciones canónicas bit a bit.  
  
## <a name="remarks"></a>Comentarios  
 En la tabla siguiente se muestran las demás funciones canónicas de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] bit a bit. Estas funciones devolverán `Null` si `Null` la entrada se proporcionó. El tipo de valor devuelto de las funciones es igual que los tipos de argumento. Los argumentos deben ser del mismo tipo, si la función toma más de uno. Para llevar a cabo operaciones bit a bit en tipos diferentes, deberá convertir explícitamente al mismo tipo.  
  
|Función|Descripción|  
|--------------|-----------------|  
|`BitWiseAnd (` `value1` `,`  `value2` `)`|Devuelve la conjunción bit a bit de `value1` y `value2` como el tipo de `value1` y `value2`.<br /><br /> **Argumentos**<br /><br /> Un `Byte`, `Int16`, `Int32`, y `Int64`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns 1.`<br /><br /> `BitWiseAnd(1,3)`|  
|`BitWiseNot (` `value` `)`|Devuelve la negación bit a bit de `value`.<br /><br /> **Argumentos**<br /><br /> Un `Byte`, `Int16`, `Int32`, y `Int64`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns -4.`<br /><br /> `BitWiseNot(3)`|  
|`BitWiseOr (` `value1` `,`  `value2` `)`|Devuelve la disyunción bit a bit de `value1` y `value2` como el tipo de `value1` y `value2`.<br /><br /> **Argumentos**<br /><br /> Un `Byte`, `Int16`, `Int32` y `Int64`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns 3.`<br /><br /> `BitWiseOr(1,3)`|  
|`BitWiseXor (` `value1` `,`  `value2` `)`|Devuelve la disyunción exclusiva bit a bit de `value1` y `value2` como el tipo de `value1` y `value2`.<br /><br /> **Argumentos**<br /><br /> Un `Byte`, `Int16`, `Int32` y `Int64`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns 2.`<br /><br /> `BitWiseXor (1,3)`|  
  
## <a name="see-also"></a>Vea también

- [Funciones canónicas](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md)
