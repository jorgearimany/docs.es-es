---
title: CorSetENC (Enumeración)
ms.date: 03/30/2017
api_name:
- CorSetENC
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorSetENC
helpviewer_keywords:
- CorSetENC enumeration [.NET Framework metadata]
ms.assetid: fe4150e8-071d-43fb-8e06-c3c616dbeed2
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1fd903cb4a9ce664b7a1c958a3fef0c639d6845d
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59122322"
---
# <a name="corsetenc-enumeration"></a>CorSetENC (Enumeración)
Contiene valores que se usan para influir en el comportamiento durante la generación de metadatos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
typedef enum CorSetENC {  
  
    MDSetENCOn                  = 0x00000001,  
    MDSetENCOff                 = 0x00000002,  
  
    MDUpdateENC                 = 0x00000001,  
    MDUpdateFull                = 0x00000002,  
    MDUpdateExtension           = 0x00000003,  
    MDUpdateIncremental         = 0x00000004,  
    MDUpdateDelta               = 0x00000005,  
    MDUpdateMask                = 0x00000007  
  
} CorSetENC;  
```  
  
## <a name="members"></a>Miembros  
  
|Miembro|Descripción|  
|------------|-----------------|  
|`MDSetENCOn`|Obsoleto.|  
|`MDSetENCOff`|Obsoleto.|  
|`MDUpdateENC`|Indica que mientras que se pueden actualizar los metadatos, no se pueden mover los tokens.|  
|`MDUpdateFull`|Indica que se pueden mover los tokens durante las actualizaciones.|  
|`MDUpdateExtension`|Indica que las actualizaciones pueden constar solo de las adiciones. No se puede mover los tokens.|  
|`MDUpdateIncremental`|Indica que la compilación es incremental.|  
|`MDUpdateDelta`|Indica que solo los metadatos modificados se deben guardar.|  
|`MDUpdateMask`|Incluye `MDUpdateENC`, `MDUpdateFull` y `MDUpdateIncremental`.|  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorHdr.h  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Enumeraciones para metadatos](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
