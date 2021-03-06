---
title: <standardEndpoints>
ms.date: 03/30/2017
ms.assetid: d62153d7-a6e6-462a-a784-cca61e9c2ba1
ms.openlocfilehash: 66b86647689ea2ca39ae2f569d275aff1f48cba5
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59190280"
---
# <a name="standardendpoints"></a>\<standardEndpoints>
Esta sección de configuración le permite definir una colección de puntos de conexión estándar, que son los puntos de conexión preconfigurados reutilizables. Un punto de conexión estándar tendrá uno o más atributos de la dirección, el enlace y el contrato establecidos en un valor fijo. Por ejemplo, en el punto de conexión de la detección el contrato es fijo. También puede usar los puntos de conexión estándar para extender el punto de conexión de servicio con nuevas propiedades similares a la definición de enlaces personalizados.  
  
 \<system.ServiceModel>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<system.serviceModel>
  <standardEndpoints>
  </standardEndpoints>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
 Ninguno.  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<announcementEndpoint>](announcementendpoint.md)|Define un punto de conexión estándar con un contrato de anuncio fijo. Un servicio puede anunciar su disponibilidad opcionalmente enviando un mensaje del anuncio en línea y sin conexión cuando se abre o se cierra respectivamente. Un servicio de Windows Communication Foundation (WCF) especifica los extremos del anuncio en el [ \<serviceDiscovery >](servicediscovery.md) elemento y utiliza AnnouncementClient para realizar los anuncios. Un cliente que desea escuchar el anuncio desde otro servicio realmente está actuando como un servicio WCF; Por tanto, tendrá que configurar los extremos del anuncio para el cliente en el [ \<services >](services.md) sección.|  
|[\<discoveryEndpoint>](discoveryendpoint.md)|Define un punto de conexión estándar con un contrato de detección fijo. Cuando se agrega a la configuración de servicio, especifica dónde escuchar los mensajes de detección. Cuando se agrega a la configuración del cliente, especifica dónde enviar las consultas de detección.|  
|[\<dynamicEndpoint>](dynamicendpoint.md)|Este elemento de configuración define un punto de conexión estándar que contiene información para permitir que una aplicación funcione como un programa cliente que pueda buscar la dirección del punto de conexión dinámicamente en tiempo de ejecución.|  
|[\<mexEndpoint>](mexendpoint.md)|Define un punto de conexión estándar con un contrato IMetadataExchange fijo. Puesto que todos los puntos de conexión del intercambio de metadatos especifican IMetadataExchange como su contrato, puede usar este punto estándar en lugar de definir uno para sí mismo.|  
|[\<udpAnnouncementEndpoint>](udpannouncementendpoint.md)|Define un extremo estándar que usan los servicios para enviar mensajes de anuncio a través de un enlace de UDP. Tiene un contrato fijo y admite dos versiones de la detección. Además, tiene un enlace de UDP fijo y un valor de dirección predeterminado según se indica en las especificaciones de WS-Discovery (WS-Discovery April 2005 o WS-Discovery versión 1.1). Puede especificar la dirección de multidifusión que se va a usar para enviar y recibir los mensajes del anuncio.|  
|[\<udpDiscoveryEndpoint>](udpdiscoveryendpoint.md)|Define un extremo estándar que se pre-configura para las operaciones de detección en un enlace de multidifusión de UDP. Este punto de conexión tiene un contrato fijo y admite dos versiones del protocolo WS-Discovery. Además, tiene un enlace de UDP fijo y una dirección predeterminada según se indica en las especificaciones de WS-Discovery (WS-Discovery April 2005 o WS-Discovery V1.1).|  
|[\<webHttpEndpoint>](webhttpendpoint.md)|Define un extremo estándar con un fijo [ \<webHttpBinding >](webhttpbinding.md) enlace que automáticamente se agrega el [ \<webHttp >](webhttp.md) comportamiento. Utilice este punto de conexión al escribir un servicio REST.|  
|[\<webScriptEndpoint>](webscriptendpoint.md)|Define un extremo estándar con un fijo [ \<webHttpBinding >](webhttpbinding.md) enlace que automáticamente se agrega el [ \<enableWebScript >](enablewebscript.md) comportamiento. Use este extremo cuando esté escribiendo un servicio al que se llama desde una aplicación AJAX de ASP.NET.|  
|[\<workflowControlEndpoint>](workflowcontrolendpoint.md)|Define un extremo estándar para controlar la ejecución de instancias de flujo de trabajo (crear, ejecutar, suspender, terminar, etc).|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|\<system.ServiceModel>|Elemento raíz de todos los elementos de configuración de WCF.|  
  
## <a name="see-also"></a>Vea también

- [Puntos de conexión estándar](../../../../../docs/framework/wcf/feature-details/standard-endpoints.md)
