---
title: <appDomainResourceMonitoring> (Elemento)
ms.date: 03/30/2017
helpviewer_keywords:
- appDomainResourceMonitoring element
- <appDomainResourceMonitoring> element
ms.assetid: 02119ab6-1e91-448e-97ad-e7b2e5c4bbbd
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 71cc69eba17de8465cc7999f334c724e4ec14e7d
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59224382"
---
# <a name="appdomainresourcemonitoring-element"></a>\<appDomainResourceMonitoring > elemento
Indica el runtime para recopilar estadísticas de todos los dominios de aplicación en el proceso mientras dura este.  
  
 \<configuration>  
\<runtime>  
\<appDomainResourceMonitoring>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<appDomainResourceMonitoring    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|`enabled`|Atributo necesario.<br /><br /> Especifica si el tiempo de ejecución recopila estadísticas para la supervisión de recursos de dominio de aplicación.|  
  
## <a name="enabled-attribute"></a>Atributo enabled  
  
|Valor|Descripción|  
|-----------|-----------------|  
|`true`|Se recopilan estadísticas para la supervisión de recursos de dominio de aplicación.|  
|`false`|No se recopilan estadísticas para la supervisión de recursos de dominio de aplicación.|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|`configuration`|Elemento raíz de cada archivo de configuración usado por las aplicaciones de Common Language Runtime y .NET Framework.|  
|`runtime`|Contiene información del enlace del ensamblado y de la recolección de elementos no utilizados.|  
  
## <a name="remarks"></a>Comentarios  
 Supervisión de recursos de dominio de aplicación está disponible a través de la clase de dominio de aplicación administrada, el hospedaje [ICLRAppDomainResourceMonitor](../../../../../docs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-interface.md) interfaz y seguimiento de eventos para Windows (ETW). Cuando se habilita la supervisión, se recopilan estadísticas para todos los dominios de aplicación en el proceso durante la vida del proceso.  
  
 Para habilitar la supervisión desde código administrado, utilice el <xref:System.AppDomain.MonitoringIsEnabled%2A> propiedad.  
  
 Este elemento de configuración solo está disponible en el [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] y versiones posteriores.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo se habilita la supervisión de recursos de dominio de aplicación.  
  
```xml  
<configuration>  
   <runtime>  
      <appDomainResourceMonitoring enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=nameWithType>
- [Esquema de la configuración de Common Language Runtime](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [Esquema de los archivos de configuración](../../../../../docs/framework/configure-apps/file-schema/index.md)
