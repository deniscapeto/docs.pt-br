---
title: TENDO (Entity SQL)
ms.date: 03/30/2017
ms.assetid: b5d52d97-8372-4335-beac-2d0b79dc3707
ms.openlocfilehash: 97ed6e06241804bf2f576c910a2235b0cb570bbb
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833727"
---
# <a name="having-entity-sql"></a>TENDO (Entity SQL)
Especifica um critério de pesquisa para um grupo ou uma agregação.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
[ HAVING search_condition ]  
```  
  
## <a name="arguments"></a>Argumentos  
 `search_condition`  
 Especifica o critério de pesquisa para o grupo ou a agregação encontre-se. Quando HAVING foi usado com GROUP BY ALL, a cláusula HAVING substitui ALL.  
  
## <a name="remarks"></a>Comentários  
 A cláusula HAVING é usada para especificar uma condição adicional de filtragem no resultado de um agrupamento. Se nenhum GRUPO é especificado pela cláusula a expressão de consulta, um único grupo implícito definido será adotado.  
  
> [!NOTE]
> With pode ser usado somente com a instrução [Select](select-entity-sql.md) . Quando [Group by](group-by-entity-sql.md) não é usado, ter se comportar como uma cláusula WHERE.  
  
A cláusula HAVING funciona como a cláusula WHERE exceto que são aplicados após a operação GROUP BY. Isso significa que a cláusula HAVING só pode fazer referências para Agrupamento de aliases e agregações, conforme ilustrado no exemplo a seguir:
  
```sql  
SELECT Name, SUM(o.Price * o.Quantity) AS Total FROM orderLines AS o GROUP BY o.Product AS Name  
HAVING SUM(o.Quantity) > 1  
```  
  
 O anterior restringe os grupos somente aquelas que incluem mais de um produto.  
  
## <a name="example"></a>Exemplo  
 A seguinte consulta SQL Entity usa HAVING e o GROUP BY operadores especificar um critério de pesquisa para um grupo ou uma agregação. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [How para: Executar uma consulta que retorna os resultados de Primitivatype @ no__t-0.  
  
2. Passe a consulta a seguir como um argumento para o método `ExecutePrimitiveTypeQuery`:  
  
 [!code-sql[DP EntityServices Concepts#HAVING](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#having)]  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
- [Expressões de Consulta](query-expressions-entity-sql.md)
