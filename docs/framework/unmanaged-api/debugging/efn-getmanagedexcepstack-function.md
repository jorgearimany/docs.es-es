---
title: _EFN_GetManagedExcepStack (Función)
ms.date: 03/30/2017
api_name:
- _EFN_GetManagedExcepStack
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- _EFN_GetManagedExcepStack
helpviewer_keywords:
- _EFN_GetManagedExcepStack function [.NET Framework debugging]
ms.assetid: 21ceed9e-62b2-4024-b027-6d095109955a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7e201b9a350c030da59e2b6ed27f84f570c8e621
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59126664"
---
# <a name="efngetmanagedexcepstack-function"></a>_EFN_GetManagedExcepStack (Función)
Dada una dirección de objeto de excepción administrado, devuelve una versión de cadena del seguimiento de pila que contiene.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT _EFN_GetManagedExcepStack(  
    [in]  PDEBUG_CLIENT Client,  
    [in]  ULONG64       StackObjAddr,  
    [out] __out_ecount(cbString) PSTR szStackString,  
    [out] ULONG         cbString  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `Client`  
 [in] El cliente que se está depurando.  
  
 `StackObjAddr`  
 [in] Un puntero de objeto administrado, derivado de <xref:System.Exception>.  
  
 szStackString  
 [out] La cadena devuelta.  
  
 `cbString`  
 [out] El número de caracteres disponibles en el búfer de cadena.  
  
## <a name="remarks"></a>Comentarios  
 Si no hay ningún código administrado en el subproceso actualmente en contexto, la función devuelve HRESULT SOS_E_NOMANAGEDCODE con un valor 0xa0 y un código de error de 0 x 1000.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: SOS_Stacktrace.h  
  
 **Versión de .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Funciones estáticas globales de depuración](../../../../docs/framework/unmanaged-api/debugging/debugging-global-static-functions.md)
