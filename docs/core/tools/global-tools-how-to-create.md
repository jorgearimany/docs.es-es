---
title: Creación de una herramienta global en .NET Core
description: Se describe cómo crear una herramienta global. La herramienta global es una aplicación de consola que se instala mediante la CLI de .NET Core.
author: Thraka
ms.author: adegeo
ms.date: 08/22/2018
ms.openlocfilehash: 3860aad5e2c13714298d50bb9ac10daec3aadf01
ms.sourcegitcommit: fb78d8abbdb87144a3872cf154930157090dd933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47231227"
---
# <a name="create-a-net-core-global-tool-using-the-net-core-cli"></a><span data-ttu-id="263b2-104">Creación de una herramienta global de .NET Core mediante la CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="263b2-104">Create a .NET Core Global Tool using the .NET Core CLI</span></span>

<span data-ttu-id="263b2-105">En este artículo se explica cómo crear y empaquetar una herramienta global en .NET Core.</span><span class="sxs-lookup"><span data-stu-id="263b2-105">This article teaches you how to create and package a .NET Core Global Tool.</span></span> <span data-ttu-id="263b2-106">La CLI de .NET Core permite crear una aplicación de consola como una herramienta global, que otros usuarios pueden instalar y ejecutar fácilmente.</span><span class="sxs-lookup"><span data-stu-id="263b2-106">The .NET Core CLI allows you to create a console application as a Global Tool, which others can easily install and run.</span></span> <span data-ttu-id="263b2-107">Las herramientas globales de .NET Core son paquetes de NuGet que se instalan desde la CLI de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="263b2-107">.NET Core Global Tools are NuGet packages that are installed from the .NET Core CLI.</span></span> <span data-ttu-id="263b2-108">Para más información sobre las herramientas globales, vea [Información general sobre las herramientas globales de .NET Core][global-tool-info].</span><span class="sxs-lookup"><span data-stu-id="263b2-108">For more information about Global Tools, see [.NET Core Global Tools overview][global-tool-info].</span></span>

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

## <a name="create-a-project"></a><span data-ttu-id="263b2-109">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="263b2-109">Create a project</span></span>

<span data-ttu-id="263b2-110">En este artículo se usa la CLI de .NET Core para crear y administrar un proyecto.</span><span class="sxs-lookup"><span data-stu-id="263b2-110">This article uses the .NET Core CLI to create and manage a project.</span></span>

<span data-ttu-id="263b2-111">Nuestra herramienta de ejemplo será una aplicación de consola que genera un bot de ASCII e imprime un mensaje.</span><span class="sxs-lookup"><span data-stu-id="263b2-111">Our example tool will be a console application that generates an ASCII bot and prints a message.</span></span> <span data-ttu-id="263b2-112">En primer lugar, cree una aplicación de consola de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="263b2-112">First, create a new .NET Core Console Application.</span></span>

```console
dotnet new console -o botsay
```

<span data-ttu-id="263b2-113">Navegue hasta el directorio `botsay` creado por el comando anterior.</span><span class="sxs-lookup"><span data-stu-id="263b2-113">Navigate to the `botsay` directory created by the previous command.</span></span>

## <a name="add-the-code"></a><span data-ttu-id="263b2-114">Agregar el código</span><span class="sxs-lookup"><span data-stu-id="263b2-114">Add the code</span></span>

<span data-ttu-id="263b2-115">Abra el archivo `Program.cs` con su editor de texto favorito, como `vim` o [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="263b2-115">Open the `Program.cs` file with your favorite text editor, such as `vim` or [Visual Studio Code](https://code.visualstudio.com/).</span></span>

<span data-ttu-id="263b2-116">Agregue la siguiente directiva `using` a la parte superior del archivo, ya que esto ayuda a reducir el código para mostrar la información de versión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="263b2-116">Add the following `using` directive to the top of the file, this helps shorten the code to display the version information of the application.</span></span>

```csharp
using System.Reflection;
```

<span data-ttu-id="263b2-117">A continuación, desplácese hacia abajo hasta el método `Main`.</span><span class="sxs-lookup"><span data-stu-id="263b2-117">Next, move down to the `Main` method.</span></span> <span data-ttu-id="263b2-118">Reemplace el método con el siguiente código para procesar los argumentos de la línea de comandos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="263b2-118">Replace the method with the following code to process the command-line arguments for your application.</span></span> <span data-ttu-id="263b2-119">Si no se pasa ningún argumento, se muestra un mensaje de Ayuda breve.</span><span class="sxs-lookup"><span data-stu-id="263b2-119">If no arguments were passed, a short help message is displayed.</span></span> <span data-ttu-id="263b2-120">En caso contrario, todos los argumentos se transforman en una cadena y se imprimen con el bot.</span><span class="sxs-lookup"><span data-stu-id="263b2-120">Otherwise, all of those arguments are transformed into a string and printed with the bot.</span></span>

```csharp
static void Main(string[] args)
{
    if (args.Length == 0)
    {
        var versionString = Assembly.GetEntryAssembly()
                                .GetCustomAttribute<AssemblyInformationalVersionAttribute>()
                                .InformationalVersion
                                .ToString();
                                
        Console.WriteLine($"botsay v{versionString}");
        Console.WriteLine("-------------");
        Console.WriteLine("\nUsage:");
        Console.WriteLine("  botsay <message>");
        return;
    }

    ShowBot(string.Join(' ', args));
}
```

### <a name="create-the-bot"></a><span data-ttu-id="263b2-121">Crear el bot</span><span class="sxs-lookup"><span data-stu-id="263b2-121">Create the bot</span></span>

<span data-ttu-id="263b2-122">A continuación, agregue un nuevo método denominado `ShowBot` que toma un parámetro de cadena.</span><span class="sxs-lookup"><span data-stu-id="263b2-122">Next, add a new method named `ShowBot` that takes a string parameter.</span></span> <span data-ttu-id="263b2-123">Este método imprime el mensaje y el bot de ASCII.</span><span class="sxs-lookup"><span data-stu-id="263b2-123">This method prints out the message and the ASCII bot.</span></span> <span data-ttu-id="263b2-124">El código de bot de ASCII se ha tomado del ejemplo de [dotnetbot](https://github.com/dotnet/core/blob/master/samples/dotnetsay/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="263b2-124">The ASCII bot code was taken from the [dotnetbot](https://github.com/dotnet/core/blob/master/samples/dotnetsay/Program.cs) sample.</span></span>

```csharp
static void ShowBot(string message)
{
    string bot = $"\n        {message}";
    bot += @"
    __________________
                      \
                       \
                          ....
                          ....'
                           ....
                        ..........
                    .............'..'..
                 ................'..'.....
               .......'..........'..'..'....
              ........'..........'..'..'.....
             .'....'..'..........'..'.......'.
             .'..................'...   ......
             .  ......'.........         .....
             .    _            __        ......
            ..    #            ##        ......
           ....       .                 .......
           ......  .......          ............
            ................  ......................
            ........................'................
           ......................'..'......    .......
        .........................'..'.....       .......
     ........    ..'.............'..'....      ..........
   ..'..'...      ...............'.......      ..........
  ...'......     ...... ..........  ......         .......
 ...........   .......              ........        ......
.......        '...'.'.              '.'.'.'         ....
.......       .....'..               ..'.....
   ..       ..........               ..'........
          ............               ..............
         .............               '..............
        ...........'..              .'.'............
       ...............              .'.'.............
      .............'..               ..'..'...........
      ...............                 .'..............
       .........                        ..............
        .....
";
    Console.WriteLine(bot);
}
```

### <a name="test-the-tool"></a><span data-ttu-id="263b2-125">Probar la herramienta</span><span class="sxs-lookup"><span data-stu-id="263b2-125">Test the tool</span></span>

<span data-ttu-id="263b2-126">Ejecute el proyecto y observe la salida.</span><span class="sxs-lookup"><span data-stu-id="263b2-126">Run the project and see the output.</span></span> <span data-ttu-id="263b2-127">Pruebe estas variaciones de la línea de comandos para ver resultados diferentes:</span><span class="sxs-lookup"><span data-stu-id="263b2-127">Try these variations of the command-line to see different results:</span></span>

```csharp
dotnet run
dotnet run -- "Hello from the bot"
dotnet run -- hello from the bot
```

<span data-ttu-id="263b2-128">Todos los argumentos después del delimitador `--` se pasan a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="263b2-128">All arguments after the `--` delimiter are passed to your application.</span></span>

## <a name="setup-the-global-tool"></a><span data-ttu-id="263b2-129">Configurar la herramienta global</span><span class="sxs-lookup"><span data-stu-id="263b2-129">Setup the global tool</span></span>

<span data-ttu-id="263b2-130">Antes de que pueda empaquetar y distribuir la aplicación como una herramienta global, debe modificar el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="263b2-130">Before you can pack and distribute the application as a Global Tool, you need to modify the project file.</span></span> <span data-ttu-id="263b2-131">Abra el archivo `botsay.csproj` y agregue tres nuevos nodos XML al nodo `<Project><PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="263b2-131">Open the `botsay.csproj` file and add three new XML nodes to the `<Project><PropertyGroup>` node:</span></span>

- `<PackAsTool>`  
<span data-ttu-id="263b2-132">[OBLIGATORIO] Indica que la aplicación se empaquetará para la instalación como una herramienta global.</span><span class="sxs-lookup"><span data-stu-id="263b2-132">[REQUIRED] Indicates that the application will be packaged for install as a Global Tool.</span></span>

- `<ToolCommandName>`  
<span data-ttu-id="263b2-133">[OPCIONAL] Un nombre alternativo para la herramienta; en caso contrario, el nombre del comando de la herramienta se asignará después del archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="263b2-133">[OPTIONAL] An alternative name for the tool, otherwise the command name for the tool will be named after the project file.</span></span> <span data-ttu-id="263b2-134">Puede tener varias herramientas en un paquete; elegir un nombre único y descriptivo ayuda a diferenciar de otras herramientas en el mismo paquete.</span><span class="sxs-lookup"><span data-stu-id="263b2-134">You can have multiple tools in a package, choosing a unique and friendly name helps differentiate from other tools in the same package.</span></span>

- `<PackageOutputPath>`  
<span data-ttu-id="263b2-135">[OPCIONAL] Dónde se generará el paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="263b2-135">[OPTIONAL] Where the NuGet package will be produced.</span></span> <span data-ttu-id="263b2-136">El paquete NuGet es el que las herramientas globales de la CLI de .NET Core utilizan para instalar la herramienta.</span><span class="sxs-lookup"><span data-stu-id="263b2-136">The NuGet package is what the .NET Core CLI Global Tools uses to install your tool.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.1</TargetFramework>

    <PackAsTool>true</PackAsTool>
    <ToolCommandName>botsay</ToolCommandName>
    <PackageOutputPath>./nupkg</PackageOutputPath>

  </PropertyGroup>

</Project>
```

<span data-ttu-id="263b2-137">Aunque `<PackageOutputPath>` es opcional, úselo en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="263b2-137">Even though `<PackageOutputPath>` is optional, use it in this example.</span></span> <span data-ttu-id="263b2-138">Asegúrese de que lo establece: `<PackageOutputPath>./nupkg</PackageOutputPath>`.</span><span class="sxs-lookup"><span data-stu-id="263b2-138">Make sure you set it: `<PackageOutputPath>./nupkg</PackageOutputPath>`.</span></span>

<span data-ttu-id="263b2-139">A continuación, cree un paquete NuGet para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="263b2-139">Next, create a NuGet package for your application.</span></span>

```console
dotnet pack
```

<span data-ttu-id="263b2-140">El archivo `botsay.1.0.0.nupkg` se crea en la carpeta identificada por el valor XML `<PackageOutputPath>` desde el archivo `botsay.csproj`, que en este ejemplo es la carpeta `./nupkg`.</span><span class="sxs-lookup"><span data-stu-id="263b2-140">The `botsay.1.0.0.nupkg` file is created in the folder identified by the `<PackageOutputPath>` XML value from the `botsay.csproj` file, which in this example is the `./nupkg` folder.</span></span> <span data-ttu-id="263b2-141">Esto facilita la instalación y las pruebas.</span><span class="sxs-lookup"><span data-stu-id="263b2-141">This makes it easy to install and test.</span></span> <span data-ttu-id="263b2-142">Si desea lanzar una herramienta públicamente, cárguela en [https://www.nuget.org](https://www.nuget.org).</span><span class="sxs-lookup"><span data-stu-id="263b2-142">When you want to release a tool publicly, upload it to [https://www.nuget.org](https://www.nuget.org).</span></span>

<span data-ttu-id="263b2-143">Ahora que tiene un paquete, instale la herramienta desde ese paquete:</span><span class="sxs-lookup"><span data-stu-id="263b2-143">Now that you have a package, install the tool from that package:</span></span> 

```console
dotnet tool install --global --add-source ./nupkg botsay
```

<span data-ttu-id="263b2-144">El parámetro `--add-source` indica a la CLI de .NET Core que use temporalmente la carpeta `./nupkg` (nuestra carpeta `<PackageOutputPath>`) como una fuente de origen adicional para los paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="263b2-144">The `--add-source` parameter tells the .NET Core CLI to temporarily use the `./nupkg` folder (our `<PackageOutputPath>` folder) as an additional source feed for NuGet packages.</span></span> <span data-ttu-id="263b2-145">Para más información sobre la instalación de las herramientas globales, vea [Información general sobre las herramientas globales de .NET Core][global-tool-info].</span><span class="sxs-lookup"><span data-stu-id="263b2-145">For more information about installing Global Tools, see [.NET Core Global Tools overview][global-tool-info].</span></span>

<span data-ttu-id="263b2-146">Si la instalación es correcta, se muestra un mensaje similar al siguiente con el comando que se usa para llamar a la herramienta y la versión instalada:</span><span class="sxs-lookup"><span data-stu-id="263b2-146">If installation is successful, a message is displayed showing the command used to call the tool and the version installed, similar to the following example:</span></span>

```
You can invoke the tool using the following command: botsay
Tool 'botsay' (version '1.0.0') was successfully installed.
```

<span data-ttu-id="263b2-147">Ahora podrá escribir `botsay` y obtener una respuesta de la herramienta.</span><span class="sxs-lookup"><span data-stu-id="263b2-147">You should now be able to type `botsay` and get a response from the tool.</span></span>

> [!NOTE]
> <span data-ttu-id="263b2-148">Si la instalación fue correcta, pero no se puede usar el comando `botsay`, es posible que deba abrir un terminal nuevo para actualizar la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="263b2-148">If the install was successful, but you cannot use the `botsay` command, you may need to open a new terminal to refresh the PATH.</span></span>

## <a name="remove-the-tool"></a><span data-ttu-id="263b2-149">Quitar la herramienta</span><span class="sxs-lookup"><span data-stu-id="263b2-149">Remove the tool</span></span>

<span data-ttu-id="263b2-150">Cuando haya terminado de experimentar con la herramienta, puede quitarla con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="263b2-150">Once you're done experimenting with the tool, you can remove it with the following commnand:</span></span>

```console
dotnet tool uninstall -g botsay
```

[global-tool-info]: global-tools.md