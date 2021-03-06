---
title: Procedimiento para determinar en qué panel del control StatusBar de formularios Windows Forms se hizo clic
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- status bars [Windows Forms], determining panel clicked
- panels [Windows Forms], determining clicked
- StatusBar control [Windows Forms], coding panel click events
- StatusBar control [Windows Forms], determining panel clicked
- PanelClick event [Windows Forms], determining panel clicked
- Panel control [Windows Forms], determining click
ms.assetid: d14c6092-04b2-4a07-8ddf-0dd11277ff5f
ms.openlocfilehash: 1c28f8eaba5c35f762d6fc57ebbddbbb71769c81
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59304290"
---
# <a name="how-to-determine-which-panel-in-the-windows-forms-statusbar-control-was-clicked"></a>Procedimiento para determinar en qué panel del control StatusBar de formularios Windows Forms se hizo clic
> [!IMPORTANT]
>  El <xref:System.Windows.Forms.StatusStrip> y <xref:System.Windows.Forms.ToolStripStatusLabel> controles reemplazan y agregan funcionalidad a la <xref:System.Windows.Forms.StatusBar> y <xref:System.Windows.Forms.StatusBarPanel> controla; sin embargo, el <xref:System.Windows.Forms.StatusBar> y <xref:System.Windows.Forms.StatusBarPanel> controles se conservan por compatibilidad con versiones anteriores y uso futuro, si se Elija esta opción.  
  
 Programa la [StatusBar (Control)](statusbar-control-windows-forms.md) control para responder a clics de usuario, utilice una instrucción case dentro de la <xref:System.Windows.Forms.StatusBar.PanelClick> eventos. El evento contiene un argumento (el argumento del panel), que contiene una referencia a la ha hecho clic <xref:System.Windows.Forms.StatusBarPanel>. Mediante esta referencia, puede determinar el índice del panel que se hace clic en él y programar en consecuencia.  
  
> [!NOTE]
>  Asegúrese de que el <xref:System.Windows.Forms.StatusBar> del control <xref:System.Windows.Forms.StatusBar.ShowPanels%2A> propiedad está establecida en `true`.  
  
### <a name="to-determine-which-panel-was-clicked"></a>Para determinar qué panel se hizo clic  
  
1. En el <xref:System.Windows.Forms.StatusBar.PanelClick> controlador de eventos, use un `Select Case` (en Visual Basic) o `switch case` (Visual C# o [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]) instrucción para determinar qué panel se hizo clic examinando el índice del panel con clic en los argumentos del evento.  
  
     El siguiente ejemplo de código requiere la presencia, en el formulario, de un <xref:System.Windows.Forms.StatusBar> control, `StatusBar1`y dos <xref:System.Windows.Forms.StatusBarPanel> objetos, `StatusBarPanel1` y `StatusBarPanel2`.  
  
    ```vb  
    Private Sub StatusBar1_PanelClick(ByVal sender As System.Object, ByVal e As System.Windows.Forms.StatusBarPanelClickEventArgs) Handles StatusBar1.PanelClick  
       Select Case StatusBar1.Panels.IndexOf(e.StatusBarPanel)  
         Case 0  
           MessageBox.Show("You have clicked Panel One.")  
         Case 1  
           MessageBox.Show("You have clicked Panel Two.")  
       End Select  
    End Sub  
    ```  
  
    ```csharp  
    private void statusBar1_PanelClick(object sender,   
    System.Windows.Forms.StatusBarPanelClickEventArgs e)  
    {  
       switch (statusBar1.Panels.IndexOf(e.StatusBarPanel))  
       {  
          case 0 :  
             MessageBox.Show("You have clicked Panel One.");  
             break;  
          case 1 :  
             MessageBox.Show("You have clicked Panel Two.");  
             break;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void statusBar1_PanelClick(System::Object ^  sender,  
          System::Windows::Forms::StatusBarPanelClickEventArgs ^  e)  
       {  
          switch (statusBar1->Panels->IndexOf(e->StatusBarPanel))  
          {  
             case 0 :  
                MessageBox::Show("You have clicked Panel One.");  
                break;  
             case 1 :  
                MessageBox::Show("You have clicked Panel Two.");  
                break;  
          }  
       }  
    ```  
  
     (Visual C#, [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]) coloque el código siguiente en el constructor del formulario para registrar el controlador de eventos.  
  
    ```csharp  
    this.statusBar1.PanelClick += new   
       System.Windows.Forms.StatusBarPanelClickEventHandler   
       (this.statusBar1_PanelClick);  
    ```  
  
    ```cpp  
    this->statusBar1->PanelClick += gcnew  
       System::Windows::Forms::StatusBarPanelClickEventHandler  
       (this, &Form1::statusBar1_PanelClick);  
    ```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Forms.StatusBar>
- <xref:System.Windows.Forms.ToolStripStatusLabel>
- [Cómo: Establecer el tamaño de los paneles de la barra de estado](how-to-set-the-size-of-status-bar-panels.md)
- [Tutorial: Actualizar la información de la barra de estado en tiempo de ejecución](walkthrough-updating-status-bar-information-at-run-time.md)
- [Información general sobre StatusBar (Control)](statusbar-control-overview-windows-forms.md)
