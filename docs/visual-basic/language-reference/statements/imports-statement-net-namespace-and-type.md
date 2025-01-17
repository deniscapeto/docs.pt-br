---
title: Instrução Imports-namespace e tipo do .NET (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Imports
- imports
helpviewer_keywords:
- declared element names [Visual Basic], qualification
- imports [Visual Basic]
- Imports statement [Visual Basic]
- aliases [Visual Basic], Imports statement
- container elements [Visual Basic]
- namespaces [Visual Basic], importing
- Imports statement [Visual Basic], syntax
- import aliases [Visual Basic]
- aliases [Visual Basic], import
- declared elements [Visual Basic], container elements
ms.assetid: 7062f8aa-d890-4232-9eed-92836e13fb6e
ms.openlocfilehash: a0b7a6a5fd16dc0daa620e6b490ddfdeb0e7c80e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912384"
---
# <a name="imports-statement-net-namespace-and-type"></a>Instrução Imports (tipo e namespace .NET)
Permite que nomes de tipos sejam referenciados sem qualificação de namespace.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Imports [ aliasname = ] namespace  
-or-  
Imports [ aliasname = ] namespace.element  
```  
  
## <a name="parts"></a>Partes  
  
|Termo|Definição|  
|---|---|  
|`aliasname`|Opcional. Um *alias de importação* ou nome pelo qual o código pode `namespace` se referir em vez da cadeia de caracteres de qualificação completa. Consulte [nomes de elementos](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)declarados.|  
|`namespace`|Necessário. O nome totalmente qualificado do namespace que está sendo importado. Pode ser uma cadeia de caracteres de namespaces aninhados em qualquer nível.|  
|`element`|Opcional. O nome de um elemento de programação declarado no namespace. Pode ser qualquer elemento de contêiner.|  
  
## <a name="remarks"></a>Comentários  
 A `Imports` instrução permite que os tipos contidos em um namespace específico sejam referenciados diretamente.  
  
 Você pode fornecer um único nome de namespace ou uma cadeia de caracteres de namespaces aninhados. Cada namespace aninhado é separado do próximo namespace de nível mais alto por um`.`ponto (), como ilustra o exemplo a seguir.  
  
 `Imports System.Collections.Generic`  
  
 Cada arquivo de origem pode conter qualquer número `Imports` de instruções. Eles devem seguir qualquer declaração de opção, como a `Option Strict` instrução, e devem preceder quaisquer declarações de elemento de programação, `Module` como `Class` instruções or.  
  
 Você pode usar `Imports` somente no nível de arquivo. Isso significa que o contexto de declaração para importação deve ser um arquivo de origem e não pode ser um namespace, classe, estrutura, módulo, interface, procedimento ou bloco.  
  
 Observe que a `Imports` instrução não torna elementos de outros projetos e assemblies disponíveis para seu projeto. A importação não tem o lugar de definir uma referência. Ele apenas remove a necessidade de qualificar nomes que já estão disponíveis para seu projeto. Para obter mais informações, consulte "importando elementos continentes" em [referências a elementos](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)declarados.  
  
> [!NOTE]
> Você pode definir instruções `Imports` implícitas usando a [página referências, designer de projeto (Visual Basic)](/visualstudio/ide/reference/references-page-project-designer-visual-basic). Para obter mais informações, confira [Como: Adicionar ou remover namespaces importados (](/visualstudio/ide/how-to-add-or-remove-imported-namespaces-visual-basic)Visual Basic).  
  
## <a name="import-aliases"></a>Aliases de importação  
 Um *alias de importação* define o alias para um namespace ou tipo. Os aliases de importação são úteis quando você precisa usar itens com o mesmo nome que são declarados em um ou mais namespaces. Para obter mais informações e um exemplo, consulte "qualificando um nome de elemento" em [referências a elementos](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)declarados.  
  
 Você não deve declarar um membro no nível de módulo com o mesmo nome `aliasname`de. Se você fizer isso, o compilador Visual Basic `aliasname` usará apenas para o membro declarado e não o reconhecerá como um alias de importação.  
  
 Embora a sintaxe usada para declarar um alias de importação seja como a usada para importar um prefixo de namespace XML, os resultados são diferentes. Um alias de importação pode ser usado como uma expressão em seu código, enquanto um prefixo de namespace XML pode ser usado somente em literais XML ou propriedades de eixo XML como o prefixo para um elemento qualificado ou nome de atributo.  
  
### <a name="element-names"></a>Nomes de elementos  
 Se você fornecer `element`, ele deve representar um *elemento de contêiner*, ou seja, um elemento de programação que pode conter outros elementos. Elementos de contêiner incluem classes, estruturas, módulos, interfaces e enumerações.  
  
 O escopo dos elementos disponibilizados por uma `Imports` instrução depende se você especificar. `element` Se você especificar somente `namespace`, todos os membros nomeados exclusivamente desse namespace e os membros dos elementos de contêiner nesse namespace estarão disponíveis sem qualificação. Se você especificar `namespace` e `element`, somente os membros desse elemento estarão disponíveis sem qualificação.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna todas as pastas em C:\ diretório usando a <xref:System.IO.DirectoryInfo> classe.  
  
 O código não `Imports` tem instruções na parte superior do arquivo. Portanto, as `DirectoryInfo`referências <xref:System.Text.StringBuilder>, e <xref:Microsoft.VisualBasic.ControlChars.CrLf> são totalmente qualificadas com os namespaces.  
  
 [!code-vb[VbVbalrStatements#152](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#152)]  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir `Imports` inclui instruções para os namespaces referenciados. Portanto, os tipos não precisam ser totalmente qualificados com os namespaces.  
  
 [!code-vb[VbVbalrStatements#153](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#153)]  
  
 [!code-vb[VbVbalrStatements#154](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#154)]  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir `Imports` inclui instruções que criam aliases para os namespaces referenciados. Os tipos são qualificados com os aliases.  
  
 [!code-vb[VbVbalrStatements#155](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#155)]  
  
 [!code-vb[VbVbalrStatements#156](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#156)]  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir `Imports` inclui instruções que criam aliases para os tipos referenciados. Os aliases são usados para especificar os tipos.  
  
 [!code-vb[VbVbalrStatements#157](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#157)]  
  
 [!code-vb[VbVbalrStatements#158](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#158)]  
  
## <a name="see-also"></a>Consulte também

- [Instrução Namespace](../../../visual-basic/language-reference/statements/namespace-statement.md)
- [Namespaces no Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)
- [Referências e a Instrução Imports](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)
- [Instrução Imports (Namespace de XML)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)
- [Referências a Elementos Declarados](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
