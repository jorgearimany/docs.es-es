---
title: "'<membername>' es ambiguo en las interfaces heredadas '<interfacename1>' y '<interfacename2>'"
ms.date: 07/20/2015
f1_keywords:
- vbc30685
- bc30685
helpviewer_keywords:
- BC30685
ms.assetid: 756add7a-23d5-4b4f-a48d-8297d6459c73
ms.openlocfilehash: 4415608bcfca63b43b3d9ebf17ce622ccd418775
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58820862"
---
# <a name="membername-is-ambiguous-across-the-inherited-interfaces-interfacename1-and-interfacename2"></a>'\<membername >' es ambiguo en las interfaces heredadas\<interfacename1 >' y '\<interfacename2 >'
La interfaz hereda a dos o más miembros con el mismo nombre de varias interfaces.  
  
 **Identificador de error:** BC30685  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
-   Convierte el valor a la interfaz base que desea usar; Por ejemplo:  
  
    ```  
    Interface Left  
        Sub MySub()  
    End Interface  
  
    Interface Right  
        Sub MySub()  
    End Interface  
  
    Interface LeftRight  
        Inherits Left, Right  
    End Interface  
  
    Module test  
        Sub Main()  
            Dim x As LeftRight  
            ' x.MySub()  'x is ambiguous.  
            CType(x, Left).MySub() ' Cast to base type.  
            CType(x, Right).MySub() ' Call the other base type.  
        End Sub  
    End Module  
    ```  
  
## <a name="see-also"></a>Vea también

- [Interfaces](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
