---
title: Arquitectura de WPF
ms.date: 03/30/2017
helpviewer_keywords:
- properties [WPF], attached
- attached properties [WPF]
- architecture [WPF]
- unmanaged components [WPF]
- affinity thread [WPF]
- Storyboards [WPF]
- milcore [WPF]
- components [WPF], unmanaged
- painter's algorithm
- interfaces [WPF], INotifyPropertyChange
- CommandBindings [WPF]
- data templates [WPF]
- thread [WPF], affinity
ms.assetid: 8579c10b-76ab-4c52-9691-195ce02333c8
ms.openlocfilehash: f4a6e6c2a63e58c40e0cca9c67b12d1f65af0d2e
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59199432"
---
# <a name="wpf-architecture"></a>Arquitectura de WPF
En este tema se proporciona un paseo guiado de la jerarquía de clases de Windows Presentation Foundation (WPF). En él se explican la mayoría de los subsistemas principales de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] y se describe cómo interactúan. También se detallan algunas de las decisiones tomadas por los arquitectos de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  

<a name="System_Object"></a>   
## <a name="systemobject"></a>System.Object  
 El modelo de programación primario de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] se expone a través de código administrado. En las primeras fases del proceso de diseño de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], hubo varios debates sobre dónde se debería fijar el límite entre los componentes administrados del sistema y los no administrados. [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] proporciona varias características que pueden hacer el proceso más sólido y productivo (como son la administración de memoria, el control de errores, Common Type System, etc.) pero todas ellas tienen su costo.  
  
 Los componentes principales de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] se muestran en la ilustración siguiente. Las secciones rojas del diagrama (PresentationFramework, PresentationCore y Milcore) son los componentes principales del código de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]. De estos, solo uno es un componente no administrado: Milcore. Milcore se ha escrito en código no administrado para permitir una estrecha integración con [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)]. La visualización en [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] se realiza a través del motor de [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)], lo que permite una representación eficaz mediante hardware y software. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] también ha necesitado un control preciso sobre la memoria y la ejecución. El motor de composición de Milcore es sumamente sensible al rendimiento, y se tuvo que renunciar a muchas de las ventajas de [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] para obtener rendimiento.  
  
 ![La posición de WPF dentro de .NET Framework.](./media/wpf-architect1.PNG "wpf_architect1")  
  
 La comunicación entre las partes administradas y no administradas de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] se describe más adelante en este tema. A continuación se describe el resto del modelo de programación administrado.  
  
<a name="System_Threading_DispatcherObject"></a>   
## <a name="systemthreadingdispatcherobject"></a>System.Threading.DispatcherObject  
 Mayoría de los objetos en [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] derivan <xref:System.Windows.Threading.DispatcherObject>, que proporciona las estructuras básicas para tratar con la simultaneidad y subprocesos. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] está basado en un sistema de mensajería implementado por el distribuidor. Funciona de modo similar al conocido suministro de mensajes de [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)]; de hecho, el distribuidor de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] usa los mensajes de User32 para realizar las llamadas entre subprocesos.  
  
 Es necesario comprender dos conceptos básicos al hablar de simultaneidad en [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]: el distribuidor y la afinidad de subprocesos.  
  
 Durante la fase de diseño de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], el objetivo era adoptar un único subproceso de ejecución, pero perteneciente a un modelo "con afinidad" y sin subprocesos. La afinidad de subprocesos se produce cuando un componente usa la identidad del subproceso que se está ejecutando para almacenar algún tipo de estado. La forma más común de esta afinidad es usar el almacenamiento local de subprocesos (TLS) para almacenar el estado. La afinidad de subprocesos requiere que cada subproceso lógico de ejecución sea propiedad de un único subproceso físico en el sistema operativo, lo que puede consumir mucha memoria. Finalmente, el modelo de subprocesos de WPF se mantuvo sincronizado con el modelo de subprocesos de User32 existente, que consiste en la ejecución de un solo subproceso con afinidad de subprocesos. La principal razón para esto fue la interoperabilidad; los sistemas como [!INCLUDE[TLA2#tla_ole2.0](../../../../includes/tla2sharptla-ole2-0-md.md)], el Portapapeles e Internet Explorer requieren la ejecución de afinidad con subproceso único (STA).  
  
 Dado que disponemos de objetos con subprocesos STA, necesitamos un medio de comunicación entre subprocesos y estar seguros de que nos encontramos en el subproceso correcto. A continuación se describe el rol del distribuidor. El distribuidor es un sistema de envío de mensajes básico que dispone de varias colas con prioridad. Por ejemplo, son mensajes las notificaciones de entrada sin formato (el mouse se ha movido), las funciones de marco de trabajo (diseño) o los comandos de usuario (ejecutar este método). Al derivar de <xref:System.Windows.Threading.DispatcherObject>, se crea un [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] objeto que tiene el comportamiento STA y le ofrecerá un puntero a un distribuidor durante la creación.  
  
<a name="System_Windows_DependencyObject"></a>   
## <a name="systemwindowsdependencyobject"></a>System.Windows.DependencyObject  
 Una de las principales filosofías arquitectónicas usadas al crear [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] fue la preferencia por las propiedades en lugar de los métodos o los eventos. Las propiedades son declarativas y le permiten especificar más fácilmente la intención en lugar de la acción. Esto también ha permitido el uso de un sistema basado en modelos, o en datos, para mostrar el contenido de la interfaz de usuario. Esta filosofía tenía como objetivo crear más propiedades con las que poder enlazar, y así tener un mejor control del comportamiento de una aplicación.  
  
 Para conseguir que más partes del sistema estuviesen controladas por propiedades, era necesario un sistema de propiedades más completo que el proporcionado por [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]. Un ejemplo sencillo de esto son las notificaciones de cambios. Para poder habilitar los enlaces bidireccionales, será necesario que ambos lados del enlace admitan la notificación de cambios. Para poder tener el comportamiento vinculado a los valores de propiedad, deberá recibir una notificación cuando cambie el valor de la propiedad. Microsoft .NET Framework tiene una interfaz, **INotifyPropertyChange**, lo que permite a un objeto publicar las notificaciones de cambio, aunque es opcional.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] Proporciona un sistema de propiedades más completo, derivado de la <xref:System.Windows.DependencyObject> tipo. El sistema de propiedades puede considerarse un sistema de "dependencias" porque realiza el seguimiento de las dependencias entre las expresiones de las propiedades y vuelve a validar automáticamente los valores de propiedad cuando cambian las dependencias. Por ejemplo, si tiene una propiedad que hereda (como <xref:System.Windows.Controls.Control.FontSize%2A>), el sistema se actualiza automáticamente si cambia la propiedad en un elemento primario de un elemento que hereda el valor.  
  
 La base del sistema de propiedades de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] es el concepto de una expresión de propiedad. En esta primera versión de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], el sistema de expresión de propiedades es cerrado y todas las expresiones que se proporcionan forman parte del marco de trabajo. Las expresiones son el motivo de que el sistema de propiedades no tenga características de enlace de datos, de estilo o de herencia incluidas en el código, sino que son proporcionadas por capas posteriores dentro del marco de trabajo.  
  
 El sistema de propiedades también proporciona almacenamiento disperso de valores de propiedades. Debido a que los objetos pueden tener docenas (o incluso cientos) de propiedades, y la mayoría de los valores está en su estado predeterminado (heredado, establecido por estilos, etc.), no todas las instancias de un objeto necesitan tener definidas todas las propiedades.  
  
 La última de las características nuevas del sistema de propiedades es el concepto de propiedades adjuntas. Los elementos de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] se basan en el principio de composición y reutilización de componentes. A menudo es el caso de que algunos que contiene el elemento (como un <xref:System.Windows.Controls.Grid> elemento de diseño) necesita datos adicionales sobre los elementos secundarios para controlar su comportamiento (por ejemplo, la información de fila/columna). En lugar de asociar todas estas propiedades a cada elemento, cualquier objeto puede proporcionar las definiciones de las propiedades para cualquier otro objeto. Esto es similar a las características "expando" de JavaScript.  
  
<a name="System_Windows_Media_Visual"></a>   
## <a name="systemwindowsmediavisual"></a>System.Windows.Media.Visual  
 Con un sistema ya definido, el paso siguiente consiste en conseguir que se dibujen los píxeles en la pantalla. El <xref:System.Windows.Media.Visual> proporciona clases para la creación de un árbol de objetos visuales, cada uno puede contener instrucciones de dibujo y metadatos sobre cómo presentar esas instrucciones (recorte, transformación, etcetera.). <xref:System.Windows.Media.Visual> está diseñado para ser sumamente ligero y flexible, por lo que la mayoría de las características no tienen pública [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] exposición y dependen en gran medida de las funciones de devolución de llamada protegidas.  
  
 <xref:System.Windows.Media.Visual> es realmente el punto de entrada para el [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] sistema de composición. <xref:System.Windows.Media.Visual> es el punto de conexión entre estos dos subsistemas, los recursos administrados [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] y el milcore no administrado.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] muestra los datos recorriendo las estructuras de datos no administradas de cuya administración se encarga Milcore. Estas estructuras, denominadas nodos de composición, representan un árbol de presentación jerárquica con instrucciones de representación en cada nodo. Solo se puede tener acceso a este árbol, mostrado en el lado derecho de la ilustración siguiente, a través de un protocolo de mensajería.  
  
 Cuando se programan [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], creas <xref:System.Windows.Media.Visual> elementos y los tipos derivados, que se comunican internamente en el árbol de composición a través de este protocolo de mensajería. Cada <xref:System.Windows.Media.Visual> en [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] puede crear uno, ninguno o varios nodos de composición.  
  
 ![Árbol visual de Windows Presentation Foundation.](./media/wpf-architecture2.PNG "wpf_architecture2")  
  
 Hay que observar aquí un detalle arquitectónico muy importante, y es que el árbol completo de objetos visuales e instrucciones de dibujo se guarda en la memoria caché. En términos gráficos, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] usa un sistema de representación retenido. Esto permite al sistema volver a dibujar con frecuencias de actualización altas sin que el sistema de composición bloquee las devoluciones de llamada al código del usuario. Esto ayuda a evitar la sensación de que la aplicación no responde.  
  
 Otro detalle importante que no es muy evidente en el diagrama es la forma en la que el sistema realiza realmente la composición.  
  
 En User32 y [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)], el sistema se basa en un método de recorte de modo inmediato. Cuando es necesario representar un componente, el sistema establece un límite de recorte en cuyo exterior no permite al componente tocar los píxeles y, después, le pide que pinte los píxeles en ese cuadro. Este método funciona muy bien en sistemas con restricciones de memoria, ya que cuando algo cambia solo se debe modificar el componente afectado; nunca hay dos componentes que afecten al color de un mismo píxel.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] usa un modelo de representación "algoritmo de pintor". Esto significa que, en lugar de recortar cada componente, se pide a este que efectúe la representación desde la parte trasera hacia la parte delantera de la imagen. Esto permite a cada componente pintar sobre la imagen generada por el componente anterior. La ventaja de este modelo es que permite tener formas complejas parcialmente transparentes. Con el moderno hardware gráfico actual, este modelo es relativamente rápido (lo que no ocurría cuando se crearon User32/ [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)]).  
  
 Como se ha mencionado previamente, la filosofía básica de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] es adoptar un modelo de programación más declarativo y "centrado en las propiedades". En el sistema visual, esto se pone de manifiesto en un par de lugares interesantes.  
  
 En primer lugar, si piensa en el sistema de gráficos de modo retenido, este se está alejando de un modelo de tipo DrawLine/DrawLine imperativo hacia un modelo orientado a datos, new Line()/new Line(). Esta migración hacia la representación controlada por datos permite expresar operaciones complejas en las instrucciones de dibujo mediante propiedades. Los tipos derivados de <xref:System.Windows.Media.Drawing> son efectivamente el modelo de objetos para la representación.  
  
 En segundo lugar, si evalúa el sistema de animación, verá que es declarativo casi por completo. En lugar de exigir al desarrollador que calcule la ubicación o el color siguiente, las animaciones pueden expresarse como un conjunto de propiedades en un objeto de animación. Estas animaciones permitirán expresar la intención del desarrollador o del diseñador (mueva este botón de aquí a allí en 5 segundos) y el sistema podrá determinar la manera más eficaz de lograrlo.  
  
<a name="System_Windows_UIElement"></a>   
## <a name="systemwindowsuielement"></a>System.Windows.UIElement  
 <xref:System.Windows.UIElement> define los subsistemas básicos: diseño, entrada y eventos.  
  
 El diseño es un concepto básico en [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]. Son muchos los sistemas en los que, o existe un conjunto fijo de modelos de diseño (HTML admite tres modelos de diseño; flujo, absoluto y tablas), o no existe ningún modelo de diseño (en realidad, User32 solo admite el posicionamiento absoluto). [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] se inició presuponiendo que los desarrolladores y diseñadores querían un modelo de diseño flexible y extensible, que pudiera ser controlado por valores de propiedades en lugar de por lógica imperativa. En el <xref:System.Windows.UIElement> nivel, se introduce el contrato para el diseño básico: modelo con la fase dos <xref:System.Windows.UIElement.Measure%2A> y <xref:System.Windows.UIElement.Arrange%2A> pasa.  
  
 <xref:System.Windows.UIElement.Measure%2A> permite que un componente determinar el tamaño quiera realizar. Se trata de una fase independiente de <xref:System.Windows.UIElement.Arrange%2A> porque hay muchas situaciones donde un elemento primario le pedirá un elemento secundario se mida varias veces para determinar su posición y tamaño óptimos. El hecho de que los elementos primarios pidan a los elementos secundarios que se midan demuestra otra filosofía clave de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], el ajuste al contenido. Todos los controles de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] admiten la capacidad de ajustarse al tamaño natural de su contenido. Esto facilita enormemente la localización y permite un diseño dinámico de los elementos cuando los objetos cambian de tamaño. El <xref:System.Windows.UIElement.Arrange%2A> fase permite un elemento primario colocar y determinar el tamaño final de cada elemento secundario.  
  
 Mucho tiempo a menudo, se habla sobre la salida de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] – <xref:System.Windows.Media.Visual> y objetos relacionados. En cambio, también hay una gran cantidad de innovaciones en cuanto a la entrada. Probablemente el cambio más importante en el modelo de entrada para [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] es el modelo coherente mediante el cual los eventos de entrada se enrutan a través del sistema.  
  
 La entrada se origina en forma de señal en un controlador de dispositivo de modo kernel y se vuelve a enrutar al proceso y subproceso correctos a través de un intrincado procedimiento que implica el kernel de Windows y User32. Una vez que el mensaje de User32 correspondiente a la entrada se ha enrutado a [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], se convierte en un mensaje de entrada sin formato de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] y se envía al distribuidor. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] permite convertir los eventos de entrada sin formato en varios eventos reales, lo que permite la implementación de características como "MouseEnter" en un nivel bajo del sistema con entrega garantizada.  
  
 Cada evento de entrada se convierte en al menos dos eventos, un evento de "vista previa" y el evento real. Todos los eventos de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] tienen información de enrutamiento a través del árbol de elementos. Se dice que los eventos "se traspasan" si atravesar desde un destino hasta el árbol hasta la raíz y se dice que "tunelizan" si se inician en la raíz y recorrer hacia abajo hasta un destino. Los eventos de vista previa de entrada tunelizan, lo que ofrece a cualquiera de los elementos del árbol una oportunidad para filtrar o realizar acciones cuando se produce un evento. Los eventos normales (sin vista previa) se traspasan a continuación desde el destino hasta la raíz.  
  
 Esta diferencia entre la fase de túnel y de traspaso permite que la implementación de características como los aceleradores de teclado funcione de manera coherente en un universo compuesto. En User32, la implementación de los aceleradores de teclado se realizaría teniendo una tabla global única con todos los aceleradores admitidos (Ctrl+N asignado a "Nuevo"). En el distribuidor de la aplicación se llamaría a **TranslateAccelerator**, que examinaría los mensajes de entrada en User32 y determinaría si alguno de ellos coincide con un acelerador registrado. En [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] esto no funcionaría, ya que el sistema es totalmente "ajustable", es decir, que cualquier elemento puede controlar y usar cualquier acelerador de teclado. Tener este modelo de dos fases para la entrada permite a los componentes implementar su propio "TranslateAccelerator".  
  
 Para realizar un paso más, <xref:System.Windows.UIElement> también introduce el concepto de CommandBindings. El [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] sistema de comandos permite a los desarrolladores definir la funcionalidad en cuanto a un punto final de comando: algo que implementa <xref:System.Windows.Input.ICommand>. Los enlaces de comandos permiten a un elemento definir una asignación entre un gesto de entrada (Ctrl+N) y un comando (Nuevo). Tanto los gestos de entrada como las definiciones de comandos son extensibles, y pueden conectarse en el momento de su uso. Esto hace que resulte trivial, por ejemplo, permitir que un usuario final personalice los enlaces de teclado que quiere usar dentro de una aplicación.  
  
 Hasta ahora, este tema se ha centrado en las características "básicas" de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], es decir, las características implementadas en el ensamblado PresentationCore. Al compilar [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], una separación limpia entre las partes fundamentales (como el contrato para el diseño con **medida** y **organizar**) y las partes del marco de trabajo (por ejemplo, la implementación de un determinado diseño como <xref:System.Windows.Controls.Grid>) fue el resultado deseado. El objetivo era proporcionar un punto de extensibilidad en la zona inferior de la pila que permitiría a los programadores externos crear sus propios marcos de trabajo en caso necesario.  
  
<a name="System_Windows_FrameworkElement"></a>   
## <a name="systemwindowsframeworkelement"></a>System.Windows.FrameworkElement  
 <xref:System.Windows.FrameworkElement> puede ser examinado de dos maneras diferentes. Presenta un conjunto de directivas y personalizaciones en los subsistemas incluidos en las capas inferiores de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]. También presenta un conjunto de nuevos subsistemas.  
  
 La directiva primaria presentada por <xref:System.Windows.FrameworkElement> es alrededor de diseño de la aplicación. <xref:System.Windows.FrameworkElement> se basa en el contrato del diseño básico introducido por <xref:System.Windows.UIElement> y agrega la noción de un diseño "ranura", lo que facilita a los autores del diseño tiene un conjunto coherente de semántica del diseño orientados de propiedad. Propiedades como <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>, <xref:System.Windows.FrameworkElement.MinWidth%2A>, y <xref:System.Windows.FrameworkElement.Margin%2A> (por nombrar algunos) dar a todos los componentes derivados <xref:System.Windows.FrameworkElement> un comportamiento coherente dentro de contenedores de diseño.  
  
 <xref:System.Windows.FrameworkElement> También facilita [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] muchas de las características que se encuentra en las capas básicas de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]. Por ejemplo, <xref:System.Windows.FrameworkElement> proporciona acceso directo a la animación a través de la <xref:System.Windows.FrameworkElement.BeginStoryboard%2A> método. Un <xref:System.Windows.Media.Animation.Storyboard> proporciona una manera de varias animaciones con un conjunto de propiedades de script.  
  
 Las dos cosas más importantes que <xref:System.Windows.FrameworkElement> presenta son el enlace de datos y estilos.  
  
 El subsistema de enlace de datos de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] debería resultarle relativamente familiar a cualquiera que haya usado [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] o [!INCLUDE[TLA#tla_aspnet](../../../../includes/tlasharptla-aspnet-md.md)] para crear la [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] de una aplicación. En cada uno de estos sistemas, hay una manera sencilla de expresar que quiere enlazar una o varias propiedades de un elemento determinado a un fragmento de datos. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] ofrece compatibilidad total para el enlace de propiedades, la transformación y el enlace de listas.  
  
 Una de las características más interesantes del enlace de datos en [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] es la introducción de plantillas de datos. Las plantillas de datos le permiten especificar mediante declaración cómo se debería visualizar un fragmento de datos. En lugar de crear una interfaz de usuario personalizada que se puede enlazar a los datos, puede solucionar el problema permitiendo que los datos determinen la presentación que se va a crear.  
  
 La aplicación de estilos es realmente una forma ligera de enlace de datos. El uso de estilos le permite enlazar un conjunto de propiedades de una definición compartida a una o varias instancias de un elemento. Los estilos se aplican a un elemento mediante una referencia explícita (estableciendo la <xref:System.Windows.FrameworkElement.Style%2A> propiedad) o de forma implícita asociando un estilo con el [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] tipo del elemento.  
  
<a name="System_Windows_Controls_Control"></a>   
## <a name="systemwindowscontrolscontrol"></a>System.Windows.Controls.Control  
 La característica más significativa del control es la definición de plantillas. Si piensa en el sistema de composición de WPF como en un sistema de representación de modo retenido, la definición de plantillas permite a un control describir su representación de una manera parametrizada y declarativa. Un <xref:System.Windows.Controls.ControlTemplate> es realmente nada más que una secuencia de comandos para crear un conjunto de secundarios de elementos, con enlaces a las propiedades proporcionadas por el control.  
  
 <xref:System.Windows.Controls.Control> Proporciona un conjunto de propiedades estándar, <xref:System.Windows.Controls.Control.Foreground%2A>, <xref:System.Windows.Controls.Control.Background%2A>, <xref:System.Windows.Controls.Control.Padding%2A>, por nombrar algunas, que los autores de plantillas, a continuación, pueden usar para personalizar la presentación de un control. La implementación de un control proporciona un modelo de datos y un modelo de interacción. El modelo de interacción define un conjunto de comandos (como Cerrar para una ventana) y enlaces a gestos de entrada (como hacer clic en la X roja situada en la esquina superior de la ventana). El modelo de datos proporciona un conjunto de propiedades para personalizar el modelo de interacción o la presentación (determinado por la plantilla).  
  
 Esta diferencia entre el modelo de datos (propiedades), el modelo de interacción (comandos y eventos) y el modelo de presentación (plantillas) permite una total personalización de la apariencia y el comportamiento de un control.  
  
 Un aspecto común del modelo de datos de los controles es el modelo de contenido. Si examina un control como <xref:System.Windows.Controls.Button>, verá que tiene una propiedad denominada "Content" de tipo <xref:System.Object>. En [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] y [!INCLUDE[TLA#tla_aspnet](../../../../includes/tlasharptla-aspnet-md.md)], esta propiedad sería normalmente una cadena; en cambio, esto limita el tipo de contenido que puede colocar en un botón. El contenido de un botón puede ser una cadena simple, un objeto de datos complejo o un árbol de elementos completo. En el caso de un objeto de datos, la plantilla de datos se usa para construir una presentación.  
  
<a name="Summary"></a>   
## <a name="summary"></a>Resumen  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] está diseñado para permitirle crear sistemas de presentación dinámicos y controlados por datos. Cada parte del sistema está diseñada para crear objetos mediante conjuntos de propiedades que controlan el comportamiento. El enlace de datos es una parte fundamental del sistema y está integrado en cada capa.  
  
 Las aplicaciones tradicionales crean una presentación y, después, enlazan a algunos datos. En [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], todo lo relacionado al control, cada aspecto de la presentación, está generado por algún tipo de enlace de datos. El texto situado dentro de un botón se muestra creando un control compuesto dentro de este y enlazando su presentación a la propiedad de contenido del botón.  
  
 Cuando comience a desarrollar aplicaciones basadas en [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], encontrará un entorno muy familiar. Podrá establecer propiedades, usar objetos y enlazar datos de la misma manera que con [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] o [!INCLUDE[TLA#tla_aspnet](../../../../includes/tlasharptla-aspnet-md.md)]. Un examen más profundo de la arquitectura de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] le permitirá descubrir que existe la posibilidad de crear aplicaciones mucho más enriquecidas controladas fundamentalmente por los datos.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Media.Visual>
- <xref:System.Windows.UIElement>
- <xref:System.Windows.Input.ICommand>
- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.Threading.DispatcherObject>
- <xref:System.Windows.Input.CommandBinding>
- <xref:System.Windows.Controls.Control>
- [Información general sobre el enlace de datos](../data/data-binding-overview.md)
- [Diseño](layout.md)
- [Información general sobre animaciones](../graphics-multimedia/animation-overview.md)
