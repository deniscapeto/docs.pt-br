---
title: Palavra-chave bool – Referência de C#
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- bool_CSharpKeyword
- bool
helpviewer_keywords:
- bool keyword [C#]
ms.assetid: 551cfe35-2632-4343-af49-33ad12da08e2
ms.openlocfilehash: 3e4e83b52cd6b275e68039693c774f6490f2b88f
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69606052"
---
# <a name="bool-c-reference"></a>bool (Referência de C#)

A palavra-chave `bool` é um alias de <xref:System.Boolean?displayProperty=nameWithType>. Ela é usada para declarar variáveis para armazenar os valores boolianos: [true](true-literal.md) e [false](false-literal.md).

> [!NOTE]
> Use o tipo `bool?`, se você precisar oferecer suporte à lógica de três valores, por exemplo, ao trabalhar com bancos de dados que dão suporte a um tipo booliano de três valores. Para os operandos `bool?`, os operadores `&` e `|` predefinidos oferecem suporte à lógica de três valores. Para obter mais informações, confira a seção [Operadores lógicos booleanos anuláveis](../operators/boolean-logical-operators.md#nullable-boolean-logical-operators) do artigo [Operadores lógicos boolianos](../operators/boolean-logical-operators.md).

## <a name="literals"></a>Literais

Você pode atribuir um valor booliano a uma variável `bool`. Você também pode atribuir uma expressão que é calculada como `bool` para um variável `bool`.

[!code-csharp[csrefKeywordsTypes#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#1)]

O valor padrão de uma variável `bool` é `false`. O valor padrão de uma variável `bool?` é `null`.

## <a name="conversions"></a>Conversões

No C++, um valor do tipo `bool` pode ser convertido em um valor do tipo `int`. Em outras palavras, `false` é equivalente a zero e `true` é equivalente a valores diferentes de zero. No C#, não há conversão entre o tipo `bool` e outros tipos. Por exemplo, a seguinte instrução `if` é inválida no C#:

[!code-csharp[csrefKeywordsTypes#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#2)]

Para testar uma variável do tipo `int`, você precisa compará-la explicitamente com um valor, como zero, da seguinte maneira:

[!code-csharp[csrefKeywordsTypes#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#3)]

## <a name="example"></a>Exemplo

Neste exemplo, você insere um caractere do teclado e o programa verifica se o caractere de entrada é uma letra. Se for uma letra, ele verificará se é maiúscula ou minúscula. Essas verificações são executadas com o <xref:System.Char.IsLetter%2A> e o <xref:System.Char.IsLower%2A>, ambos os quais retornam o tipo `bool`:

[!code-csharp[csrefKeywordsTypes#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#4)]

## <a name="c-language-specification"></a>Especificação da linguagem C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Consulte também

- [Referência de C#](../index.md)
- [Guia de Programação em C#](../../programming-guide/index.md)
- [Palavras-chave do C#](./index.md)
- [Tipos integrais](../builtin-types/integral-numeric-types.md)
- [Tabela de tipos internos](./built-in-types-table.md)
- [Tabela de conversões numéricas implícitas](./implicit-numeric-conversions-table.md)
- [Tabela de conversões numéricas explícitas](./explicit-numeric-conversions-table.md)
