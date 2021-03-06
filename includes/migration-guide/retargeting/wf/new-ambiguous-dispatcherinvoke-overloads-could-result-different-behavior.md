---
ms.openlocfilehash: 4529d8040fc08b5290ac46abd1ef752086ea3aeb
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774491"
---
### <a name="new-ambiguous-dispatcherinvoke-overloads-could-result-in-different-behavior"></a>Las nuevas sobrecargas (ambiguas) de Dispatcher.Invoke pueden generar otro comportamiento

|   |   |
|---|---|
|Detalles|.NET Framework 4.5 agrega nuevas sobrecargas para <xref:System.Windows.Threading.Dispatcher.Invoke%2A?displayProperty=nameWithType>, entre las que se incluye un parámetro de tipo <xref:System.Action>. Cuando el código existente se vuelve a compilar, los compiladores pueden resolver llamadas a métodos Dispatcher.Invoke que tienen un parámetro <xref:System.Delegate> como llamadas a métodos Dispatcher.Invoke con un parámetro <xref:System.Action>. Si una llamada a una sobrecarga de Dispatcher.Invoke con un parámetro <xref:System.Delegate> se resuelve como una llamada a una sobrecarga de Dispatcher.Invoke con un parámetro <xref:System.Action>, se pueden producir las diferencias de comportamiento siguientes:<ul><li>Si se produce una excepción, no se inician los eventos <xref:System.Windows.Threading.Dispatcher.UnhandledExceptionFilter> y <xref:System.Windows.Threading.Dispatcher.UnhandledException>. En su lugar, las excepciones se controlan mediante el evento <xref:System.Threading.Tasks.TaskScheduler.UnobservedTaskException?displayProperty=name>.</li><li>Las llamadas a algunos miembros, como <xref:System.Windows.Threading.DispatcherOperation.Result>, se bloquean hasta que se completa la operación.</li></ul>|
|Sugerencia|Para evitar ambigüedades (y posibles diferencias en el control de excepciones o los comportamientos de bloqueo), el código que llame a Dispatcher.Invoke puede pasar un objeto vacío [] como segundo parámetro de la llamada a Invoke para garantizar que la resolución se resuelva en la sobrecarga del método de .NET Framework 4.0.|
|Ámbito|Secundaria|
|Versión|4.5|
|Tipo|Redestinación|
|API afectadas|<ul><li><xref:System.Windows.Threading.Dispatcher.Invoke(System.Delegate,System.Object[])?displayProperty=nameWithType></li><li><xref:System.Windows.Threading.Dispatcher.Invoke(System.Delegate,System.TimeSpan,System.Object[])?displayProperty=nameWithType></li><li><xref:System.Windows.Threading.Dispatcher.Invoke(System.Delegate,System.TimeSpan,System.Windows.Threading.DispatcherPriority,System.Object[])?displayProperty=nameWithType></li><li><xref:System.Windows.Threading.Dispatcher.Invoke(System.Delegate,System.Windows.Threading.DispatcherPriority,System.Object[])?displayProperty=nameWithType></li></ul>|
