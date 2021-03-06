---
title: Crear una clase para contener funciones de archivos DLL
ms.date: 03/30/2017
helpviewer_keywords:
- COM interop, DLL functions
- unmanaged functions
- COM interop, platform invoke
- interoperation with unmanaged code, DLL functions
- interoperation with unmanaged code, platform invoke
- platform invoke, creating class for functions
- DLL functions
ms.assetid: e08e4c34-0223-45f7-aa55-a3d8dd979b0f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 399ad6649016e53d91d5d9d30ecc031ae8a97a4a
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59149362"
---
# <a name="creating-a-class-to-hold-dll-functions"></a>Crear una clase para contener funciones de archivos DLL
Encapsular una función DLL que se usa con frecuencia en una clase administrada es un enfoque efectivo para encapsular la funcionalidad de la plataforma. Aunque no es obligatorio hacerlo en todos los casos, proporcionar un contenedor de clases es cómodo porque la definición de funciones DLL puede ser compleja y propensa a errores. Si está programando en Visual Basic o C#, debe declarar las funciones DLL dentro de una clase o módulo de Visual Basic.  
  
 Dentro de una clase, se define un método estático para cada función DLL que se quiere llamar. La definición puede incluir información adicional, como el juego de caracteres o la convención de llamada que se usa para pasar argumentos de método; si se omite esta información, se selecciona la configuración predeterminada. Para obtener una lista completa de las opciones de declaración y sus valores predeterminados, vea [Crear prototipos en código administrado](../../../docs/framework/interop/creating-prototypes-in-managed-code.md).  
  
 Una vez encapsulados, puede llamar a métodos en la clase como llamaría a los métodos estáticos en cualquier otra clase. La invocación de plataforma controla automáticamente la función exportada subyacente.  
  
 Al diseñar una clase administrada para la invocación de plataforma, tenga en cuenta las relaciones entre las clases y las funciones de archivo DLL. Por ejemplo, se puede:  
  
-   Declarar funciones DLL dentro de una clase existente.  
  
-   Crear una clase individual para cada función DLL, para mantener las funciones aisladas y facilitar su búsqueda.  
  
-   Crear una clase para un conjunto de funciones DLL relacionadas para formar grupos lógicos y reducir la sobrecarga.  
  
 Puede asignar el nombre que quiera a la clase y sus métodos. Para obtener ejemplos que muestran cómo construir declaraciones basadas en .NET para usarse con la invocación de plataforma, vea [Serialización de datos con invocación de plataforma](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md).  
  
## <a name="see-also"></a>Vea también

- [Consumir funciones DLL no administradas](../../../docs/framework/interop/consuming-unmanaged-dll-functions.md)
- [Identificar funciones en archivos DLL](../../../docs/framework/interop/identifying-functions-in-dlls.md)
- [Crear prototipos en código administrado](../../../docs/framework/interop/creating-prototypes-in-managed-code.md)
- [Llamar a una función DLL](../../../docs/framework/interop/calling-a-dll-function.md)
