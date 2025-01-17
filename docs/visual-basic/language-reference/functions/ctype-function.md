---
title: Função CType (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.CType
helpviewer_keywords:
- expression conversion results
- explicit data type conversions [Visual Basic]
- CType function
- conversions [Visual Basic], expression
ms.assetid: dd4b29e7-6fa1-428c-877e-69955420bb72
ms.openlocfilehash: 4a0391b0a5d76f36803b433369d4832c02b05e09
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71592104"
---
# <a name="ctype-function-visual-basic"></a>Função CType (Visual Basic)

Retorna o resultado da conversão explícita de uma expressão para um tipo de dados, objeto, estrutura, classe ou interface especificado.

## <a name="syntax"></a>Sintaxe

```vb
CType(expression, typename)
```

## <a name="parts"></a>Partes

`expression` qualquer expressão válida. Se o valor de `expression` estiver fora do intervalo permitido por `typename`, Visual Basic lançará uma exceção.

`typename` qualquer expressão que seja válida em uma cláusula `As` em uma instrução `Dim`, ou seja, o nome de qualquer tipo de dados, objeto, estrutura, classe ou interface.

## <a name="remarks"></a>Comentários

> [!TIP]
> Você também pode usar as seguintes funções para executar uma conversão de tipo:
>
> - Funções de conversão de tipo, como `CByte`, `CDbl` e `CInt` que executam uma conversão para um tipo de dados específico. Para obter mais informações, consulte [funções de conversão de tipo](../../../visual-basic/language-reference/functions/type-conversion-functions.md).
> - [Operador DirectCast](../../../visual-basic/language-reference/operators/directcast-operator.md) ou [Operador TryCast](../../../visual-basic/language-reference/operators/trycast-operator.md). Esses operadores exigem que um tipo herde ou implemente o outro tipo. Eles podem fornecer um desempenho um pouco melhor do que `CType` ao converter de e para o tipo de dados `Object`.

`CType` é compilado em linha, o que significa que o código de conversão faz parte do código que avalia a expressão. Em alguns casos, o código é executado mais rapidamente porque nenhum procedimento é chamado para executar a conversão.

Se nenhuma conversão for definida de `expression` para `typename` (por exemplo, de `Integer` a `Date`), Visual Basic exibirá uma mensagem de erro de tempo de compilação.

Se uma conversão falhar em tempo de execução, a exceção apropriada será lançada. Se uma conversão de restrição falhar, um <xref:System.OverflowException> será o resultado mais comum. Se a conversão for indefinida, um <xref:System.InvalidCastException> em lançada. Por exemplo, isso pode acontecer se `expression` for do tipo `Object` e seu tipo de tempo de execução não tiver nenhuma conversão para `typename`.

Se o tipo de dados de `expression` ou `typename` for uma classe ou estrutura que você definiu, você poderá definir `CType` nessa classe ou estrutura como um operador de conversão. Isso faz com que `CType` atue como um *operador sobrecarregado*. Se você fizer isso, poderá controlar o comportamento de conversões de e para sua classe ou estrutura, incluindo as exceções que podem ser geradas.

## <a name="overloading"></a>Sobrecarga

O operador `CType` também pode ser sobrecarregado em uma classe ou estrutura definida fora do seu código. Se o seu código converter para ou de uma classe ou estrutura desse tipo, certifique-se de entender o comportamento de seu operador `CType`. Para obter mais informações, consulte [procedimentos de operador](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).

## <a name="converting-dynamic-objects"></a>Convertendo objetos dinâmicos

As conversões de tipo de objetos dinâmicos são executadas por conversões dinâmicas definidas pelo usuário que usam os métodos <xref:System.Dynamic.DynamicObject.TryConvert%2A> ou <xref:System.Dynamic.DynamicMetaObject.BindConvert%2A>. Se você estiver trabalhando com objetos dinâmicos, use o método <xref:Microsoft.VisualBasic.Conversion.CTypeDynamic%2A> para converter o objeto dinâmico.

## <a name="example"></a>Exemplo

O exemplo a seguir usa a função `CType` para converter uma expressão no tipo de dados `Single`.

[!code-vb[VbVbalrFunctions#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#24)]

Para obter exemplos adicionais, consulte [conversões implícitas e explícitas](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md).

## <a name="see-also"></a>Consulte também

- <xref:System.OverflowException>
- <xref:System.InvalidCastException>
- [Funções de Conversão do Tipo](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [Funções de Conversão](../../../visual-basic/language-reference/functions/conversion-functions.md)
- [Instrução Operator](../../../visual-basic/language-reference/statements/operator-statement.md)
- [Como: Definir um operador de conversão @ no__t-0
- [Conversão de tipos no .NET Framework](../../../standard/base-types/type-conversion.md)
