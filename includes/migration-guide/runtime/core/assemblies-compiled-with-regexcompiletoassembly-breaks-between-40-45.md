---
ms.openlocfilehash: 69b25db88c7580787bbb47fb0902b6bb072f8dde
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59235944"
---
### <a name="assemblies-compiled-with-regexcompiletoassembly-breaks-between-40-and-45"></a>Los ensamblados compilados con Regex.CompileToAssembly se interrumpen entre las versiones 4.0 y 4.5

|   |   |
|---|---|
|Detalles|Si un ensamblado de expresiones regulares compiladas se crea con .NET Framework 4.5 pero tiene como destino .NET Framework 4, se inicia una excepción al intentar usar una de las expresiones regulares de ese ensamblado en un sistema con .NET Framework 4 instalado.|
|Sugerencia|Para evitar este problema, realice una de las acciones siguientes:<ul><li>Compile el ensamblado que contiene las expresiones regulares con .NET Framework 4.</li><li>Use una expresión regular interpretada.</li></ul>|
|Ámbito|Secundaria|
|Versión|4.5|
|Tipo|Tiempo de ejecución|
|API afectadas|<ul><li><xref:System.Text.RegularExpressions.Regex.CompileToAssembly(System.Text.RegularExpressions.RegexCompilationInfo[],System.Reflection.AssemblyName)?displayProperty=nameWithType></li><li><xref:System.Text.RegularExpressions.Regex.CompileToAssembly(System.Text.RegularExpressions.RegexCompilationInfo[],System.Reflection.AssemblyName,System.Reflection.Emit.CustomAttributeBuilder[])?displayProperty=nameWithType></li><li><xref:System.Text.RegularExpressions.Regex.CompileToAssembly(System.Text.RegularExpressions.RegexCompilationInfo[],System.Reflection.AssemblyName,System.Reflection.Emit.CustomAttributeBuilder[],System.String)?displayProperty=nameWithType></li></ul>|
