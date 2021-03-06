---
title: -win32manifest (Visual Basic)
ms.date: 03/13/2018
helpviewer_keywords:
- /win32manifest compiler option [Visual Basic]
- win32manifest compiler option [Visual Basic]
- -win32manifest compiler option [Visual Basic]
ms.assetid: 9e3191b4-90db-41c8-966a-28036fd20005
ms.openlocfilehash: 15fe62457ed11ffcd08a1db3aa8be57080f22869
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59300803"
---
# <a name="-win32manifest-visual-basic"></a>-win32manifest (Visual Basic)
Identifica un archivo de manifiesto de la aplicación Win32 definido por el usuario que se va a insertar en un archivo ejecutable portable (PE) del proyecto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-win32manifest: fileName  
```  
  
## <a name="arguments"></a>Argumentos  
  
|Término|Definición|  
|---|---|  
|`fileName`|La ruta de acceso del archivo de manifiesto personalizado.|  
  
## <a name="remarks"></a>Comentarios  
 De forma predeterminada, el compilador de Visual Basic incrusta un manifiesto de aplicación que especifica un nivel de ejecución solicitado de asInvoker. Crea el manifiesto en la misma carpeta en la que se compila el archivo ejecutable, normalmente la carpeta bin\Debug o bin\Release cuando se usa Visual Studio. Si desea proporcionar un manifiesto personalizado, por ejemplo, para especificar un nivel de ejecución solicitado de highestAvailable y requireAdministrator, utilice esta opción para especificar el nombre del archivo.  
  
> [!NOTE]
>  Esta opción y la [-win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md) son mutuamente excluyentes. Si intenta usar ambas opciones en la misma línea de comandos, obtendrá un error de compilación.  
  
 Una aplicación sin manifiesto de aplicación que especifique un nivel de ejecución solicitado estará sujeta a virtualización de archivos y Registro conforme a la característica Control de cuentas de usuario de Windows Vista. Para más información sobre la virtualización, vea [Implementación de ClickOnce en Windows Vista](/visualstudio/deployment/clickonce-deployment-on-windows-vista).  
  
 La aplicación estará sujeta a virtualización si se cumple alguna de las condiciones siguientes:  
  
1. Usa el `-nowin32manifest` opción y no se proporciona un manifiesto en un paso de compilación posterior o como parte de un archivo de recursos de Windows (. res) mediante el uso de la `-win32resource` opción.  
  
2. Se proporciona un manifiesto personalizado que no especifica un nivel de ejecución solicitado.  
  
 Visual Studio crea un archivo de manifiesto predeterminado y lo almacena en los directorios de depuración y versión junto con el archivo ejecutable. Puede ver o editar el archivo app.manifest predeterminado haciendo clic en **ver configuración de UAC** en el **aplicación** ficha del Diseñador de proyectos. Para obtener más información, consulte [Application Page, Project Designer (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic).  
  
 Puede proporcionar el manifiesto de aplicación como un paso personalizado posterior a la compilación o como parte de un archivo de recursos Win32 mediante la `-nowin32manifest` opción. Use esa misma opción si quiere que la aplicación esté sujeta a virtualización de archivos y Registro en Windows Vista. Esto evitará que el compilador cree e incruste un manifiesto predeterminado en el archivo PE.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente se muestra el manifiesto predeterminado que el compilador de Visual Basic inserta en un archivo PE.  
  
> [!NOTE]
>  El compilador inserta un nombre de aplicación estándar MyApplication.app en el manifiesto XML. Se trata de una solución alternativa para permitir que las aplicaciones se ejecuten en Windows Server 2003 Service Pack 3.  
  
```xml  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
  <assemblyIdentity version="1.0.0.0" name="MyApplication.app"/>  
  <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">  
    <security>  
      <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">  
        <requestedExecutionLevel level="asInvoker"/>  
      </requestedPrivileges>  
    </security>  
  </trustInfo>  
</assembly>  
```  
  
## <a name="see-also"></a>Vea también

- [Compilador de línea de comandos de Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)
- [-nowin32manifest (Visual Basic)](../../../visual-basic/reference/command-line-compiler/nowin32manifest.md)
