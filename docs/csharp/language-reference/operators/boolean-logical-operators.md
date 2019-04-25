---
title: 'Operadores lógicos booleanos: referencia de C#'
description: Obtenga información sobre los operadores de C# que realizan operaciones lógicas de negación, conjunción (AND) y disyunción inclusiva y exclusiva (OR) con operandos booleanos.
ms.date: 04/08/2019
author: pkulikov
f1_keywords:
- '!_CSharpKeyword'
- '&_CSharpKeyword'
- ^_CSharpKeyword
- '|_CSharpKeyword'
- '&&_CSharpKeyword'
- '||_CSharpKeyword'
helpviewer_keywords:
- logical operators [C#]
- short-circuiting operators [C#]
- logical negation operator [C#]
- NOT operator [C#]
- '! operator [C#]'
- AND operator [C#]
- ampersand operator [C#]
- conjunction operator [C#]
- '& operator [C#]'
- exclusive OR operator [C#]
- XOR operator [C#]
- ^ operator [C#]
- OR operator [C#]
- disjunction operator [C#]
- '| operator [C#]'
- conditional AND operator [C#]
- short-circuiting AND operator [C#]
- '&& operator [C#]'
- conditional OR operator [C#]
- short-circuiting OR operator [C#]
- '|| operator [C#]'
ms.openlocfilehash: de621b26334bbc9679ba7e48a9d5a0cbaec67eab
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59427323"
---
# <a name="boolean-logical-operators-c-reference"></a>Operadores lógicos booleanos (referencia de C#)

Los operandos siguientes realizan operaciones lógicas con los operandos [bool](../keywords/bool.md):

- Operador unario [`!` (negación lógica)](#logical-negation-operator-).
- Operadores binarios [`&` (AND lógico)](#logical-and-operator-), [`|` (OR lógico)](#logical-or-operator-) y [`^` (OR exclusivo lógico)](#logical-exclusive-or-operator-). Esos operadores siempre evalúan ambos operandos.
- Operadores binarios [`&&` (AND lógico condicional)](#conditional-logical-and-operator-) y [`||` (OR lógico condicional)](#conditional-logical-or-operator-). Esos operadores evalúan el segundo operando solo si es necesario.

Para los operandos de tipos [de datos enteros](../keywords/integral-types-table.md), los operadores `&`, `|` y `^` realizan operaciones lógicas bit a bit.

## <a name="logical-negation-operator-"></a>Operador de negación lógico !

El operador `!` calcula la negación lógica de su operando. Es decir, genera `true`, si el operando se evalúa como `false`, y `false`, si el operando se evalúa como `true`:

[!code-csharp-interactive[logical negation](~/samples/snippets/csharp/language-reference/operators/LogicalOperators.cs#Negation)]

## <a name="logical-and-operator-amp"></a>Operador AND lógico &amp;

El operador `&` calcula el operador AND lógico de sus operandos. El resultado de `x & y` es `true` si `x` y `y` se evalúan como `true`. De lo contrario, el resultado es `false`.

El operador `&` evalúa ambos, incluso aunque el primero se evalúe como `false`, de modo que el resultado debe ser `false` con independencia del valor del segundo operando.

En el ejemplo siguiente, el segundo operando del operador `&` es una llamada de método, que se realiza independientemente del valor del primer operando:

[!code-csharp-interactive[logical AND](~/samples/snippets/csharp/language-reference/operators/LogicalOperators.cs#And)]

El [operador AND lógico condicional](#conditional-logical-and-operator-) `&&` también calcula el operador AND lógico de sus operandos, pero no evalúa el segundo operando si el primero se evalúa como `false`.

En el caso de los operandos de tipos de datos enteros, el operador `&` calcula el operador [AND lógico bit a bit](and-operator.md#integer-logical-bitwise-and-operator) de sus operandos. El operador `&` unario es el [operador address-of](and-operator.md#unary-address-of-operator).

## <a name="logical-exclusive-or-operator-"></a>Operador OR exclusivo lógico ^

El operador `^` calcula el operador OR exclusivo lógica, también conocido como el operador XOR lógico, de sus operandos. El resultado de `x ^ y` es `true` si `x` se evalúa como `true` y `y` se evalúa como `false` o `x` se evalúa como `false` y `y` se evalúa como `true`. De lo contrario, el resultado es `false`. Es decir, para los operandos `bool`, el operador `^` calcula el mismo resultado como el [operador de desigualdad](equality-operators.md#inequality-operator-) `!=`.

[!code-csharp-interactive[logical exclusive OR](~/samples/snippets/csharp/language-reference/operators/LogicalOperators.cs#Xor)]

En el caso de los operandos de tipos de datos enteros, el operador `^` calcula el operador [OR exclusivo lógico bit a bit](xor-operator.md) de sus operandos.

## <a name="logical-or-operator-"></a>Operador lógico OR |

El operador `|` calcula el operador OR lógico de sus operandos. El resultado de `x | y` es `true` si `x` o `y` se evalúan como `true`. De lo contrario, el resultado es `false`.

El operador `|` evalúa ambos, incluso aunque el primero se evalúe como `true`, de modo que el resultado debe ser `true` con independencia del valor del segundo operando.

En el ejemplo siguiente, el segundo operando del operador `|` es una llamada de método, que se realiza independientemente del valor del primer operando:

[!code-csharp-interactive[logical OR](~/samples/snippets/csharp/language-reference/operators/LogicalOperators.cs#Or)]

El [operador OR lógico condicional](#conditional-logical-or-operator-) `||` también calcula el operador OR lógico de sus operandos, pero no evalúa el segundo operando si el primero se evalúa como `true`.

En el caso de los operados de tipos de datos enteros, el operador `|` calcula el operador [OR lógico bit a bit](or-operator.md) de sus operandos.

## <a name="conditional-logical-and-operator-ampamp"></a>Operador AND lógico condicional &amp;&amp;

El operador AND lógico condicional `&&`, también denominado operador AND lógico "de cortocircuito", calcula el operador AND lógico de sus operandos. El resultado de `x && y` es `true` si `x` y `y` se evalúan como `true`. De lo contrario, el resultado es `false`. Si el primer operando se evalúa como `false`, no se evalúa el segundo operando.

En el ejemplo siguiente, el segundo operando del operador `&&` es una llamada de método, que no se realiza si el primer operando se evalúa como `false`:

[!code-csharp-interactive[conditional logical AND](~/samples/snippets/csharp/language-reference/operators/LogicalOperators.cs#ConditionalAnd)]

El [operador AND lógico](#logical-and-operator-) `&` también calcula el operador AND lógico de sus operandos, pero siempre evalúa ambos operandos.

## <a name="conditional-logical-or-operator-"></a>Operador OR lógico condicional ||

El operador OR lógico condicional `||`, también denominado operador OR lógico "de cortocircuito", calcula el operador OR lógico de sus operandos. El resultado de `x || y` es `true` si `x` o `y` se evalúan como `true`. De lo contrario, el resultado es `false`. Si el primer operando se evalúa como `true`, no se evalúa el segundo operando.

En el ejemplo siguiente, el segundo operando del operador `||` es una llamada de método, que no se realiza si el primer operando se evalúa como `true`:

[!code-csharp-interactive[conditional logical OR](~/samples/snippets/csharp/language-reference/operators/LogicalOperators.cs#ConditionalOr)]

El [operador OR lógico](#logical-or-operator-) `|` también calcula el operador OR lógico de sus operandos, pero siempre evalúa ambos operandos.

## <a name="nullable-boolean-logical-operators"></a>Operadores lógicos booleanos que aceptan valores NULL

En el caso de los operandos `bool?`, los operadores `&` y `|` admiten la lógica de tres valores. La semántica de estos operadores se define en la tabla siguiente:  
  
|x|y|x e y|x&#124;y|  
|----|----|----|----|  
|true|true|true|true|  
|true|False|false|true|  
|true|nulo|nulo|true|  
|False|true|False|true|  
|False|False|False|False|  
|False|nulo|False|nulo|  
|nulo|true|nulo|true|  
|nulo|False|False|nulo|  
|nulo|nulo|nulo|nulo|  

El comportamiento de esos operadores difiere del comportamiento típico del operador con tipos de valor que aceptan valores NULL. Por lo general, un operador que se define para los operandos de un tipo de valor también se puede usar con los operandos del tipo de valor que acepta valores NULL correspondientes. Este tipo de operador genera `null` si alguno de sus operandos es `null`. Sin embargo, los operadores `&` y `|` pueden generar un valor no NULL incluso si uno de los operandos es `null`. Para más información sobre el comportamiento de los operandos con tipos de valor que aceptan valores NULL, consulte la sección [Operadores](../../programming-guide/nullable-types/using-nullable-types.md#operators) del artículo [Uso de tipos que aceptan valores NULL](../../programming-guide/nullable-types/using-nullable-types.md).

También puede usar los operadores `!` y `^` con los operandos `bool?`, como se muestra en el ejemplo siguiente:

[!code-csharp-interactive[lifted negation and xor](~/samples/snippets/csharp/language-reference/operators/LogicalOperators.cs#WithNullableBoolean)]

Los operadores lógicos condicionales `&&` y `||` no admiten los operandos `bool?`.

## <a name="compound-assignment"></a>Asignación compuesta

Para un operador binario `op`, una expresión de asignación compuesta con el formato

```csharp
x op= y
```

es equivalente a

```csharp
x = x op y
```

salvo que `x` solo se evalúa una vez.

Los operadores `&`, `|` y `^` admiten la asignación compuesta, como se muestra en el ejemplo siguiente:

[!code-csharp-interactive[compound assignment](~/samples/snippets/csharp/language-reference/operators/LogicalOperators.cs#CompoundAssignment)]

Los operadores lógicos condicionales `&&` y `||` no admiten la asignación compuesta.

## <a name="operator-precedence"></a>Prioridad de operadores

En la lista siguiente se ordenan los operadores lógicos desde la prioridad más alta a la más baja:

- Operador de negación lógico `!`
- Operador AND lógico `&`
- Operador OR exclusivo lógico `^`
- Operador OR lógico `|`
- Operador AND lógico condicional `&&`
- Operador OR lógico condicional `||`

Use los paréntesis, `()`, para cambiar el orden de evaluación impuesto por la prioridad de los operadores:

[!code-csharp-interactive[operator precedence](~/samples/snippets/csharp/language-reference/operators/LogicalOperators.cs#Precedence)]

Para obtener la lista completa de los operadores de C# ordenados por nivel de prioridad, vea [Operadores de C#](index.md).

## <a name="operator-overloadability"></a>Posibilidad de sobrecarga del operador

Un tipo definido por el usuario puede [sobrecargar](../keywords/operator.md) los operadores `!`, `&`, `|` y `^`. Cuando se sobrecarga un operador binario, también se sobrecarga de forma implícita el operador de asignación compuesta correspondiente. Un tipo definido por el usuario no puede sobrecargar de forma explícita un operador de asignación compuesta.

Un tipo definido por el usuario no puede sobrecargar los operadores lógicos condicionales `&&` y `||`. Sin embargo, si un tipo definido por el usuario sobrecarga los [operadores true y false](../keywords/true-false-operators.md) y el operador `&` o `|` de cierta manera, la operación `&&` o `||`, respectivamente, se puede evaluar para los operandos de ese tipo. Para obtener más información, vea la sección [Operadores lógicos condicionales definidos por el usuario](~/_csharplang/spec/expressions.md#user-defined-conditional-logical-operators) de la [Especificación del lenguaje C#](~/_csharplang/spec/introduction.md).

## <a name="c-language-specification"></a>Especificación del lenguaje C#

Para más información, vea las secciones siguientes de la [Especificación del lenguaje C#](~/_csharplang/spec/introduction.md):

- [Operador de negación lógico](~/_csharplang/spec/expressions.md#logical-negation-operator)
- [Operadores lógicos](~/_csharplang/spec/expressions.md#logical-operators)
- [Operadores lógicos condicionales](~/_csharplang/spec/expressions.md#conditional-logical-operators)

## <a name="see-also"></a>Vea también

- [Referencia de C#](../index.md)
- [Guía de programación de C#](../../programming-guide/index.md)
- [Operadores de C#](index.md)
