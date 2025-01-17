---
title: Atualizando o serviço de dados (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, changing data
- WCF Data Services, client library
ms.assetid: 00d993be-ffed-4dea-baf7-6eea982cdb54
ms.openlocfilehash: 5cf7a6e563069e35a4ac0fe729a616dc1c56bdb5
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70779749"
---
# <a name="updating-the-data-service-wcf-data-services"></a>Atualizando o serviço de dados (WCF Data Services)
Quando você usa a [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] biblioteca de cliente para consumir [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] um feed, a biblioteca converte as entradas no feed em instâncias de classes de serviço de dados do cliente. Essas classes de serviço de dados são controladas <xref:System.Data.Services.Client.DataServiceContext> usando o ao <xref:System.Data.Services.Client.DataServiceQuery%601> qual o pertence. O cliente controla as alterações nas entidades que você relata usando métodos em <xref:System.Data.Services.Client.DataServiceContext>. Esses métodos permitem que o cliente rastreie entidades adicionadas e excluídas e também alterações feitas em valores de propriedade ou em relações entre instâncias de entidade. Essas alterações controladas são enviadas de volta ao serviço de dados como operações baseadas em REST quando você <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> chama o método.  
  
> [!NOTE]
> Quando você usa uma instância do <xref:System.Data.Services.Client.DataServiceCollection%601> para associar dados a controles, as alterações feitas nos dados no controle ligado são automaticamente relatadas <xref:System.Data.Services.Client.DataServiceContext>para o. Para obter mais informações, consulte [associando dados a controles](binding-data-to-controls-wcf-data-services.md).  
  
## <a name="adding-modifying-and-changing-entities"></a>Adicionando, modificando e alterando entidades  
 Quando você usa a caixa de diálogo **Adicionar referência de serviço** no Visual Studio para adicionar uma referência [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] a um feed, as classes resultantes do serviço de dados do cliente têm um método *Create* estático que recebe um parâmetro para cada propriedade de entidade não anulável . Você pode usar esse método para criar instâncias de classes de tipo de entidade, como no exemplo a seguir:  
  
 [!code-csharp[Astoria Northwind Client#CreateNewProduct](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#createnewproduct)]
 [!code-vb[Astoria Northwind Client#CreateNewProduct](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#createnewproduct)]  
  
 Para adicionar uma instância de entidade, chame o método *AddTo* apropriado na <xref:System.Data.Services.Client.DataServiceContext> classe gerada pela caixa de diálogo **Adicionar referência de serviço** , como no exemplo a seguir:  
  
 [!code-csharp[Astoria Northwind Client#AddProductSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#addproductspecific)]
 [!code-vb[Astoria Northwind Client#AddProductSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#addproductspecific)]  
  
 Isso adiciona o objeto ao contexto e ao conjunto correto de entidades. Você também pode chamar <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A>, mas, em vez disso, deve fornecer o nome do conjunto de entidades. Se a entidade adicionada tiver uma ou mais relações com outras entidades, você poderá usar o <xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A> método ou usar um dos métodos anteriores e também definir explicitamente esses links. Essas operações são discutidas posteriormente neste tópico.  
  
 Para modificar uma instância de entidade existente, primeiro consulte essa entidade, faça as alterações desejadas em suas propriedades e, em <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> seguida, chame <xref:System.Data.Services.Client.DataServiceContext> o método no para indicar à biblioteca de cliente que ele precisa para enviar uma atualização para esse objeto, conforme mostrado na o exemplo a seguir:  
  
 [!code-csharp[Astoria Northwind Client#ModifyCustomerSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#modifycustomerspecific)]
 [!code-vb[Astoria Northwind Client#ModifyCustomerSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#modifycustomerspecific)]  
  
 Para excluir uma instância de entidade, chame <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> o método <xref:System.Data.Services.Client.DataServiceContext>no, conforme mostrado no exemplo a seguir:  
  
 [!code-csharp[Astoria Northwind Client#DeleteProductSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#deleteproductspecific)]
 [!code-vb[Astoria Northwind Client#DeleteProductSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#deleteproductspecific)]  
  
 Para obter mais informações, confira [Como: Adicionar, modificar e excluir entidades](how-to-add-modify-and-delete-entities-wcf-data-services.md).  
  
## <a name="attaching-entities"></a>Anexando entidades  
 A biblioteca de cliente permite que você salve as atualizações feitas em uma entidade sem primeiro executar uma consulta para carregar a entidade no <xref:System.Data.Services.Client.DataServiceContext>. Use o <xref:System.Data.Services.Client.DataServiceContext.AttachTo%2A> método para anexar um objeto existente a uma entidade específica definida <xref:System.Data.Services.Client.DataServiceContext>no. Em seguida, você pode modificar o objeto e salvar as alterações no serviço de dados. No exemplo a seguir, um objeto Customer que foi alterado está anexado ao contexto e, em seguida <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> , é chamado para marcar o objeto anexado <xref:System.Data.Services.Client.EntityStates.Modified> como <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> antes é chamado:  
  
 [!code-csharp[Astoria Northwind Client#AttachObjectSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#attachobjectspecific)]
 [!code-vb[Astoria Northwind Client#AttachObjectSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#attachobjectspecific)]  
  
 As seguintes considerações se aplicam ao anexar objetos:  
  
- Um objeto está anexado no <xref:System.Data.Services.Client.EntityStates.Unchanged> estado.  
  
- Quando um objeto é anexado, os objetos que estão relacionados ao objeto anexado também não são anexados.  
  
- Um objeto não poderá ser anexado se a entidade já estiver sendo rastreada pelo contexto.  
  
- A <xref:System.Data.Services.Client.DataServiceContext.AttachTo%28System.String%2CSystem.Object%2CSystem.String%29> sobrecarga do método que usa `etag` um parâmetro é usada quando você anexa um objeto de entidade que foi recebido junto com um valor de eTag. Esse valor de eTag é usado para verificar a simultaneidade quando as alterações no objeto anexado são salvas.  
  
 Para obter mais informações, confira [Como: Anexe uma entidade existente ao DataServiceContext](attach-an-existing-entity-to-dc-wcf-data.md).  
  
## <a name="creating-and-modifying-relationship-links"></a>Criando e modificando links de relações  
 Quando você adiciona uma <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> nova entidade usando o método ou o método *AddTo* apropriado da <xref:System.Data.Services.Client.DataServiceContext> classe que a caixa de diálogo **Adicionar referência de serviço** gera, todas as relações entre a nova entidade e as entidades relacionadas são Não definido automaticamente.  
  
 Você pode criar e alterar relações entre instâncias de entidade e fazer com que a biblioteca de cliente reflita essas alterações no serviço de dados. As relações entre as entidades são definidas como associações no modelo e o <xref:System.Data.Services.Client.DataServiceContext> rastreia cada relação como um objeto de link no contexto. [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]fornece os seguintes métodos na <xref:System.Data.Services.Client.DataServiceContext> classe para criar, modificar e excluir esses links:  
  
|Método|Descrição|  
|------------|-----------------|  
|<xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A>|Cria um novo link entre dois objetos de entidade relacionados. Chamar esse método é equivalente a chamar <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> e <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> criar o novo objeto e definir a relação com um objeto existente.|  
|<xref:System.Data.Services.Client.DataServiceContext.AddLink%2A>|Cria um novo link entre dois objetos de entidade relacionados.|  
|<xref:System.Data.Services.Client.DataServiceContext.SetLink%2A>|Atualiza um link existente entre dois objetos de entidade relacionados. <xref:System.Data.Services.Client.DataServiceContext.SetLink%2A>também é usado para excluir links com uma cardinalidade de zero-ou-um para um (`0..1:1`) e um para um (`1:1`). Você pode fazer isso definindo o objeto relacionado como `null`.|  
|<xref:System.Data.Services.Client.DataServiceContext.DeleteLink%2A>|Marca um link que o contexto está rastreando para exclusão quando <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> o método é chamado. Use esse método quando você excluir um objeto relacionado ou alterar uma relação excluindo primeiro o link para um objeto existente e, em seguida, adicionando um link para o novo objeto relacionado.|  
|<xref:System.Data.Services.Client.DataServiceContext.AttachLink%2A>|Notifica o contexto de um link existente entre dois objetos de entidade. O contexto supõe que essa relação já existe no serviço de dados e não tenta criar o link quando você chama o <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> método. Use este método quando você anexa objetos a um contexto e também precisa anexar o link entre os dois. Se você estiver definindo uma nova relação, deverá usar <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A>.|  
|<xref:System.Data.Services.Client.DataServiceContext.DetachLink%2A>|Interrompe o rastreamento do link especificado no contexto. Esse método é usado para excluir relações um-para-muitos`*:*`(). Para links de relação com uma cardinalidade de um, você deve usar <xref:System.Data.Services.Client.DataServiceContext.SetLink%2A>.|  
  
 O exemplo a seguir mostra como usar o <xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A> método para adicionar um novo `Order_Detail` que está relacionado a uma entidade `Orders` existente. Como o novo `Order_Details` objeto agora é acompanhado <xref:System.Data.Services.Client.DataServiceContext>pelo, a relação do objeto adicionado `Order_Details` à entidade existente `Products` é definida chamando-se o <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> método:  
  
 [!code-csharp[Astoria Northwind Client#AddOrderDetailToOrderSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#addorderdetailtoorderspecific)]
 [!code-vb[Astoria Northwind Client#AddOrderDetailToOrderSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#addorderdetailtoorderspecific)]  
  
 Embora o <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> método defina links que devem ser criados no serviço de dados, para que esses links sejam refletidos nos objetos que estão no contexto, você também deve definir as propriedades de navegação nos próprios objetos. No exemplo anterior, você deve definir as propriedades de navegação da seguinte maneira:  
  
 [!code-csharp[Astoria Northwind Client#SetNavProps](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#setnavprops)]
 [!code-vb[Astoria Northwind Client#SetNavProps](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#setnavprops)]  
  
 Para obter mais informações, confira [Como: Definir relações](how-to-define-entity-relationships-wcf-data-services.md)de entidade.  
  
## <a name="saving-changes"></a>Salvando alterações  
 As alterações são rastreadas <xref:System.Data.Services.Client.DataServiceContext> na instância, mas não são enviadas ao servidor imediatamente. Depois de concluir as alterações necessárias para uma atividade especificada, chame <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> para enviar todas as alterações para o serviço de dados. Para obter mais informações, consulte [Gerenciando o contexto do serviço de dados](managing-the-data-service-context-wcf-data-services.md). Você também pode salvar as alterações de forma assíncrona <xref:System.Data.Services.Client.DataServiceContext.EndSaveChanges%2A> usando os <xref:System.Data.Services.Client.DataServiceContext.BeginSaveChanges%2A> métodos e. Para obter mais informações, consulte [operações assíncronas](asynchronous-operations-wcf-data-services.md).  
  
## <a name="see-also"></a>Consulte também

- [WCF Data Services Client Library](wcf-data-services-client-library.md) (Biblioteca de clientes do WCF Data Services)
- [Querying the Data Service](querying-the-data-service-wcf-data-services.md) (Consultando o serviço de dados)
- [Operações assíncronas](asynchronous-operations-wcf-data-services.md)
- [Operações de envio em lote](batching-operations-wcf-data-services.md)
- [Materialização de objetos](object-materialization-wcf-data-services.md)
- [Gerenciando o contexto do serviço de dados](managing-the-data-service-context-wcf-data-services.md)
