---
title: MDA de dateTimeInvalidLocalFormat
ms.date: 03/30/2017
helpviewer_keywords:
- dates [.NET Framework], formatting
- invalid date time local format
- invalid local formats
- MDAs (managed debugging assistants), invalid local formats
- managed debugging assistants (MDAs), invalid local formats
- dateTimeInvalidLocalFormat MDA
- date formatting
- time formatting
- UTC formatting
ms.assetid: c4a942bb-2651-4b65-8718-809f892a0659
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 380334dbe9b91ea369de6cbe58686a9a74254c2c
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59148231"
---
# <a name="datetimeinvalidlocalformat-mda"></a>MDA de dateTimeInvalidLocalFormat
El MDA `dateTimeInvalidLocalFormat` se activa cuando una instancia de <xref:System.DateTime> que está almacenada como horario universal coordinado (UTC) tiene un formato pensado para usarse solo para instancias locales de <xref:System.DateTime>. Este MDA no está activado para instancias de <xref:System.DateTime> sin especificar o predeterminadas.  
  
## <a name="symptom"></a>Síntoma  
 Una aplicación está serializando manualmente una instancia de <xref:System.DateTime> UTC mediante un formato local:  
  
```csharp
DateTime myDateTime = DateTime.UtcNow;  
Serialize(myDateTime.ToString("yyyy-MM-dd'T'HH:mm:ss.fffffffzzz"));  
```  
  
### <a name="cause"></a>Motivo  
 El formato "z" para el método <xref:System.DateTime.ToString%2A?displayProperty=nameWithType> incluye el desplazamiento de zona horaria local, por ejemplo, "+ 10:00" para la hora de Sydney. Por lo tanto, solo genera un resultado significativo si el valor de <xref:System.DateTime> es local. Si el valor es la hora UTC, <xref:System.DateTime.ToString%2A?displayProperty=nameWithType> incluye el desplazamiento de zona horaria local, pero no muestra ni ajusta el especificador de zona horaria.  
  
### <a name="resolution"></a>Resolución  
 Las instancias de <xref:System.DateTime> UTC deben tener el formato de una manera que indique que son UTC. El formato recomendado para la hora UTC es usar un carácter "Z" para indicar la hora UTC:  
  
```csharp
DateTime myDateTime = DateTime.UtcNow;  
Serialize(myDateTime.ToString("yyyy-MM-dd'T'HH:mm:ss.fffffffZ"));  
```  
  
 También hay un formato "o" que serializa un instancia de <xref:System.DateTime> mediante la propiedad <xref:System.DateTime.Kind%2A>, que serializa correctamente independientemente de si la instancia es local, UTC o sin especificar:  
  
```csharp
DateTime myDateTime = DateTime.UtcNow;  
Serialize(myDateTime.ToString("o"));  
```  
  
## <a name="effect-on-the-runtime"></a>Efecto en el Runtime  
 Este MDA no afecta al tiempo de ejecución.  
  
## <a name="output"></a>Salida  
 No hay ningún resultado especial como consecuencia de la activación de este MDA, aunque se puede usar la pila de llamadas para determinar la ubicación de la llamada a <xref:System.DateTime.ToString%2A> que ha activado el MDA.  
  
## <a name="configuration"></a>Configuración  
  
```xml  
<mdaConfig>  
  <assistants>  
    <dateTimeInvalidLocalFormat />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>Ejemplo  
 Imagine una aplicación que está serializando indirectamente un valor <xref:System.DateTime> UTC mediante la clase <xref:System.Xml.XmlConvert> o <xref:System.Data.DataSet> de la siguiente manera.  
  
```csharp
DateTime myDateTime = DateTime.UtcNow;  
String serialized = XMLConvert.ToString(myDateTime);  
```  
  
 Las serializaciones <xref:System.Xml.XmlConvert> y <xref:System.Data.DataSet> usan formatos locales para la serialización de forma predeterminada. Se necesitan opciones adicionales para serializar otros tipos de valores <xref:System.DateTime>, como UTC.  
  
 Para obtener este ejemplo concreto, pase `XmlDateTimeSerializationMode.RoundtripKind` a la llamada a `ToString` en `XmlConvert`. Con esto se serializan los datos como una hora UTC.  
  
 Si usa <xref:System.Data.DataSet>, establezca la propiedad <xref:System.Data.DataColumn.DateTimeMode%2A> del objeto <xref:System.Data.DataColumn> en <xref:System.Data.DataSetDateTime.Utc>.  
  
```csharp
DateTime myDateTime = DateTime.UtcNow;  
String serialized = XmlConvert.ToString(myDateTime,   
    XmlDateTimeSerializationMode.RoundtripKind);  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Globalization.DateTimeFormatInfo>
- [Diagnosing Errors with Managed Debugging Assistants (Diagnóstico de errores con asistentes para la depuración administrada)](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
