---
title: <endpoint> de <client>
ms.date: 03/30/2017
ms.assetid: de6238ae-bbf8-48e9-a1b5-e24c0bea8afa
ms.openlocfilehash: 3af41ad5b5681b08aac44d984372ab5ac66caf5e
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59231206"
---
# <a name="endpoint-of-client"></a>\<punto de conexión > de \<cliente >
Especifica el contrato, enlace y propiedades de dirección del extremo del canal, que es utilizado por clientes para conectar a los extremos de servicio en el servidor.  
  
 \<system.ServiceModel>  
\<client>  
\<endpoint>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<endpoint address="String"
          behaviorConfiguration="String"
          binding="String"
          bindingConfiguration="String"
          contract="String"
          endpointConfiguration="String"
          kind="String"
          name="String">
</endpoint>
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|dirección|Atributo de cadena necesario.<br /><br /> Especifica la dirección del punto de conexión. El valor predeterminado es una cadena vacía. La dirección debe ser un URI absoluto.|  
|behaviorConfiguration|Una cadena que contiene el nombre de comportamiento del comportamiento que se va a usar para crear una instancia del punto de conexión. El nombre de comportamiento debe estar en el ámbito en el punto definido del servicio. El valor predeterminado es una cadena vacía.|  
|enlace|Atributo de cadena necesario.<br /><br /> Una cadena que indica el tipo de enlace que se va a utilizar. El tipo debe tener una sección de configuración registrada para que se haga referencia al mismo. El tipo está registrado por el nombre de sección, en lugar de por el nombre de tipo del enlace.|  
|bindingConfiguration|Opcional. Una cadena que contiene el nombre de la configuración de enlace que se va a utilizar cuando se instancia el extremo. La configuración del enlace debe estar en el ámbito en el punto definido del punto de conexión. El valor predeterminado es una cadena vacía.<br /><br /> Este atributo se utiliza junto con `binding` para hacer referencia a una configuración de enlace concreta en el archivo de configuración. Establezca este atributo si está intentando utilizar un enlace personalizado. De lo contrario, puede producirse una excepción.|  
|contrato|Atributo de cadena necesario.<br /><br /> Una cadena que indica qué contrato está exponiendo este punto de conexión. El ensamblado debe implementar el tipo de contrato.|  
|endpointConfiguration|Cadena que especifica el nombre del punto de conexión estándar establecido por el atributo `kind`, que hace referencia a la información de configuración adicional de este punto de conexión estándar. El mismo nombre se debe definir en la sección `<standardEndpoints>`.|  
|kind|Cadena que especifica el tipo de extremo estándar aplicado. El tipo se debe registrar en la sección `<extensions>` o en machine.config. Si no se especifica nada, se crea un extremo de canal común.|  
|name|Atributo de cadena opcional. Este atributo identifica singularmente un extremo para un contrato determinado. Puede definir varios clientes para un tipo de contrato determinado. Cada definición tiene que diferenciarse por un nombre de configuración unívoco. Si se omite este atributo, el punto de conexión correspondiente se usa como el punto de conexión predeterminado asociado al tipo de contrato especificado. El valor predeterminado es una cadena vacía.<br /><br /> El atributo de `name` de un enlace se utiliza para la exportación de la definición a través de WSDL.|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<headers>](../../../../../docs/framework/configure-apps/file-schema/wcf/headers.md)|Una colección de encabezados de dirección.|  
|[\<identity>](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)|Una identidad que habilita la autenticación de un punto de conexión por otros puntos de conexión que intercambian mensajes con él.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<client>](../../../../../docs/framework/configure-apps/file-schema/wcf/client.md)|Una sección de configuración que define una lista de puntos de conexión a los que un cliente puede conectarse.|  
  
## <a name="example"></a>Ejemplo  
 Éste es un ejemplo de una configuración del extremo del canal.  
  
```xml  
<endpoint address="/HelloWorld/"
          bindingConfiguration="usingDefaults"
          name="MyBinding"
          binding="customBinding"
          contract="HelloWorld">
</endpoint>
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Configuration.ChannelEndpointElement>
- <xref:System.ServiceModel.Configuration.ClientSection>
- <xref:System.ServiceModel.Configuration.ChannelEndpointElementCollection>
- <xref:System.ServiceModel.Configuration.ClientSection.Endpoints%2A>
- <xref:System.ServiceModel.Configuration.ChannelEndpointElement>
- [Configuración del cliente de WCF](../../../../../docs/framework/wcf/feature-details/client-configuration.md)
- [Clientes](../../../../../docs/framework/wcf/feature-details/clients.md)
