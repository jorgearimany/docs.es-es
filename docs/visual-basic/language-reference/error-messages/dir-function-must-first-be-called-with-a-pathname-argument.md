---
title: Se debe llamar primero a la función 'Dir' con un argumento 'Pathname'
ms.date: 07/20/2015
f1_keywords:
- vbrDIR_IllegalCall
ms.assetid: 7b5d149f-be91-4ac3-8262-86a360894e7d
ms.openlocfilehash: d255b8dddd098835764f72b8a166eaa08b0353df
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59767895"
---
# <a name="dir-function-must-first-be-called-with-a-pathname-argument"></a>Se debe llamar primero a la función 'Dir' con un argumento 'Pathname'
Una llamada inicial a la `Dir` función no incluye el `PathName` argumento. La primera llamada a `Dir` debe incluir un `PathName`, las llamadas posteriores, pero a `Dir` no es necesario incluir parámetros para recuperar el elemento siguiente.  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
1. Proporcione un `PathName` argumento en la llamada de función.  
  
## <a name="see-also"></a>Vea también

- <xref:Microsoft.VisualBasic.FileSystem.Dir%2A>
