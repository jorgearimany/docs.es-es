---
title: Uso compartido de puertos Net.TCP
ms.date: 03/30/2017
helpviewer_keywords:
- port activation [WCF]
- port sharing [WCF]
ms.assetid: f13692ee-a179-4439-ae72-50db9534eded
ms.openlocfilehash: b04266b15f786e3a5a93ac1e9fff1754c397ccd4
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59073699"
---
# <a name="nettcp-port-sharing"></a>Uso compartido de puertos Net.TCP
Windows Communication Foundation (WCF) proporciona un nuevo protocolo de red basados en TCP (net.tcp://) para la comunicación de alto rendimiento. WCF también introduce un nuevo componente del sistema, el servicio de uso compartido de puertos Net.TCP que permite a los puertos de net.tcp para compartirse entre varios procesos de usuario.  
  
## <a name="background-and-motivation"></a>Fondo y motivación  
 Cuando se introdujo el protocolo TCP/IP por primera vez, solo un número pequeño de protocolos de aplicación lo emplearon. TCP/IP utilizaba números de puertos para diferenciar entre aplicaciones asignando un número de puerto de 16 bits único para cada protocolo de aplicación. Por ejemplo, el tráfico de HTTP hoy está normalizado para que utilice el puerto TCP 80, SMTP utiliza el puerto TCP 25 y el FTP utiliza los puertos TCP 20 y 21. Otras aplicaciones que utilicen TCP como transporte pueden elegir otro número de puerto disponible, por convención o a través de estandarización formal.  
  
 El uso de números de puerto para distinguir entre aplicaciones provocaba problemas de seguridad. Los firewalls generalmente se configuran para bloquear el tráfico TCP en todos los puertos salvo unos puntos de entrada conocidos, así que implementar una aplicación que utiliza un puerto no estándar es, a menudo, complicado o imposible, debido a la presencia de firewalls personales y corporativos. Las aplicaciones que pueden comunicarse sobre puertos estándar bien conocidos que ya están permitidos, reducen la superficie de ataque externo. Muchas aplicaciones de red utilizan el protocolo HTTP porque la mayoría de los firewalls se configuran de forma predeterminada para permitir el tráfico en el puerto TCP 80.  
  
 El modelo HTTP.SYS en el que el tráfico de muchas aplicaciones HTTP diferentes se multiplexa hacia un único puerto TCP se ha vuelto un estándar en la plataforma de Windows. Esto proporciona un punto común de control para los administradores del firewall, al tiempo que permite a los desarrolladores de aplicaciones minimizar el costo de implementación de crear nuevas aplicaciones que pueden utilizar la red.  
  
 La capacidad de compartir puertos en varias aplicaciones HTTP ha sido durante mucho tiempo una característica de Internet Information Services (IIS). Sin embargo, solo fue con la introducción de HTTP.SYS (el agente de escucha de protocolo HTTP de modo kernel) con [!INCLUDE[iis601](../../../../includes/iis601-md.md)] que se generalizó por completo esta infraestructura. En efecto, HTTP.SYS permite a procesos de usuario arbitrarios compartir los puertos TCP dedicados al tráfico de HTTP. Esta función permite que muchas aplicaciones HTTP coexistan en el mismo equipo físico en procesos aislados y separados mientras comparten la infraestructura de red requerida para enviar y recibir tráfico a través del puerto TCP 80. El servicio de uso compartido de puertos Net.TCP permite el mismo tipo de uso compartido de puertos para las aplicaciones de net.tcp.  
  
## <a name="port-sharing-architecture"></a>Arquitectura de uso compartido de puertos  
 La arquitectura de uso compartido de puertos en WCF tiene tres componentes principales:  
  
-   Un proceso de trabajo: Cualquier proceso que se comunica sobre net.tcp:// utilizando los puertos compartidos.  
  
-   El transporte TCP de WCF: Implementa el protocolo net.tcp://.  
  
-   El servicio de uso compartido de puertos Net.TCP: Permite que varios procesos de trabajo compartir el mismo puerto TCP.  
  
 El servicio de uso compartido de puertos Net.TCP es un servicio de Windows de modo de usuario que acepta conexiones net.tcp:// en nombre de los procesos de trabajo que se conectan a través de él. Cuando una conexión de socket llega, el servicio de uso compartido de puertos inspecciona la secuencia del mensaje entrante para obtener su dirección de destino. Basándose en esta dirección, el servicio de uso compartido de puertos puede enrutar el flujo de datos a la aplicación que finalmente lo procesa.  
  
 Cuando un servicio WCF que usa los puertos de net.tcp:// se abre, la infraestructura de transporte TCP de WCF no abre directamente un socket TCP en el proceso de aplicación. En su lugar, la infraestructura de transporte registra el Identificador uniforme de recursos (URI) de la dirección base del servicio con el servicio de uso compartido de puertos Net.TCP y espera a que el servicio de uso compartido de puertos escuche mensajes en su nombre.  El servicio de uso compartido de puertos entrega mensajes direccionados al servicio de la aplicación según van llegando.  
  
## <a name="installing-port-sharing"></a>Instalación del uso compartido de puertos  
 El servicio de uso compartido de puertos Net.TCP está disponible en todos los sistemas operativos que [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] admite, pero el servicio no está habilitado de forma predeterminada. Como precaución de seguridad, un administrador debe poder habilitar manualmente el servicio de uso compartido de puertos Net.TCP antes de utilizarlo por primera vez. El servicio de uso compartido de puertos Net.TCP expone opciones de configuración que permiten manipular varias características de los sockets de red que posee el servicio de uso compartido de puertos. Para obtener más información, vea [Cómo: Habilitar el servicio de uso compartido de puertos Net.TCP](../../../../docs/framework/wcf/feature-details/how-to-enable-the-net-tcp-port-sharing-service.md).  
  
## <a name="using-nettcp-port-sharing-in-an-application"></a>Uso del uso compartido de puertos Net.tcp en una aplicación  
 La manera más fácil de usar puertos de net.tcp:// en su aplicación WCF es exponer un servicio mediante el <xref:System.ServiceModel.NetTcpBinding> y, a continuación, para habilitar el servicio de uso compartido de puertos Net.TCP mediante el <xref:System.ServiceModel.NetTcpBinding.PortSharingEnabled%2A> propiedad.  
  
 Para obtener más información sobre cómo hacerlo, vea [Cómo: Configurar un servicio WCF para utilizar puertos compartidos](../../../../docs/framework/wcf/feature-details/how-to-configure-a-wcf-service-to-use-port-sharing.md).  
  
## <a name="security-implications-of-port-sharing"></a>Implicaciones de seguridad del uso compartido de puertos  
 Aunque el servicio de uso compartido de puertos Net.TCP proporciona una capa de procesamiento entre las aplicaciones y la red, las aplicaciones que utilizan el uso compartido de puertos todavía deberían seguir estando protegidas como si estuvieran realizando escuchas directamente en la red. En concreto, las aplicaciones que utilizan el uso compartido de puertos deberían evaluar los privilegios de procesos bajo los que se ejecutan. Considere ejecutar su aplicación utilizando la cuenta de servicio de red integrada, que se ejecuta con el conjunto mínimo de privilegios de procesos requeridos para la comunicación por red.  
  
## <a name="see-also"></a>Vea también

- [Configuración del servicio de uso compartido de puertos Net.TCP](../../../../docs/framework/wcf/feature-details/configuring-the-net-tcp-port-sharing-service.md)
- [Hospedar aplicaciones de WPF](../../../../docs/framework/wcf/feature-details/hosting.md)
- [Cómo: Configurar un servicio WCF para utilizar puertos compartidos](../../../../docs/framework/wcf/feature-details/how-to-configure-a-wcf-service-to-use-port-sharing.md)
- [Cómo: Habilitar el servicio de uso compartido de puertos Net.TCP](../../../../docs/framework/wcf/feature-details/how-to-enable-the-net-tcp-port-sharing-service.md)
