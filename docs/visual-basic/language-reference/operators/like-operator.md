---
title: Operador Like (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- Like
- vb.Like
helpviewer_keywords:
- similar to
- pattern matching
- Like operator [Visual Basic]
- '? symbol, wildcard character'
- string comparison [Visual Basic], Like operator
- strings [Visual Basic], comparing
- comparison operators [Visual Basic]
- symbols, wildcard
- wildcards, Like operator
- strings [Visual Basic], matching
- string comparison [Visual Basic], sorting data
- data [Visual Basic], sorting
- text [Visual Basic], comparing
- operators [Visual Basic], pattern-matching
- data [Visual Basic], string comparisons
- string comparison [Visual Basic], Like operators
ms.assetid: 966283ec-80e2-4294-baa8-c75baff804f9
ms.openlocfilehash: 795ecc2e80d57af29ccd50c50d2dd209c6425e40
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701131"
---
# <a name="like-operator-visual-basic"></a>Operador Like (Visual Basic)
Compara uma cadeia de caracteres com um padrão.  

> [!IMPORTANT]
> No momento, não há suporte para o operador `Like` no .NET Core e .NET Standard projetos.

## <a name="syntax"></a>Sintaxe  
  
```vb  
result = string Like pattern  
```  
  
## <a name="parts"></a>Partes  
 `result`  
 Necessário. Qualquer variável `Boolean`. O resultado é um valor `Boolean` indicando se o `string` satisfaz ou não o `pattern`.  
  
 `string`  
 Necessário. Qualquer expressão de `String` .  
  
 `pattern`  
 Necessário. Qualquer expressão `String` que esteja de acordo com as convenções de correspondência de padrões descritas em "Comentários".  
  
## <a name="remarks"></a>Comentários  
 Se o valor em `string` satisfizer o padrão contido em `pattern`, `result` será `True`. Se a cadeia de caracteres não atender ao padrão, `result` será `False`. Se `string` e `pattern` forem cadeias de caracteres vazias, o resultado será `True`.  
  
## <a name="comparison-method"></a>Método de comparação  
 O comportamento do operador `Like` depende da [instrução Option Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md). O método de comparação de cadeia de caracteres padrão para cada arquivo de origem é `Option Compare Binary`.  
  
## <a name="pattern-options"></a>Opções de padrão  
 A correspondência de padrões internos fornece uma ferramenta versátil para comparações de cadeias de caracteres. Os recursos de correspondência de padrões permitem que você corresponda a cada caractere em `string` em um caractere específico, um caractere curinga, uma lista de caracteres ou um intervalo de caracteres. A tabela a seguir mostra os caracteres permitidos no `pattern` e o que eles correspondem.  
  
|Caracteres no `pattern`|Correspondências no `string`|  
|-----------------------------|-------------------------|  
|`?`|Qualquer caractere único|  
|`*`|Zero ou mais caracteres|  
|`#`|Qualquer dígito único (0 a 9)|  
|`[charlist]`|Qualquer caractere único no `charlist`|  
|`[!charlist]`|Qualquer caractere único que não esteja em `charlist`|  
  
## <a name="character-lists"></a>Listas de caracteres  
 Um grupo de um ou mais caracteres (`charlist`) entre colchetes (`[ ]`) pode ser usado para corresponder a qualquer caractere único no `string` e pode incluir quase qualquer código de caractere, incluindo dígitos.  
  
 Um ponto de exclamação (`!`) no início de `charlist` significa que uma correspondência será feita se qualquer caractere, exceto os caracteres em `charlist`, for encontrado em `string`. Quando usados fora dos colchetes, o ponto de exclamação corresponde a si mesmo.  
  
## <a name="special-characters"></a>Caracteres especiais  
 Para corresponder ao colchete esquerdo de caracteres especiais (`[`), ponto de interrogação (`?`), sinal de número (`#`) e asterisco (`*`), coloque-os entre colchetes. O colchete direito (`]`) não pode ser usado em um grupo para corresponder a si mesmo, mas pode ser usado fora de um grupo como um caractere individual.  
  
 A sequência de caracteres `[]` é considerada uma cadeia de caracteres de comprimento zero (`""`). No entanto, ele não pode fazer parte de uma lista de caracteres entre colchetes. Se você quiser verificar se uma posição em `string` contém um de um grupo de caracteres ou nenhum caractere, você pode usar `Like` duas vezes. Para obter um exemplo, consulte [ Corresponder uma cadeia de caracteres com um padrão @ no__t-0.  
  
## <a name="character-ranges"></a>Intervalos de caracteres  
 Usando um hífen (`–`) para separar os limites inferior e superior do intervalo, `charlist` pode especificar um intervalo de caracteres. Por exemplo, `[A–Z]` resultará em uma correspondência se a posição de caractere correspondente em `string` contiver qualquer caractere dentro do intervalo `A` – `Z` e `[!H–L]` resultar em uma correspondência se a posição do caractere correspondente contiver qualquer caractere fora do intervalo `H` – `L`.  
  
 Quando você especifica um intervalo de caracteres, eles devem aparecer em ordem de classificação crescente, ou seja, do mais baixo para o mais alto. Assim, `[A–Z]` é um padrão válido, mas `[Z–A]` não é.  
  
### <a name="multiple-character-ranges"></a>Vários intervalos de caracteres  
 Para especificar vários intervalos para a mesma posição de caractere, coloque-os dentro dos mesmos colchetes sem delimitadores. Por exemplo, `[A–CX–Z]` resultará em uma correspondência se a posição de caractere correspondente em `string` contiver qualquer caractere dentro do intervalo `A` – `C` ou o intervalo `X` – `Z`.  
  
### <a name="usage-of-the-hyphen"></a>Uso do hífen  
 Um hífen (`–`) pode aparecer no início (após um ponto de exclamação, se houver) ou no final de `charlist` para corresponder a si mesmo. Em qualquer outro local, o hífen identifica um intervalo de caracteres delimitado pelos caracteres em ambos os lados do hífen.  
  
## <a name="collating-sequence"></a>Sequência de agrupamento  
 O significado de um intervalo especificado depende da ordenação de caracteres em tempo de execução, conforme determinado pelo `Option Compare` e pela configuração de localidade do sistema em que o código está sendo executado. Com `Option Compare Binary`, o intervalo `[A–E]` corresponde a `A`, `B`, `C`, `D` e `E`. Com `Option Compare Text`, `[A–E]` corresponde a `A`, `a`, `À`, `à`, `B`, `b`, `C`, `c`, 0, 1, 2 e 3. O intervalo não corresponde a `Ê` ou `ê` porque os caracteres acentuados se agrupam após caracteres não acentuados na ordem de classificação.  
  
## <a name="digraph-characters"></a>Caracteres digrafo  
 Em alguns idiomas, há caracteres alfabéticos que representam dois caracteres separados. Por exemplo, várias linguagens usam o caractere `æ` para representar os caracteres `a` e `e` quando aparecem juntos. O operador `Like` reconhece que o caractere dígrafo único e os dois caracteres individuais são equivalentes.  
  
 Quando um idioma que usa um caractere dígrafo é especificado nas configurações de localidade do sistema, uma ocorrência do caractere digraph único em `pattern` ou `string` corresponde à sequência de dois caracteres equivalente na outra cadeia de caracteres. Da mesma forma, um caractere digrafo em `pattern` entre colchetes (por si só, em uma lista ou em um intervalo) corresponde à sequência de dois caracteres equivalente em `string`.  
  
## <a name="overloading"></a>Sobrecarga  
 O operador `Like` pode ser *sobrecarregado*, o que significa que uma classe ou estrutura pode redefinir seu comportamento quando um operando tem o tipo dessa classe ou estrutura. Se o seu código usar esse operador em uma classe ou estrutura desse tipo, certifique-se de entender seu comportamento redefinido. Para obter mais informações, consulte [procedimentos de operador](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa o operador `Like` para comparar cadeias de caracteres com vários padrões. Os resultados entram em uma variável `Boolean` indicando se cada cadeia de caracteres satisfaz o padrão.  
  
 [!code-vb[VbVbalrOperators#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#30)]  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.Strings.InStr%2A>
- <xref:Microsoft.VisualBasic.Strings.StrComp%2A>
- [Operadores de Comparação](../../../visual-basic/language-reference/operators/comparison-operators.md)
- [Precedência do operador no Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [Operadores Listados por Funcionalidade](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Instrução Option Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md)
- [Operadores e Expressões](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)
- [Como: Corresponder uma cadeia de caracteres com um padrão @ no__t-0
