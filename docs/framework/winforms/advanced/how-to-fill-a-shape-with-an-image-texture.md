---
title: Procedimiento para rellenar una forma con una textura de imagen
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [Windows Forms], using with brushes
- bitmaps [Windows Forms], using texture
- shapes [Windows Forms], filling with images
ms.assetid: 508da5a6-2433-4d2b-9680-eaeae4e96e3b
ms.openlocfilehash: 099bc9f5359f19439f308f28a6766d470956daea
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59177325"
---
# <a name="how-to-fill-a-shape-with-an-image-texture"></a>Procedimiento para rellenar una forma con una textura de imagen
Puede rellenar una forma cerrada con una textura utilizando la <xref:System.Drawing.Image> clase y el <xref:System.Drawing.TextureBrush> clase.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente rellena una elipse con una imagen. El código construye una <xref:System.Drawing.Image> de objetos y, a continuación, pasa la dirección de ese <xref:System.Drawing.Image> objeto como argumento a un <xref:System.Drawing.TextureBrush.%23ctor%2A> constructor. La tercera instrucción escala la imagen y la cuarta rellena la elipse con copias repetidas de la imagen escalada.  
  
 En el código siguiente, la <xref:System.Drawing.TextureBrush.Transform%2A> propiedad contiene la transformación que se aplica a la imagen antes de dibujarlo. Suponga que la imagen original tiene un ancho de 640 píxeles y un alto de 480 píxeles. La transformación de la imagen reduce a 75 × 75 estableciendo los valores de escalado horizontales y verticales.  
  
> [!NOTE]
>  En el ejemplo siguiente, el tamaño de la imagen es 75 × 75 y el tamaño de la elipse es 150 × 250. Dado que la imagen es menor que la elipse que va a rellenar, la elipse se coloca en mosaico con la imagen. Se alcanza la disposición en mosaico, que la imagen se repite hasta que el límite de la forma horizontalmente y verticalmente. Para obtener más información acerca de la segmentación, vea [Cómo: Una forma con una imagen en mosaico](how-to-tile-a-shape-with-an-image.md).  
  
 [!code-csharp[System.Drawing.UsingABrush#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.UsingABrush#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#21)]  
  
## <a name="compiling-the-code"></a>Compilar el código  
 El ejemplo anterior está diseñado para su uso con Windows Forms y requiere <xref:System.Windows.Forms.PaintEventArgs> `e`, que es un parámetro de la <xref:System.Windows.Forms.Control.Paint> controlador de eventos.  
  
## <a name="see-also"></a>Vea también

- [Utilizar un pincel para rellenar formas](using-a-brush-to-fill-shapes.md)
