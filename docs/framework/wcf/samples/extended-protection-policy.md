---
title: Directiva de protección extendida
ms.date: 03/30/2017
ms.assetid: e2616a10-317e-4c34-8023-0c015a80a82f
ms.openlocfilehash: 645b48b3c7ce3daaaedac372ba5ba6fd5edfc8f8
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59768428"
---
# <a name="extended-protection-policy"></a>Directiva de protección extendida
Protección extendida es una iniciativa de seguridad para protegerse contra los ataques de tipo "Man in the middle" (MITM). Un ataque MITM es una amenaza de seguridad en la que MITM toma las credenciales de un cliente y lo reenvía a un servidor.  
  
## <a name="demonstrates"></a>Demostraciones  
 Protección extendida  
  
## <a name="discussion"></a>Discusión  
 Cuando las aplicaciones cliente se autentican mediante Kerberos, Digest o NTLM usando HTTPS, se establece en primer lugar un canal de Seguridad de nivel de transporte (TLS) y después la autenticación se lleva a cabo usando el canal seguro. Sin embargo, no hay ningún enlace entre la clave de sesión generada por SSL y la clave de sesión generada durante la autenticación. MITM se puede establecer entre el cliente y el servidor, y comienza a reenviar las solicitudes del cliente, incluso cuando el propio canal de transporte es seguro, porque el servidor no tiene ninguna manera de saber si el canal seguro se ha establecido desde el cliente o desde un MITM. La solución en este escenario es enlazar el canal de TLS externo con el canal de autenticación interno de modo que el servidor puede detectar si hay un MITM.  
  
> [!NOTE]
>  Este ejemplo solo funciona cuando se hospeda en IIS y no puede trabajar en Cassini. El servidor de desarrollo de Visual Studio porque Cassini no admite HTTPS.  
  
> [!NOTE]
>  Esta característica solo está disponible actualmente en Windows 7. Los siguientes pasos son específicos de Windows 7.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Configurar, compilar y ejecutar el ejemplo  
  
1. Instalar Internet Information Services de **Panel de Control**, **agregar o quitar programas**, **características de Windows**.  
  
2. Instalar **Windows autenticación** en **características de Windows**, **Internet Information Services**, **servicios World Wide Web**,  **Seguridad**, y **Windows autenticación**.  
  
3. Instalar **activación de Windows Communication Foundation HTTP** en **características de Windows**, **Microsoft .NET Framework 3.5.1**, y **comunicación de Windows Activación HTTP Foundation**.  
  
4. Este ejemplo requiere que el cliente establezca un canal seguro con el servidor, por lo que es necesaria la presencia de un certificado de servidor que se puede instalar desde el Administrador de Internet Information Services (IIS).  
  
    1.  Abra el Administrador de IIS. Abra **certificados de servidor**, que aparece en el **característica vista** pestaña cuando se selecciona el nodo raíz (nombre de equipo).  
  
    2.  Para las pruebas de este ejemplo, puede crear un certificado autofirmado. Si no desea que Internet Explorer le indique que el certificado no es seguro, instálelo en el almacén Entidades emisoras de certificados raíz de confianza.  
  
5. Abra el **acciones** panel para el sitio Web predeterminado. Haga clic en **editar sitio**, **enlaces**. Agregue HTTPS como un tipo si no está presente, con el número de puerto 443. Asigne el certificado SSL creado en el paso anterior.  
  
6. Compile el servicio. De esta forma se crea un directorio virtual en IIS y se copian los archivos .dll, .svc y .config, tal y como se requiere para que el servicio se hospede en web.  
  
7. Abra el Administrador de IIS. Haga clic en el directorio virtual (**ExtendedProtection**), que se creó en el paso anterior. Seleccione **convertir en aplicación**.  
  
8. Abra el **autenticación** módulo en el Administrador de IIS para este directorio virtual y habilite **autenticación de Windows**.  
  
9. Abra **configuración avanzada** en **autenticación de Windows** para este directorio virtual y establézcalo en **necesario**.  
  
10. Puede probar el servicio teniendo acceso a la dirección URL HTTPS de una ventana del explorador (proporcione un nombre de dominio completo). Si desea tener acceso a esta dirección URL desde un equipo remoto, asegúrese de que el firewall está abierto para todas las conexiones HTTP y HTTPS entrantes.  
  
11. Abra el archivo de configuración del cliente y proporcione un nombre de dominio completo para el cliente o el atributo de dirección de punto de conexión que reemplace a `<<full_machine_name>>`.  
  
12. Ejecute el cliente. El cliente se comunica con el servicio, que establece un canal seguro y utiliza la protección extendida.  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo. Compruebe el siguiente directorio (predeterminado) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a [Windows Communication Foundation (WCF) y Windows Workflow Foundation (WF) Samples para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los Windows Communication Foundation (WCF) y [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ejemplos. Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Security\ExtendedProtection`
