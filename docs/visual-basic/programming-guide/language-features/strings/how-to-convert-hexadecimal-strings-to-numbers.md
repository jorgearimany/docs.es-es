---
title: Procedimiento Convertir cadenas hexadecimales en números (Visual Basic)
ms.date: 01/31/2018
helpviewer_keywords:
- numbers [Visual Basic], hexadecimals
- hexadecimals [Visual Basic], decimals
- examples [Visual Basic], string conversion
- decimals [Visual Basic], hexadecimals
- string conversion [Visual Basic], hexadecimal to numbers
ms.assetid: 76675807-eadb-4c08-bd50-e6c6ff4b8ced
ms.openlocfilehash: ddb7b39f7a47234c003ca16e1d7ea013e113c108
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59773693"
---
# <a name="how-to-convert-hexadecimal-strings-to-numbers-visual-basic"></a>Procedimiento Convertir cadenas hexadecimales en números (Visual Basic)

En este ejemplo convierte una cadena hexadecimal en un entero con el <xref:System.Convert.ToInt32%2A?displayProperty=nameWithType> método.

## <a name="to-convert-a-hexadecimal-string-to-a-number"></a>Para convertir una cadena hexadecimal en un número

- Use el <xref:System.Convert.ToInt32(System.String,System.Int32)> método para convertir el número expresado en base 16 en un entero.

  El primer argumento de la <xref:System.Convert.ToInt32(System.String,System.Int32)> método es la cadena para convertir. El segundo argumento describe la base en que el número se expresa en; hexadecimal es base 16.

  [!code-vb[VbVbalrStrings#62](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#62)]

- Tenga en cuenta que la cadena hexadecimal tiene las siguientes restricciones:

  - No puede incluir el `&h` prefijo.
  - No puede incluir el `_` separador de dígitos.

  Si el prefijo o un separador de dígitos está presente, la llamada a la <xref:System.Convert.ToInt32(System.String,System.Int32)> método produce una <xref:System.FormatException>.

## <a name="see-also"></a>Vea también

- <xref:Microsoft.VisualBasic.Conversion.Hex%2A>
- <xref:System.Convert.ToInt32%2A?displayProperty=nameWithType>
