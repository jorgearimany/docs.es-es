---
title: Procedimiento Dibujar una secuencia de B&#233;curvas spline de Bézier
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- splines [Windows Forms], drawing Bezier
- Bezier splines [Windows Forms], drawing sequence of
ms.assetid: 37a0bedb-20c2-4cf0-91fa-a5509e826b30
ms.openlocfilehash: 976787f5830282a581d05a9c24d1f83dceca4b25
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59168160"
---
# <a name="how-to-draw-a-sequence-of-b233zier-splines"></a>Procedimiento Dibujar una secuencia de B&#233;curvas spline de Bézier
Puede usar el <xref:System.Drawing.Graphics.DrawBeziers%2A> método de la <xref:System.Drawing.Graphics> conectado de clase para dibujar una secuencia de curvas spline de Bézier.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente dibuja una curva que consta de dos curvas spline de Bézier conectadas. El punto de conexión de la primera curva spline de Bézier es el punto inicial de la segunda curva spline de Bézier.  
  
 La siguiente ilustración muestra las curvas spline conectada junto con los siete puntos:  
  
 ![Gráfico que muestra las curvas spline conectada junto con los siete puntos.](./media/how-to-draw-a-sequence-of-bezier-splines/bezier-spline-seven-points.png)  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#11)]  
  
## <a name="compiling-the-code"></a>Compilar el código  
 El ejemplo anterior está diseñado para su uso con Windows Forms y requiere <xref:System.Windows.Forms.PaintEventArgs> `e`, que es un parámetro de la <xref:System.Windows.Forms.Control.Paint> controlador de eventos.  
  
## <a name="see-also"></a>Vea también

- [Gráficos y dibujos en Windows Forms](graphics-and-drawing-in-windows-forms.md)
- [Curvas spline de Bézier en GDI+](bezier-splines-in-gdi.md)
- [Crear y dibujar curvas](constructing-and-drawing-curves.md)
