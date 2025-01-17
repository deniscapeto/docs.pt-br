---
title: 'Como: representar um cliente em um serviço'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, impersonation
- impersonation
- WCF, security
ms.assetid: 431db851-a75b-4009-9fe2-247243d810d3
ms.openlocfilehash: 918cbba30cbb997a1f029a250adbdc4ed6310299
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69951054"
---
# <a name="how-to-impersonate-a-client-on-a-service"></a>Como: representar um cliente em um serviço
A representação de um cliente em um serviço de Windows Communication Foundation (WCF) permite que o serviço execute ações em nome do cliente. Para ações sujeitas a verificações de ACL (lista de controle de acesso), como o acesso a diretórios e arquivos em um computador ou acesso a um banco de dados SQL Server, a verificação de ACL é feita em relação à conta de usuário do cliente. Este tópico mostra as etapas básicas necessárias para habilitar um cliente em um domínio do Windows para definir um nível de representação do cliente. Para obter um exemplo de trabalho disso, consulte [personificando o cliente](../../../docs/framework/wcf/samples/impersonating-the-client.md). Para obter mais informações sobre a representação do cliente, consulte [delegação e representação](../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md).  
  
> [!NOTE]
> Quando o cliente e o serviço estão em execução no mesmo computador e o cliente está sendo executado em uma conta do sistema ( `Local System` ou `Network Service`seja, ou), o cliente não pode ser representado quando uma sessão segura é estabelecida com tokens de contexto de segurança com estado. Um aplicativo de console ou WinForms normalmente é executado na conta atualmente conectada, para que essa conta possa ser representada por padrão. No entanto, quando o cliente é uma página ASP.net e essa página é hospedada no IIS 6,0 ou no IIS 7,0, o cliente executa `Network Service` a execução na conta por padrão. Todas as associações fornecidas pelo sistema que dão suporte a sessões seguras usam um token de contexto de segurança sem estado por padrão. No entanto, se o cliente for uma página ASP.NET e as sessões seguras com tokens de contexto de segurança com estado forem usadas, o cliente não poderá ser representado. Para obter mais informações sobre como usar tokens de contexto de segurança com estado [em uma sessão segura, consulte Como: Crie um token de contexto de segurança para uma](../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md)sessão segura.  
  
### <a name="to-enable-impersonation-of-a-client-from-a-cached-windows-token-on-a-service"></a>Para habilitar a representação de um cliente de um token do Windows em cache em um serviço  
  
1. Criar o serviço. Para obter um tutorial desse procedimento básico, consulte [introdução tutorial](../../../docs/framework/wcf/getting-started-tutorial.md).  
  
2. Use uma associação que usa a autenticação do Windows e crie uma sessão, <xref:System.ServiceModel.NetTcpBinding> como <xref:System.ServiceModel.WSHttpBinding>ou.  
  
3. Ao criar a implementação da interface do serviço, aplique a <xref:System.ServiceModel.OperationBehaviorAttribute> classe ao método que requer a representação do cliente. Defina a propriedade <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A> como <xref:System.ServiceModel.ImpersonationOption.Required>.  
  
     [!code-csharp[c_SimpleImpersonation#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_simpleimpersonation/cs/source.cs#2)]
     [!code-vb[c_SimpleImpersonation#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_simpleimpersonation/vb/source.vb#2)]  
  
### <a name="to-set-the-allowed-impersonation-level-on-the-client"></a>Para definir o nível de representação permitido no cliente  
  
1. Crie o código do cliente de serviço usando a [ferramenta de utilitário de metadados ServiceModel (svcutil. exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md). Para obter mais informações, consulte Acessando [serviços usando um cliente WCF](../../../docs/framework/wcf/accessing-services-using-a-wcf-client.md).  
  
2. Depois de criar o cliente WCF, defina <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> a propriedade <xref:System.ServiceModel.Security.WindowsClientCredential> da <xref:System.Security.Principal.TokenImpersonationLevel> classe como um dos valores de enumeração.  
  
    > [!NOTE]
    > Para usar <xref:System.Security.Principal.TokenImpersonationLevel.Delegation>, a autenticação Kerberos negociada (às vezes chamada de Kerberos de *vários trechos* ou *várias etapas* ) deve ser usada. Para obter uma descrição de como implementar isso, consulte [práticas recomendadas de segurança](../../../docs/framework/wcf/feature-details/best-practices-for-security-in-wcf.md).  
  
     [!code-csharp[c_SimpleImpersonation#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_simpleimpersonation/cs/source.cs#1)]
     [!code-vb[c_SimpleImpersonation#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_simpleimpersonation/vb/source.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.OperationBehaviorAttribute>
- <xref:System.Security.Principal.TokenImpersonationLevel>
- [Representar o cliente](../../../docs/framework/wcf/samples/impersonating-the-client.md)
- [Delegação e representação](../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)
