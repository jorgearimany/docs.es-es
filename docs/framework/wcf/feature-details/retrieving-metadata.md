---
title: Recuperación de metadatos
ms.date: 03/30/2017
helpviewer_keywords:
- metadata [WCF], retrieving
ms.assetid: 18d8ba4c-af0f-4827-a50b-4202d767bacc
ms.openlocfilehash: bb415d88c2bae75cb16aa137bdf867eb463afa63
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59152404"
---
# <a name="retrieving-metadata"></a>Recuperación de metadatos
La recuperación de metadatos es el proceso de solicitar y recuperar los metadatos desde un extremo de metadatos, como un extremo de metadatos de WS-MetadataExchange (MEX) o de HTTP/GET.  
  
## <a name="retrieving-metadata-from-the-command-line-using-svcutilexe"></a>Recuperación de metadatos de la línea de comandos mediante Svcutil.exe  
 Puede recuperar metadatos de servicio mediante solicitudes HTTP/GET o WS-MetadataExchange utilizando la [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) herramienta y pasando el `/target:metadata` conmutador y una dirección. Svcutil.exe descarga los metadatos en la dirección especificada y guarda el archivo en el disco. Svcutil.exe utiliza una instancia <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> internamente y carga la configuración de punto de conexión de <xref:System.ServiceModel.Description.IMetadataExchange> desde la configuración cuyo nombre coincide con el esquema de la dirección pasada a Svcutil.exe como entrada.  
  
## <a name="retrieving-metadata-programmatically-using-the-metadataexchangeclient"></a>Recuperación de metadatos mediante programación con MetadataExchangeClient  
 Windows Communication Foundation (WCF) puede recuperar los metadatos del servicio mediante protocolos normalizados como WS-MetadataExchange y solicitudes HTTP/GET. Ambos protocolos están admitidos por el tipo <xref:System.ServiceModel.Description.MetadataExchangeClient>. Recupera metadatos de servicio utilizando el tipo <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> al proporcionar una dirección para el extremo de metadatos y un enlace opcional. El enlace utilizado por una instancia de <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> puede ser uno de los enlaces predeterminados de la clase estática <xref:System.ServiceModel.Description.MetadataExchangeBindings>, un enlace proporcionado por el usuario o un enlace cargado desde una configuración de extremo para el contrato `IMetadataExchange`. <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> también puede resolver las referencias a la dirección URL HTTP a los metadatos utilizando el tipo <xref:System.Net.HttpWebRequest>.  
  
 De forma predeterminada, se ata una instancia <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> a una instancia <xref:System.ServiceModel.ChannelFactory> única. Puede cambiar o reemplazar la instancia <xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType> utilizada por <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> invalidando el método virtual <xref:System.ServiceModel.Description.MetadataExchangeClient.GetChannelFactory%2A>. De igual forma, puede cambiar o reemplazar la instancia de <xref:System.Net.HttpWebRequest> utilizada por <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> para realizar solicitudes HTTP/GET mediante la invalidación del método virtual <xref:System.ServiceModel.Description.MetadataExchangeClient.GetWebRequest%2A?displayProperty=nameWithType>.  
  
## <a name="in-this-section"></a>En esta sección  
 [Cómo: Utilice Svcutil.exe para descargar documentos de metadatos](../../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-download-metadata-documents.md)  
 Demuestra cómo usar Svcutil.exe para descargar los documentos de metadatos.  
  
 [Cómo: Utilizar MetadataResolver para obtener dinámicamente metadatos de enlace](../../../../docs/framework/wcf/feature-details/how-to-use-metadataresolver-to-obtain-binding-metadata-dynamically.md)  
 Muestra cómo utilizar <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=nameWithType> para obtener dinámicamente metadatos de enlace en el tiempo de ejecución.  
  
 [Cómo: Utilizar MetadataExchangeClient para recuperar metadatos](../../../../docs/framework/wcf/feature-details/how-to-use-metadataexchangeclient-to-retrieve-metadata.md)  
 Muestra cómo utilizar la clase <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> para descargar los archivos de metadatos en un objeto <xref:System.ServiceModel.Description.MetadataSet?displayProperty=nameWithType> que contiene objetos <xref:System.ServiceModel.Description.MetadataSection?displayProperty=nameWithType> para escribir en archivos o para otros usos.  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Description.MetadataExchangeClient>
