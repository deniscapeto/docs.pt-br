---
title: Classificando com DataView (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 885b3b7b-51c1-42b3-bb29-b925f4f69a6f
ms.openlocfilehash: 481a56f923c4218cd8689c578ce990785aee0ab3
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782716"
---
# <a name="sorting-with-dataview-linq-to-dataset"></a>Classificando com DataView (LINQ to DataSet)
A capacidade de classificar dados com base em critérios específicos e apresentá-los para um cliente através de um controle da interface do usuário é um aspecto importante da vinculação de dados. O objeto <xref:System.Data.DataView> fornece várias maneiras de classificar dados e retornar linhas de dados ordenadas por critérios específicos. Além de seus recursos de classificação baseados em cadeia de <xref:System.Data.DataView> caracteres, o também permite [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] que você use expressões para os critérios de classificação. [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)]as expressões permitem operações de classificação muito mais complexas e poderosas do que a classificação baseada em cadeia de caracteres. Este tópico descreve as duas abordagens de classificação usando <xref:System.Data.DataView>.  
  
## <a name="creating-dataview-from-a-query-with-sorting-information"></a>Criando um DataView a partir de uma consulta com informações de classificação  
 Um <xref:System.Data.DataView> objeto pode ser criado a partir de uma consulta LINQ to DataSet. Se essa consulta contiver <xref:System.Linq.Enumerable.OrderBy%2A>uma <xref:System.Linq.Enumerable.OrderByDescending%2A>cláusula <xref:System.Linq.Enumerable.ThenBy%2A>,, <xref:System.Linq.Enumerable.ThenByDescending%2A> ou, as expressões nessas cláusulas <xref:System.Data.DataView>serão usadas como base para classificar os dados no. Por exemplo, se a consulta contiver `Order By…`as `Then By…` cláusulas e, o <xref:System.Data.DataView> resultado resultaria na ordenação dos dados por ambas as colunas especificadas.  
  
 A classificação baseada em expressão oferece uma classificação mais avançada e complexa do que a classificação mais simples baseada em cadeia de caracteres. Observe que a classificação baseada em cadeia de caracteres e a classificação baseada em expressão são mutuamente excludentes. Se a <xref:System.Data.DataView.Sort%2A> baseada em cadeia de caracteres for definida após <xref:System.Data.DataView> ser criado a partir de uma consulta, o filtro baseado em expressão inferido da consulta será limpo e não poderá ser redefinido.  
  
 O índice de um <xref:System.Data.DataView> é compilado quando <xref:System.Data.DataView> é criado e quando qualquer informação de classificação ou de filtragem é modificada. Você Obtém o melhor desempenho fornecendo critérios de classificação na consulta de LINQ to DataSet da qual o <xref:System.Data.DataView> é criado e não modificando as informações de classificação, mais tarde. Para obter mais informações, consulte [DataView performance](dataview-performance.md).  
  
> [!NOTE]
> Na maioria dos casos, as expressões usadas para classificação não devem ter efeitos colaterais e devem ser determinísticas. Além disso, as expressões não devem conter lógica que dependa de um número definido de execuções, pois as operações de classificação podem ser executadas qualquer número de vezes.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir consulta a tabela SalesOrderHeader e ordena as linhas retornadas pela ordem do pedido; cria <xref:System.Data.DataView> a partir da consulta e associa o objeto <xref:System.Data.DataView> a uma <xref:System.Windows.Forms.BindingSource>.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryOrderBy](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromqueryorderby)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryOrderBy](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromqueryorderby)]  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir consulta a tabela SalesOrderHeader e ordena as linhas retornadas pelo valor total devido; cria <xref:System.Data.DataView> a partir da consulta e associa o objeto <xref:System.Data.DataView> a uma <xref:System.Windows.Forms.BindingSource>.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryOrderBy2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromqueryorderby2)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryOrderBy2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromqueryorderby2)]  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir consulta a tabela SalesOrderDetail e ordena as linhas retornadas pela quantidade de pedidos e depois pela ID da ordem de venda; cria <xref:System.Data.DataView> a partir da consulta e associa o objeto <xref:System.Data.DataView> a uma <xref:System.Windows.Forms.BindingSource>.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryOrderByThenBy](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromqueryorderbythenby)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryOrderByThenBy](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromqueryorderbythenby)]  
  
## <a name="using-the-string-based-sort-property"></a>Usando a propriedade de classificação baseada em cadeia de caracteres  
 A funcionalidade de classificação baseada em cadeia <xref:System.Data.DataView> de caracteres do ainda funciona com LINQ to DataSet. Depois que <xref:System.Data.DataView> um tiver sido criado a partir de uma consulta LINQ to DataSet, você <xref:System.Data.DataView.Sort%2A> poderá usar a propriedade para <xref:System.Data.DataView>definir a classificação no.  
  
 As funcionalidades de classificação baseada em cadeia de caracteres e de classificação baseada em expressão são mutuamente excludentes. A definição da propriedade <xref:System.Data.DataView.Sort%2A> limpa a classificação baseada em expressão herdada da consulta a partir da qual o objeto <xref:System.Data.DataView> foi criado.  
  
 Para obter mais informações sobre filtragem baseada <xref:System.Data.DataView.Sort%2A> em cadeia de caracteres, consulte [classificando e Filtrando dados](./dataset-datatable-dataview/sorting-and-filtering-data.md).  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir cria um <xref:System.Data.DataView> a partir da tabela de contatos e classifica as linhas por sobrenome em ordem decrescente e depois por nome em ordem crescente:  
  
 [!code-csharp[DP DataView Samples#LDVStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvstringsort)]
 [!code-vb[DP DataView Samples#LDVStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvstringsort)]  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir consulta na tabela de contatos os sobrenomes que começam com a letra "S".  Um <xref:System.Data.DataView> é criado a partir dessa consulta e associado a um objeto <xref:System.Windows.Forms.BindingSource>.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromquerystringsort)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromquerystringsort)]  
  
## <a name="clearing-the-sort"></a>Limpando a classificação  
 As informações de classificação em um objeto <xref:System.Data.DataView> podem ser limpas depois de definidas usando a propriedade <xref:System.Data.DataView.Sort%2A>. Existem duas maneiras de limpar informações de classificação no objeto <xref:System.Data.DataView>:  
  
- Defina a propriedade <xref:System.Data.DataView.Sort%2A> como `null`.  
  
- Defina a propriedade <xref:System.Data.DataView.Sort%2A> como uma cadeia de caracteres vazia.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir cria um objeto <xref:System.Data.DataView> a partir de uma consulta e limpa a classificação definindo a propriedade <xref:System.Data.DataView.Sort%2A> como uma cadeia de caracteres vazia:  
  
 [!code-csharp[DP DataView Samples#LDVClearSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearsort)]
 [!code-vb[DP DataView Samples#LDVClearSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearsort)]  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir cria um objeto <xref:System.Data.DataView> a partir da tabela de contatos e define a propriedade <xref:System.Data.DataView.Sort%2A> a ser classificada por sobrenome em ordem decrescente. As informações de classificação serão limpas definindo a propriedade <xref:System.Data.DataView.Sort%2A> como `null`:  
  
 [!code-csharp[DP DataView Samples#LDVClearSort2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearsort2)]
 [!code-vb[DP DataView Samples#LDVClearSort2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearsort2)]  
  
## <a name="see-also"></a>Consulte também

- [Associação de dados e LINQ to DataSet](data-binding-and-linq-to-dataset.md)
- [Filtrando com DataView](filtering-with-dataview-linq-to-dataset.md)
- [Classificando Dados](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/bb546145(v=vs.120))
