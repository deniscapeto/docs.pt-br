---
title: O nome da variável de intervalo só pode ser inferido a partir de um nome simples ou qualificado sem argumentos
ms.date: 07/20/2015
f1_keywords:
- vbc36599
- bc36599
helpviewer_keywords:
- BC36599
ms.assetid: 17763dbe-f74f-4ccb-8086-cb7e45ec4d12
ms.openlocfilehash: f448f34dc5909b9128fc700abab5b4f00e911edf
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701009"
---
# <a name="range-variable-name-can-be-inferred-only-from-a-simple-or-qualified-name-with-no-arguments"></a>O nome da variável de intervalo só pode ser inferido a partir de um nome simples ou qualificado sem argumentos
Um elemento de programação que usa um ou mais argumentos é incluído em uma consulta LINQ. O compilador não pode inferir uma variável de intervalo desse elemento de programação.  
  
 **ID do erro:** BC36599  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1. Forneça um nome de variável explícito para o elemento de programação, conforme mostrado no código a seguir:  
  
```vb  
Dim query = From var1 In collection1   
            Select VariableAlias= SampleFunction(var1), var1  
```  
  
## <a name="see-also"></a>Consulte também

- [Introdução ao LINQ no Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [Cláusula Select](../../../visual-basic/language-reference/queries/select-clause.md)
