---
title: Delegados (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- delegates [Visual Basic]
- Visual Basic code, delegates
ms.assetid: 410b60dc-5e60-4ec0-bfae-426755a2ee28
ms.openlocfilehash: b3f333f1714a66a8ff462000385af92cf343a19e
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2019
ms.locfileid: "57674034"
---
# <a name="delegates-visual-basic"></a>Delegados (Visual Basic)

Los delegados son objetos que hacen referencia a métodos. A veces se describen como *punteros de función con seguridad de tipos* porque son similares a los punteros de función utilizados en otros lenguajes de programación. Pero a diferencia de los punteros de función, los delegados de Visual Basic son un tipo de referencia basado en la clase <xref:System.Delegate?displayProperty=nameWithType>. Los delegados pueden hacer referencia a los métodos compartidos, métodos a los que se puede llamar sin una instancia específica de una clase, y a los métodos de instancia.

## <a name="delegates-and-events"></a>Delegados y eventos

Los delegados son útiles en situaciones donde es necesario un intermediario entre un procedimiento que realiza la llamada y el procedimiento que la recibe. Por ejemplo, puede que necesite un objeto que provoca que los eventos puedan llamar a controladores de eventos diferentes en distintas circunstancias. Lamentablemente, el objeto que provoca los eventos no puede conocer de antemano qué controlador de eventos controla un evento específico. Visual Basic permite controladores de eventos dinámicamente asociar con eventos mediante la creación de un delegado para cuando se usa el `AddHandler` instrucción. En tiempo de ejecución, el delegado reenvía las llamadas al controlador de eventos adecuado.

Aunque puede crear a sus propios delegados, en muchos casos, Visual Basic crea al delegado y se encarga de los detalles por usted. Por ejemplo, una instrucción `Event` define implícitamente una clase delegada denominada `<EventName>EventHandler` como una clase anidada de la clase que contiene la instrucción `Event`, y con la misma firma que el evento. La instrucción `AddressOf` crea implícitamente una instancia de un delegado que hace referencia a un procedimiento específico. Las dos líneas de código siguientes son equivalentes. En la primera línea, verá que la creación explícita de una instancia de `EventHandler`, con una referencia al método `Button1_Click` enviada como argumento. La segunda línea es una manera más práctica de conseguir el mismo resultado.

[!code-vb[VbVbalrDelegates#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#6)]

Puede utilizar la forma abreviada para crear delegados en cualquier lugar en que el compilador puede determinar el tipo de delegado en función del contexto.

## <a name="declaring-events-that-use-an-existing-delegate-type"></a>Declaración de eventos que usan un tipo de delegado existente

En algunas situaciones, puede declarar un evento para utilizar un tipo de delegado existente como su delegado subyacente. La sintaxis siguiente muestra cómo:

[!code-vb[VbVbalrDelegates#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#7)]

Esto es útil cuando desea enrutar diversos eventos hacia el mismo controlador.

## <a name="delegate-variables-and-parameters"></a>Variables y parámetros delegados

Puede utilizar delegados para otras tareas relacionadas sin eventos, como un subproceso libre, o con procedimientos que necesiten llamar a diferentes versiones de funciones en tiempo de ejecución.

Por ejemplo, suponga que tiene una aplicación de anuncios clasificados que incluye un cuadro de lista con los nombres de los automóviles. Los anuncios se ordenan por título, que suele ser la marca del automóvil. Se puede plantear un problema si algunos coches incluyen el año del automóvil antes de la marca. El problema es que la funcionalidad de ordenación integrada del cuadro de lista ordena únicamente por códigos de caracteres; coloca todos los anuncios que empiezan con las fechas primero, seguidos de los anuncios que empiezan con la marca.

Para solucionar este problema, puede crear un procedimiento de ordenación en una clase que usa la ordenación alfabética estándar en la mayoría de los cuadros de lista, pero puede cambiar en tiempo de ejecución al procedimiento de ordenación personalizado para los anuncios de los automóviles. Para ello, pasa el procedimiento de ordenación personalizado a la clase de ordenación en tiempo de ejecución, mediante el uso de delegados.

## <a name="addressof-and-lambda-expressions"></a>Expresiones lambda y AddressOf

Cada clase delegada define un constructor que se pasa la especificación de un método de objeto. Un argumento para un constructor delegado debe ser una referencia a un método o una expresión lambda.

Para especificar una referencia a un método, utilice la siguiente sintaxis:

`AddressOf` [`expression`.]`methodName`

El tipo de tiempo de compilación de `expression` debe ser el nombre de una clase o una interfaz que contiene un método del nombre especificado cuya firma coincida con la firma de la clase delegada. `methodName` puede ser un método compartido o un método de instancia. `methodName` no es opcional, incluso si se crea un delegado para el método predeterminado de la clase.

Para especificar una expresión lambda, utilice la siguiente sintaxis:

`Function` ([`parm` As `type`, `parm2` As `type2`, ...]) `expression`

En el ejemplo siguiente se muestran las expresiones lambda y `AddressOf` usadas para especificar la referencia de un delegado.

[!code-vb[VbVbalrDelegates#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class2.vb#15)]

La firma de la función debe coincidir con la del tipo de delegado. Para obtener más información sobre las expresiones lambda, vea [Expresiones lambda](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md). Para obtener más ejemplos de expresión lambda y asignaciones de `AddressOf` a delegados, vea [Conversión de delegado flexible](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md).

## <a name="related-topics"></a>Temas relacionados

|Título|Descripción|
|-----------|-----------------|
|[Cómo: Invocar un método delegado](../../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)|Proporciona un ejemplo que muestra cómo asociar un método a un delegado y después invocar ese método a través del delegado.|
|[Cómo: Pasar procedimientos a otro procedimiento en Visual Basic](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)|Muestra cómo utilizar los delegados para pasar un procedimiento a otro procedimiento.|
|[Conversión de delegado flexible](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)|Describe cómo asignar subfunciones y funciones a delegados o controladores incluso cuando sus firmas no son idénticas.|
|[Eventos](../../../../visual-basic/programming-guide/language-features/events/index.md)|Proporciona información general sobre eventos en Visual Basic.|
