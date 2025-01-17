---
title: 'Como: Criar um procedimento (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- Visual Basic code, reusing
- procedure declarations
- procedures [Visual Basic], about procedures
ms.assetid: 4f779247-0b50-47e8-9e5c-ab5cf39ac0d2
ms.openlocfilehash: 2cf4c788ec421c1e74ef7198496a92149e049752
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216729"
---
# <a name="how-to-create-a-procedure-visual-basic"></a>Como: Criar um procedimento (Visual Basic)

Você coloca um procedimento entre uma instrução de declaração inicial`Sub` ( `Function`ou) e uma instrução de Declaração`End Sub` final `End Function`(ou). Todo o código do procedimento está entre essas instruções.

 Um procedimento não pode conter outro procedimento, portanto, suas instruções de início e término devem estar fora de qualquer outro procedimento.

 Se você tiver um código que executa a mesma tarefa em locais diferentes, você pode gravar a tarefa uma vez como um procedimento e, em seguida, chamá-la de diferentes locais em seu código.

### <a name="to-create-a-procedure-that-does-not-return-a-value"></a>Para criar um procedimento que não retorna um valor

1. Fora de qualquer outro procedimento, use `Sub` uma instrução, seguida por `End Sub` uma instrução.

2. Na instrução, siga a `Sub` palavra-chave com o nome do procedimento e, em seguida, a lista de parâmetros entre parênteses. `Sub`

3. Coloque as instruções de código do procedimento entre `Sub` as `End Sub` instruções e.

### <a name="to-create-a-procedure-that-returns-a-value"></a>Para criar um procedimento que retorna um valor

1. Fora de qualquer outro procedimento, use `Function` uma instrução, seguida por `End Function` uma instrução.

2. Na instrução, siga a `Function` palavra-chave com o nome do procedimento, em seguida, a lista de parâmetros entre parênteses e `As` , em seguida, uma cláusula especificando o tipo de dados do valor de retorno. `Function`

3. Coloque as instruções de código do procedimento entre `Function` as `End Function` instruções e.

4. Use uma `Return` instrução para retornar o valor para o código de chamada.

### <a name="to-connect-your-new-procedure-with-the-old-repetitive-blocks-of-code"></a>Para conectar seu novo procedimento com os blocos de código antigos e repetitivos

1. Certifique-se de definir o novo procedimento em um local onde o código antigo tenha acesso a ele.

2. No seu bloco de código repetitivo antigo, substitua as instruções que executam a tarefa repetitiva com uma única instrução que `Sub` chama `Function` o procedimento or.

3. Se o procedimento for um `Function` que retorna um valor, verifique se a instrução de chamada executa uma ação com o valor retornado, como armazená-lo em uma variável ou se o valor será perdido.

## <a name="example"></a>Exemplo

 O procedimento `Function` a seguir calcula o lado mais longo, ou hipotenusa, de um triângulo à direita, dado os valores para os outros dois lados:

 [!code-vb[VbVbcnProcedures#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#1)]

## <a name="see-also"></a>Consulte também

- [Procedimentos](index.md)
- [Subprocedimentos](sub-procedures.md)
- [Procedimentos de Função](function-procedures.md)
- [Procedimentos de Propriedade](property-procedures.md)
- [Procedimentos de Operador](operator-procedures.md)
- [Parâmetros e Argumentos de Procedimento](procedure-parameters-and-arguments.md)
- [Procedimentos Recursivos](recursive-procedures.md)
- [Sobrecarga de Procedimento](procedure-overloading.md)
- [Objetos e Classes](../objects-and-classes/index.md)
- [Programação orientada a objeto (Visual Basic)](../../concepts/object-oriented-programming.md)
