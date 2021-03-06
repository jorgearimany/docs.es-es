---
title: Procedimiento Implementar la notificación de cambio de propiedad
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- notifications of change [WPF]
- data binding [WPF], property change notifications
- change notifications [WPF]
- properties [WPF], change notifications
ms.assetid: 30b59d9e-8c3a-4349-aa82-4be837e841cf
ms.openlocfilehash: d37d468acc94470be8c2afdc495b40168932ec83
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59204359"
---
# <a name="how-to-implement-property-change-notification"></a>Procedimiento Implementar la notificación de cambio de propiedad
Para admitir <xref:System.Windows.Data.BindingMode.OneWay> o <xref:System.Windows.Data.BindingMode.TwoWay> enlace para habilitar las propiedades de destino de enlace para que reflejen automáticamente los cambios dinámicos del origen del enlace (por ejemplo, para que el panel de vista previa actualizado automáticamente cuando el usuario edita un formulario), la clase debe proporcionar las notificaciones de cambio de propiedad adecuado. En este ejemplo se muestra cómo crear una clase que implementa <xref:System.ComponentModel.INotifyPropertyChanged>.  
  
## <a name="example"></a>Ejemplo  
 Para implementar <xref:System.ComponentModel.INotifyPropertyChanged> debe declarar la <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> eventos y cree el `OnPropertyChanged` método. Por lo tanto, para cada propiedad para las que desee cambiar las notificaciones, calle a `OnPropertyChanged` cuando se actualice la propiedad.  
  
 [!code-csharp[SimpleBinding#PersonClass](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Person.cs#personclass)]
 [!code-vb[SimpleBinding#PersonClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Person.vb#personclass)]  
  
 Para ver un ejemplo de cómo el `Person` clase puede usarse para admitir <xref:System.Windows.Data.BindingMode.TwoWay> enlace, vea [controlar cuándo el texto de TextBox actualiza el origen](how-to-control-when-the-textbox-text-updates-the-source.md).  
  
## <a name="see-also"></a>Vea también

- [Información general sobre orígenes de enlaces](binding-sources-overview.md)
- [Información general sobre el enlace de datos](data-binding-overview.md)
- [Temas "Cómo..."](data-binding-how-to-topics.md)
