---
title: -refout (Opções do compilador do C#)
ms.date: 08/08/2017
f1_keywords:
- /refout
helpviewer_keywords:
- refout compiler option [C#]
- /refout compiler option [C#]
- -refout compiler option [C#]
ms.openlocfilehash: 97cbf540527d0449387b71bb1d97df95b6a4aba4
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69602510"
---
# <a name="-refout-c-compiler-options"></a>-refout (Opções do compilador do C#)

A opção **-refout** especifica um caminho de arquivo em que o assembly de referência deve ser gerado. Isso se converte em `metadataPeStream` na API de emissão. Essa opção corresponde à propriedade de projeto [ProduceReferenceAssembly](/visualstudio/msbuild/common-msbuild-project-properties) do MSBuild.

## <a name="syntax"></a>Sintaxe

```console
-refout:filepath
```

## <a name="arguments"></a>Arguments

 `filepath` O fipeath so assembly de referência. Geralmente, ele deve corresponder ao assembly principal. A convenção recomendada (usada pelo MSBuild) é colocar o assembly de referência em uma subpasta "ref/" em relação ao assembly principal.

## <a name="remarks"></a>Comentários

Os assemblies somente de metadados têm seus corpos de método substituídos por um único corpo `throw null`, mas incluem todos os membros, exceto tipos anônimos. O motivo para usar corpos `throw null` (em vez de nenhum corpo) é que PEVerify poderia ser executado e passado (validando, assim, a integridade dos metadados).

Os assemblies de referência incluem um atributo `ReferenceAssembly` de nível de assembly. Esse atributo pode ser especificado na origem (assim, o compilador não precisará sintetizá-lo). Por causa desse atributo, os tempos de execução se recusarão a carregar assemblies de referência para execução (mas ainda podem ser carregados em modo somente reflexão). As ferramentas que se refletem nos assemblies precisam garantir que elas carreguem assemblies de referência como somente reflexão, caso contrário, elas receberão um erro de typeload do tempo de execução.

Os assemblies de referência removem ainda mais metadados (membros particulares) de assemblies somente de metadados:

- Um assembly de referência tem somente referências para o que ele precisa na superfície de API. Talvez o assembly real tenha outras referências relacionadas a implementações específicas. Por exemplo, o assembly de referência para `class C { private void M() { dynamic d = 1; ... } }` não referencia nenhum tipo necessário para `dynamic`.
- Membros de função privados (métodos, propriedades e eventos) são removidos nos casos em que sua remoção não afeta nitidamente a compilação. Se não houver nenhum atributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>, faça o mesmo para os membros de função internos.
- Mas todos os tipos (incluindo tipos aninhados ou privados) são mantidos em assemblies de referência. Todos os atributos são mantidos (até mesmo os internos).
- Todos os métodos virtuais são mantidos. As implementações explícitas da interface são mantidas. As propriedades e eventos explicitamente implementados são mantidos, uma vez que seus acessadores são virtuais (e são, portanto, mantidos).
- Todos os campos de um struct são mantidos. (Este é um candidato para refinamento pós-c#-7.1)

As opções `-refout` e [`-refonly`](refonly-compiler-option.md) são mutualmente exclusivas.

## <a name="see-also"></a>Consulte também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
