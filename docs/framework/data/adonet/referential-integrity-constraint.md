---
title: restrição de integridade referencial
ms.date: 03/30/2017
ms.assetid: 3d3ba44b-4302-40d8-a7a9-62932e0395e5
ms.openlocfilehash: 28880c7085f8b4e3dd2e51b5633c1f0e2a984a4b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794450"
---
# <a name="referential-integrity-constraint"></a>restrição de integridade referencial
Uma *restrição de integridade referencial* no modelo de dados de entidade (EDM) é semelhante a uma restrição de integridade referencial em um banco de dados relacional. Da mesma forma que uma coluna (ou colunas) de uma tabela de banco de dados pode referenciar a chave primária de outra tabela, uma [Propriedade](property.md) (ou Propriedades) de um [tipo de entidade](entity-type.md) pode referenciar a [chave de entidade](entity-key.md) de outro tipo de entidade. O tipo de entidade referenciado é chamado de *extremidade principal* da restrição. O tipo de entidade que faz referência à extremidade principal é chamado de *extremidade dependente* da restrição.  
  
 Uma restrição de integridade referencial é definida como parte de uma [Associação](association-type.md) entre dois tipos de entidade. A definição de uma restrição de integridade referencial especifica as seguintes informações:  
  
- O final principal de restrição. (Um tipo de entidade cuja chave de entidade é referenciada pela o final dependente.)  
  
- A chave de entidade de extremidade principal.  
  
- O final dependente de restrição. (Um tipo de entidade que tem uma propriedade ou um propriedades que referenciem a chave de entidade de extremidade principal.)  
  
- A propriedade ou propriedades referência de extremidade dependente.  
  
 O objetivo de restrições de integridade referencial em EDM é garantir que as associações válidos sempre existe. Para obter mais informações, consulte [Propriedade Foreign Key](foreign-key-property.md).  
  
## <a name="example"></a>Exemplo  
 O diagrama a seguir mostra um modelo conceitual com duas associações: `WrittenBy` e `PublishedBy`. O tipo de entidade de `Book` tem uma propriedade, `PublisherId`, que faz referência a chave de entidade do tipo de entidade de `Publisher` quando você define uma restrição de integridade referencial em associação de `PublishedBy` .  
  
 ![RefConstraintModel](./media/referential-integrity-constraint/reference-constraint-model.gif "Exemplo de um modelo de restrição referencial")  
  
 O [Entity Framework ADO.net](./ef/index.md) usa uma DSL (linguagem específica de domínio) chamada[CSDL](./ef/language-reference/csdl-specification.md)(linguagem de definição de esquema conceitual) para definir modelos conceituais. CSDL seguir define uma restrição de integridade referencial em associação de `PublishedBy` mostrada no modelo conceitual anterior.  
  
 [!code-xml[EDM_Example_Model#RefConstraint](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#refconstraint)]  
  
## <a name="see-also"></a>Consulte também

- [Principais conceitos do Modelo de Dados de Entidade](entity-data-model-key-concepts.md)
- [Modelo de Dados de Entidade](entity-data-model.md)
