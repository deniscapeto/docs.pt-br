---
title: Palavra-chave protected – Referência de C#
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- protected
- protected_CSharpKeyword
helpviewer_keywords:
- protected keyword [C#]
ms.assetid: 05ce3794-6675-4025-bddb-eaaa0ec22892
ms.openlocfilehash: a0420dd10d81c4ae893ab0447244a611091ed7b0
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69601978"
---
# <a name="protected-c-reference"></a>protected (Referência de C#)

A palavra-chave `protected` é um modificador de acesso de membro.

 > Esta página aborda o acesso `protected`. A palavra-chave `protected` também faz parte dos modificadores de acesso [`protected internal`](protected-internal.md) e [`private protected`](private-protected.md).

Um membro protegido é acessível dentro de sua classe e por instâncias da classe derivada.

Para obter uma comparação de `protected` com os outros modificadores de acesso, consulte [Níveis de acessibilidade](accessibility-levels.md).

## <a name="example"></a>Exemplo

Um membro protegido de uma classe base será acessível em uma classe derivada somente se o acesso ocorrer por meio do tipo da classe derivada. Por exemplo, considere o seguinte segmento de código:

[!code-csharp[csrefKeywordsModifiers#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#11)]

A instrução `a.x = 10` gera um erro porque ela é feita dentro do método estático Main e não em uma instância da classe B.

Membros de struct não podem ser protegidos porque o struct não pode ser herdado.

## <a name="example"></a>Exemplo

Nesse exemplo, a classe `DerivedPoint` é derivada de `Point`. Portanto, você pode acessar os membros protegidos da classe base diretamente da classe derivada.

[!code-csharp[csrefKeywordsModifiers#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#12)]  

Se você alterar os níveis de acesso de `x` e `y` para [private](private.md), o compilador emitirá as mensagens de erro:

`'Point.y' is inaccessible due to its protection level.`

`'Point.x' is inaccessible due to its protection level.`

## <a name="c-language-specification"></a>Especificação da linguagem C#  

Para obter mais informações, veja [Acessibilidade declarada](~/_csharplang/spec/basic-concepts.md#declared-accessibility) na [Especificação da Linguagem C#](../language-specification/index.md). A especificação da linguagem é a fonte definitiva para a sintaxe e o uso de C#.

## <a name="see-also"></a>Consulte também

- [Referência de C#](../index.md)
- [Guia de Programação em C#](../../programming-guide/index.md)
- [Palavras-chave do C#](index.md)
- [Modificadores de acesso](access-modifiers.md)
- [Níveis de acessibilidade](accessibility-levels.md)
- [Modificadores](modifiers.md)
- [public](public.md)
- [private](private.md)
- [internal](internal.md)
- [Questões de segurança de palavras-chave virtuais internas](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/heyd8kky(v=vs.100))
