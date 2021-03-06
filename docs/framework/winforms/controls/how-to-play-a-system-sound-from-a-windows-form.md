---
title: Procedimiento para reproducir un sonido del sistema desde un formulario Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sounds [Windows Forms], playing for system events
- playing sounds [Windows Forms], Windows Forms
- system sounds [Windows Forms], playing from Windows Forms
- playing sounds [Windows Forms], system
- SoundPlayer class [Windows Forms], system sounds
- sounds [Windows Forms], playing
- examples [Windows Forms], sounds
ms.assetid: afb206ff-4824-4804-a8d4-185bf5ad8e7c
ms.openlocfilehash: d85d8cd40ff2b32cb3f2a79cf9a8221964f186c0
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59153236"
---
# <a name="how-to-play-a-system-sound-from-a-windows-form"></a>Procedimiento para reproducir un sonido del sistema desde un formulario Windows Forms
El siguiente código de ejemplo reproduce el sonido del sistema `Exclamation` en tiempo de ejecución. Para obtener más información sobre los sonidos del sistema, consulte <xref:System.Media.SystemSounds>.  
  
## <a name="example"></a>Ejemplo  
  
```vb  
Public Sub PlayExclamation()  
    SystemSounds.Exclamation.Play()  
End Sub  
```  
  
```csharp  
public void playExclamation()  
{  
    SystemSounds.Exclamation.Play();  
}  
```  
  
## <a name="compiling-the-code"></a>Compilar el código  
 Para este ejemplo se necesita:  
  
-   Una referencia al espacio de nombres <xref:System.Media?displayProperty=nameWithType>.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Media.SoundPlayer>
- <xref:System.Media.SystemSounds>
- [Cómo: Reproducir un sonido desde Windows Forms](how-to-play-a-beep-from-a-windows-form.md)
- [Cómo: Reproducir un sonido desde Windows Forms](how-to-play-a-sound-from-a-windows-form.md)
