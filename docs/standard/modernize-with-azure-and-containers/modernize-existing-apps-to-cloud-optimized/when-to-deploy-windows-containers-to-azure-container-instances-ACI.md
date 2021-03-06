---
title: Cuándo se deben implementar contenedores de Windows Azure Container Instances (ACI)
description: Modernizar aplicaciones .NET existentes con contenedores de Windows y la nube de Azure | Cuándo se deben implementar contenedores de Windows Azure Container Instances (ACI)
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/29/2018
ms.openlocfilehash: 03ee7c8b65e1a92dcc7fd40b44e9ba081f571487
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2019
ms.locfileid: "57674411"
---
# <a name="when-to-deploy-windows-containers-to-azure-container-instances-aci"></a>Cuándo se deben implementar contenedores de Windows Azure Container Instances (ACI)

Azure Container Instances propuesta de valor principal es que inmediatamente puede implementar contenedores en él y no es necesario mantener ese entorno, no es necesario actualizar/aplicar revisiones del sistema operativo o las máquinas virtuales, todo lo que es transparente subyacente y acaba de implementar contenedores en un entorno listos para usar.

Los escenarios cuando desee utilizar ACI y motivos son similares a los escenarios principales al usar máquinas virtuales de Azure con contenedores, básicamente, los escenarios principales para usar Azure Container Instances son:

- **Escenarios de desarrollo/pruebas**
- **Automatización de tareas**
- **Agentes de CI/CD**
- **Procesamiento por lotes de pequeño o escala**
- **Aplicaciones web sencillas**

Las aplicaciones web simple es un escenario razonable para ACI, pero tenga en cuenta que dado que en Azure Container Instances solo puede tener una instancia de contenedor único por cada imagen de contenedor, no tendrá alta disponibilidad y solo tienen una limitada escalabilidad.

Sin embargo, incluso cuando ACI se considere como infraestructura porque simplemente proporciona instancias de contenedor único, hay una enorme ventaja en comparación con las máquinas virtuales de Azure normales con Windows Server. Con ACI, solo implementa los contenedores en un entorno de mantenimiento automático y solo paga por los contenedores. No es necesario para mantener, actualizaciones o revisiones de máquinas virtuales, por lo que es una mejor plataforma para la mayoría de los escenarios donde puede que esté usando máquinas virtuales con contenedores. Utilizando ACI es sencilla, simplemente implementar un contenedor, no hay ninguna necesidad de crear un entorno de máquinas virtuales basta con implementar contenedores.

Las principales ventajas de Azure Container Instances (ACI) son:

- Ejecute contenedores sin administrar servidores
- Aumentar la agilidad con contenedores a petición
- Implementar contenedores en la nube con una velocidad y una simplicidad sin precedentes, con un solo comando.
- Aplicaciones seguras con aislamiento de hipervisor

En resumen, con ACI puede desarrollar aplicaciones rápidamente sin administrar máquinas virtuales ni tener que aprender nuevas herramientas. Es simplemente la aplicación en un contenedor, que se ejecutan en la nube.

> [!div class="step-by-step"]
> [Anterior](when-to-deploy-windows-containers-to-azure-vms-iaas-cloud.md)
> [Siguiente](when-to-deploy-windows-containers-to-service-fabric.md)
