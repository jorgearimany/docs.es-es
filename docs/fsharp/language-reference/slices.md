---
title: Los segmentos (F#)
description: Obtenga información sobre cómo utilizar los segmentos existentes F# tipos de datos y cómo definir sus propios segmentos para otros tipos de datos.
ms.date: 01/22/2019
ms.openlocfilehash: 1d8bb029ad18c8853ab58888959967ed279fb368
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2019
ms.locfileid: "57675282"
---
# <a name="slices"></a>Segmentos

En F#, un segmento es un subconjunto de un tipo de datos. Para poder tomar un segmento de un tipo de datos, debe definir el tipo de datos un `GetSlice` método o en un [escriba extensión](type-extensions.md) decir en ámbito. Este artículo explica cómo aprovechar los segmentos de existentes F# tipos y cómo definir las suyas propias.

Los segmentos son similares a [indizadores](members/indexed-properties.md), pero en lugar de producir un único valor de la estructura de datos subyacente, producen varias.

F#actualmente tiene compatibilidad intrínseca para dividir las cadenas, matrices, listas y matrices 2D.

## <a name="basic-slicing-with-f-lists-and-arrays"></a>Segmentación básica con F# listas y matrices

Los tipos de datos más comunes que se segmenta son F# listas y matrices. El ejemplo siguiente muestra cómo hacer esto con listas:

```fsharp
// Generate a list of 100 integers
let fullList = [ 1 .. 100 ]

// Create a slice from indices 1-5 (inclusive)
let smallSlice = fullList.[1..5]
printfn "Small slice: %A" smallSlice

// Create a slice from the beginning to index 5 (inclusive)
let unboundedBeginning = fullList.[..5]
printfn "Unbounded beginning slice: %A" unboundedBeginning

// Create a slice from an index to the end of the list
let unboundedEnd = fullList.[94..]
printfn "Unbounded end slice: %A" unboundedEnd
```

Segmentación de matrices es igual que la segmentación de listas:

```fsharp
// Generate an array of 100 integers
let fullArray = [| 1 .. 100 |]

// Create a slice from indices 1-5 (inclusive)
let smallSlice = fullArray.[1..5]
printfn "Small slice: %A" smallSlice

// Create a slice from the beginning to index 5 (inclusive)
let unboundedBeginning = fullArray.[..5]
printfn "Unbounded beginning slice: %A" unboundedBeginning

// Create a slice from an index to the end of the list
let unboundedEnd = fullArray.[94..]
printfn "Unbounded end slice: %A" unboundedEnd
```

## <a name="slicing-multidimensional-arrays"></a>Fragmentación de matrices multidimensionales

F#admite matrices multidimensionales en el F# biblioteca principal. Al igual que con las matrices unidimensionales, también pueden ser útiles sectores de matrices multidimensionales. Sin embargo, la introducción de dimensiones adicionales exige una sintaxis ligeramente diferente para que pueden tomar segmentos de columnas y filas específicas.

Los ejemplos siguientes muestran cómo segmentar una matriz 2D:

```fsharp
// Generate a 3x3 2D matrix
let A = array2D [[1;2;3];[4;5;6];[7;8;9]]
printfn "Full matrix:\n %A" A

// Take the first row
let row0 = A.[0,*]
printfn "Row 0: %A" row0

// Take the first column
let col0 = A.[*,0]
printfn "Column 0: %A" col0

// Take all rows but only two columns
let subA = A.[*,0..1]
printfn "%A" subA

// Take two rows and all columns
let subA' = A.[0..1,*]
printfn "%A" subA'

// Slice a 2x2 matrix out of the full 3x3 matrix
let twoByTwo = A.[0..1,0..1]
printfn "%A" twoByTwo
```

El F# biblioteca principal no define `GetSlice`para matrices 3D. Si desea segmentar los u otras matrices o varias dimensiones, debe definir el `GetSlice` miembro usted mismo.

## <a name="defining-slices-for-other-data-structures"></a>Definición de segmentos de otras estructuras de datos

El F# biblioteca principal define los segmentos para un conjunto limitado de tipos. Si desea definir segmentos más tipos de datos, puede hacerlo en la propia definición de tipo o en una extensión de tipo.

Por ejemplo, aquí es cómo podría definir segmentos de la <xref:System.ArraySegment%601> clase para permitir la manipulación de datos adecuada:

```fsharp
open System

type ArraySegment<'TItem> with
    member segment.GetSlice(?start, ?finish) =
        let start = defaultArg start 0
        let finish = defaultArg finish segment.Count
        ArraySegment(segment.Array, segment.Offset + start, finish - start)

let arr = ArraySegment [| 1 .. 10 |]
let slice = arr.[2..5] //[ 3; 4; 5]
```

### <a name="use-inlining-to-avoid-boxing-if-it-is-necessary"></a>Uso de inclusión para evitar la conversión boxing si es necesario

Si va a definir segmentos de un tipo que es realmente un struct, se recomienda `inline` el `GetSlice` miembro. El F# compilador optimiza los argumentos opcionales, evitando las asignaciones del montón como resultado de la segmentación. Esto es muy importante para la segmentación de construcciones como <xref:System.Span%601> que no se puede asignar en el montón.

```fsharp
open System

type Span<'T> with
    // Note the 'inline' in the member definition
    member inline sp.GetSlice(startIdx, endIdx) =
        let s = defaultArg startIdx 0
        let e = defaultArg endIdx sp.Length
        sp.Slice(s, e)

let printSpan (sp: Span<int>) =
    let arr = sp.ToArray()
    printfn "%A" arr

let sp = [| 1; 2; 3; 4; 5 |].AsSpan()
printSpan sp.[0..] // [|1; 2; 3; 4; 5|]
printSpan sp.[..5] // [|1; 2; 3; 4; 5|]
printSpan sp.[0..3] // [|1; 2; 3|]
printSpan sp.[1..2] // |2; 3|]
```

## <a name="see-also"></a>Vea también

- [Propiedades indizadas](members/indexed-properties.md)
