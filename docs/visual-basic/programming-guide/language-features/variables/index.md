---
title: Variáveis no Visual Basic
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic]
- values [Visual Basic], storing
ms.assetid: 4cfaa06d-4ae3-4307-897b-cf599dc24caa
ms.openlocfilehash: 30baab24c54b5158da53f1ba88206d8f1564ebaf
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69953343"
---
# <a name="variables-in-visual-basic"></a>Variáveis no Visual Basic
Geralmente, você precisa armazenar valores ao executar cálculos com Visual Basic. Por exemplo, talvez você queira calcular vários valores, compará-los e executar operações diferentes dependendo do resultado da comparação. Você precisará reter os valores se desejar compará-los.  
  
## <a name="usage"></a>Uso  
 Visual Basic, assim como a maioria das linguagens de programação, usa variáveis para armazenar valores. Uma *variável* tem um nome (a palavra que você usa para se referir ao valor que a variável contém). Uma variável também tem um tipo de dados (que determina o tipo de dados que a variável pode armazenar). Se precisar armazenar um conjunto indexado de itens de dados estritamente relacionados, uma variável poderá representar uma matriz.  
  
 A inferência de tipo de variável local permite que você declare variáveis sem especificar de maneira explícita um tipo de dados. Em vez disso, o compilador infere o tipo da variável com base no tipo da expressão de inicialização. Para obter mais informações, consulte [Inferência de tipo de variável local](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md) e [Instrução Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md).  
  
## <a name="assigning-values"></a>Atribuindo valores  
 Você pode usar instruções de atribuição para executar cálculos e atribuir o resultado a uma variável, conforme mostra o exemplo a seguir.  
  
 [!code-vb[VbVbalrVariables#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrVariables/VB/Class1.vb#1)]  
  
> [!NOTE]
> O sinal de igual (`=`) no exemplo é um operador de atribuição e não um operador de igualdade. O valor é atribuído à variável `applesSold`.  
  
 Para obter mais informações, confira [Como: Mover dados para dentro e fora de uma](../../../../visual-basic/programming-guide/language-features/variables/how-to-move-data-into-and-out-of-a-variable.md)variável.  
  
## <a name="variables-and-properties"></a>Variáveis e propriedades  
 Como uma variável, uma *propriedade* representa um valor que você pode acessar. No entanto, ela é mais complexa que uma variável. Uma propriedade usa blocos de código que controlam como definir e recuperar seu valor. Para obter mais informações, consulte [Diferenças entre propriedades e variáveis no Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md).  
  
## <a name="see-also"></a>Consulte também

- [Declaração de Variável](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
- [Variáveis de Objeto](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)
- [Solução de problemas de Variáveis](../../../../visual-basic/programming-guide/language-features/variables/troubleshooting-variables.md)
- [Como: Mover dados para dentro e fora de uma variável](../../../../visual-basic/programming-guide/language-features/variables/how-to-move-data-into-and-out-of-a-variable.md)
- [Diferenças entre propriedades e variáveis no Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)
- [Inferência de Tipo de Variável Local](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
