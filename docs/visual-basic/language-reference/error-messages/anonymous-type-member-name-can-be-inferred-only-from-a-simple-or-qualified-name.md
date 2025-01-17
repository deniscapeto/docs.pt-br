---
title: O nome do membro de tipo anônimo só pode ser inferido a partir de um nome simples ou qualificado sem argumentos
ms.date: 07/20/2015
f1_keywords:
- vbc36556
- bc36556
helpviewer_keywords:
- BC36556
ms.assetid: e3ba1f33-3a71-4f03-9b04-ed5ec17de17c
ms.openlocfilehash: 38f669fe183ac79ebed6e5a122bc70aedc9bb753
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701223"
---
# <a name="anonymous-type-member-name-can-be-inferred-only-from-a-simple-or-qualified-name-with-no-arguments"></a>O nome do membro de tipo anônimo só pode ser inferido a partir de um nome simples ou qualificado sem argumentos
Não é possível inferir um nome de membro de tipo anônimo de uma expressão complexa.  
  
```vb  
Dim numbers() As Integer = {1, 2, 3, 4, 5}  
' Not valid.  
' Dim instanceName1 = New With {numbers(3)}  
```  
  
 Para obter mais informações sobre fontes das quais tipos anônimos podem e não podem inferir nomes e tipos de membros, consulte [How para: Inferir nomes e tipos de propriedade em declarações de tipo anônimos @ no__t-0.  
  
 **ID do erro:** BC36556  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Atribua a expressão a um nome de membro, conforme mostrado no código a seguir:  
  
    ```vb  
    Dim instanceName2 = New With {.number = numbers(3)}  
    ```  
  
## <a name="see-also"></a>Consulte também

- [Tipos Anônimos](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [Como: Inferir nomes e tipos de propriedade em declarações de tipo anônimo @ no__t-0
