---
title: Construtor de tipo nomeado (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 549dea04-d93d-4c87-a292-f81b1598dbfd
ms.openlocfilehash: c7027614e5667acedb02d871a09df1ac9d799405
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70250016"
---
# <a name="named-type-constructor-entity-sql"></a>Construtor de tipo nomeado (Entity SQL)
Usado para criar instâncias de tipos nominais de modelo conceitual como a entidade ou tipos complexos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
[{identifier. }] identifier( [expression [{, expression }]] )  
```  
  
## <a name="arguments"></a>Arguments  
 `identifier`  
 Valor que é um identificador simples ou citado. Para obter mais informações, consulte [identificadores](identifiers-entity-sql.md)  
  
 `expression`  
 Atributos de tipo que são considerados para estar na mesma ordem que aparecem na declaração de tipo.  
  
## <a name="return-value"></a>Valor de retorno  
 Instâncias de tipos complexos nomeados e tipos de entidade.  
  
## <a name="remarks"></a>Comentários  
 Os exemplos a seguir mostram como construir o substantivo e os tipos complexos:  
  
 A expressão a seguir cria uma instância de um tipo de `Person` :  
  
 `Person("abc", 12)`  
  
 A expressão a seguir cria uma instância de um tipo complexo:  
  
 `MyModel.ZipCode(‘98118’, ‘4567’)`  
  
 A expressão a seguir cria uma instância de um tipo complexo aninhado:  
  
 `MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567'))`  
  
 A expressão a seguir cria uma instância de um objeto com um tipo complexo aninhado:  
  
 `MyModel.Person("Bill", MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567')))`  
  
 O exemplo a seguir mostra como inicializar uma propriedade de um tipo complexo para nulo:`MyModel.ZipCode(‘98118’, null)`  
  
## <a name="example"></a>Exemplo  
 A seguinte consulta SQL Entity usa o construtor chamado de tipo para criar uma instância de um tipo de modelo conceitual. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [como: Executar uma consulta que retorna resultados](../how-to-execute-a-query-that-returns-structuraltype-results.md)de estruturaistype.  
  
2. Passe a consulta a seguir como um argumento para o método `ExecuteStructuralTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#NAMED_TYPE_CONSTRUCTOR](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#named_type_constructor)]  
  
## <a name="see-also"></a>Consulte também

- [Construindo tipos](constructing-types-entity-sql.md)
- [Referência de Entity SQL](entity-sql-reference.md)
