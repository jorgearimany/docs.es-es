---
ms.openlocfilehash: cbe1b32fa40e509f620845866c7a584e37f49a80
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774225"
---
### <a name="targetframeworkname-for-default-app-domain-no-longer-defaults-to-null-if-not-set"></a>TargetFrameworkName para el dominio de aplicación predeterminado ya no tiene un valor NULL como valor predeterminado si no se establece

|   |   |
|---|---|
|Detalles|<xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=name> anteriormente tenía un valor NULL en el dominio de aplicación predeterminado, a menos que se estableciera de forma explícita. A partir de la versión 4.6, la propiedad <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=name> del dominio de aplicación predeterminado tendrá un valor predeterminado derivado del elemento TargetFrameworkAttribute (si hay alguno presente). Los dominios de aplicación no predeterminados continuarán heredando su propiedad <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=name> del dominio de aplicación predeterminado (que no tendrá un valor NULL como valor predeterminado en la versión 4.6) a menos que se invalide de forma explícita.|
|Sugerencia|El código debería actualizarse para no depender de que <xref:System.AppDomainSetup.TargetFrameworkName> establezca un valor nulo como valor predeterminado. Si es necesario que esta propiedad continúe evaluándose como un valor nulo, puede establecerse en dicho valor de forma explícita.|
|Ámbito|Borde|
|Versión|4.6|
|Tipo|Tiempo de ejecución|
|API afectadas|<ul><li><xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=nameWithType></li></ul>|
