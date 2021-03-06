---
ms.openlocfilehash: 88e00454894c8404fd48e92404e35ae27fa056f6
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59235797"
---
### <a name="wpf-treeviewitem-must-be-used-within-a-treeview"></a>El elemento TreeViewItem de WPF se debe usar dentro de una instancia de TreeView

|   |   |
|---|---|
|Detalles|En la versión 4.5 se introdujo un cambio que restringe el uso de elementos <xref:System.Windows.Controls.TreeViewItem?displayProperty=name> fuera de una instancia de <xref:System.Windows.Controls.TreeView?displayProperty=name>. Se manifiesta en las siguientes condiciones:<ul><li>Cuando el elemento primario del objeto visual de <xref:System.Windows.Controls.TreeViewItem?displayProperty=name> no es un panel. (Un elemento <xref:System.Windows.Controls.TreeViewItem?displayProperty=name> generado para una instancia de <xref:System.Windows.Controls.TreeView?displayProperty=name> tendrá un panel como su elemento primario).</li><li>Cuando el elemento <xref:System.Windows.Controls.TreeViewItem?displayProperty=name> es un descendiente de una instancia de <xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=name> que actúa como &quot;host de elementos&quot; para un control de lista (ListBox, DataGrid, ListView, etc.). No es necesario que la virtualización esté activada.</li><li>El panel <xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=name> se desplaza por elementos (<code>ScrollUnit=&quot;Item&quot;</code>).</li><li>Alguien llama a <code>VirtualizingStackPanel.MakeVisible(v)</code> para desplazar un elemento <code>v</code> a la vista. Puede hacerse de forma explícita, o bien implícita de diferentes formas; tal vez la más habitual sea simplemente hacer clic en <code>v</code> para asignarle el foco del teclado.</li><li>La cadena del elemento primario del objeto visual desde <code>v</code> a <xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=name> pasa a través del elemento <xref:System.Windows.Controls.TreeViewItem?displayProperty=name>.</li></ul>En otras palabras, esto se observa cuando se usa un elemento <xref:System.Windows.Controls.TreeViewItem?displayProperty=name> fuera de una instancia de <xref:System.Windows.Controls.TreeView?displayProperty=name> y el usuario hace clic en un descendiente del elemento <xref:System.Windows.Controls.TreeViewItem?displayProperty=name> para mostrarlo en la vista. Si el elemento <xref:System.Windows.Controls.TreeViewItem?displayProperty=name> no tiene ningún descendiente activable, nunca observará este problema. Un ejemplo de situación en la que se produce este problema es cuando el elemento <xref:System.Windows.Controls.TreeViewItem?displayProperty=name> es la raíz de una instancia de DataTemplate. Cuando se produce este problema, se genera una instancia InvalidCastException dentro del marco de WPF.|
|Sugerencia|Se lanzará una revisión para esta solucionar esta situación.|
|Ámbito|Secundaria|
|Versión|4.5|
|Tipo|Tiempo de ejecución|
