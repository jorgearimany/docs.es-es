---
title: IMetaDataDispenserEx (Interfaz)
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx
helpviewer_keywords:
- IMetaDataDispenserEx interface [.NET Framework metadata]
ms.assetid: 78b3629e-77a2-4406-89c3-56b5cc2c4594
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 96475086b1244ae75ed692dd10cb693af0be9af7
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59186958"
---
# <a name="imetadatadispenserex-interface"></a>IMetaDataDispenserEx (Interfaz)
Extiende la [IMetaDataDispenser (interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-interface.md) interfaz para proporcionar la capacidad para controlar el funcionamiento de las API de metadatos en el ámbito de metadatos actual.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descripción|  
|------------|-----------------|  
|[FindAssembly (método)](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-findassembly-method.md)|Este método no se implementa. Si se llama, devuelve E_NOTIMPL.|  
|[FindAssemblyModule (método)](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-findassemblymodule-method.md)|Este método no se implementa. Si se llama, devuelve E_NOTIMPL.|  
|[GetCORSystemDirectory (método)](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-getcorsystemdirectory-method.md)|Obtiene el directorio que contiene el actual common language runtime (CLR). Este método es compatible solo para su uso con los depuradores fuera de proceso. Si se llama desde otro componente, devolverá E_NOTIMPL.|  
|[GetOption (método)](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-getoption-method.md)|Obtiene el valor de la opción especificada para el ámbito de metadatos actual. La opción controla cómo se controlan las llamadas al ámbito de metadatos actual.|  
|[OpenScopeOnITypeInfo (método)](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-openscopeonitypeinfo-method.md)|Este método no se implementa. Si se llama, devuelve E_NOTIMPL.|  
|[SetOption (método)](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-setoption-method.md)|Establece la opción especificada en un valor especificado para el ámbito de metadatos actual. La opción controla cómo se controlan las llamadas al ámbito de metadatos actual.|  
  
## <a name="requirements"></a>Requisitos  
 **Plataforma:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Cor.h  
  
 **Biblioteca:** Usar como un recurso en MsCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Interfaces de metadatos](../../../../docs/framework/unmanaged-api/metadata/metadata-interfaces.md)
- [IMetaDataDispenser (interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-interface.md)
- [IMetaDataEmit (interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataImport (interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
