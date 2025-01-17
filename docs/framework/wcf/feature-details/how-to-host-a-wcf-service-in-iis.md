---
title: 'Como: hospedar um serviço WCF no IIS'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b044b1c9-c1e5-4c9f-84d8-0f02f4537f8b
ms.openlocfilehash: ad1fb7d289dea3396b4edb4d3b3e9fb7fb1891e3
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972416"
---
# <a name="how-to-host-a-wcf-service-in-iis"></a>Como: hospedar um serviço WCF no IIS
Este tópico descreve as etapas básicas necessárias para criar um serviço de Windows Communication Foundation (WCF) hospedado no Serviços de Informações da Internet (IIS). Este tópico pressupõe que você está familiarizado com o IIS e compreende como usar a ferramenta de gerenciamento do IIS para criar e gerenciar aplicativos do IIS. Para obter mais informações sobre o IIS, consulte [serviços de informações da Internet](https://go.microsoft.com/fwlink/?LinkId=132449). Um serviço WCF executado no ambiente do IIS aproveita totalmente os recursos do IIS, como reciclagem de processo, desligamento ocioso, monitoramento de integridade do processo e ativação baseada em mensagem. Essa opção de hospedando requer que o IIS esteja configurado corretamente, mas não requer que nenhum código de hospedagem seja escrito como parte do aplicativo. Você pode usar a hospedagem do IIS somente com um transporte HTTP.  
  
 Para obter mais informações sobre como o WCF e o ASP.NET interagem, consulte [Serviços WCF e ASP.net](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md). Para obter mais informações sobre como configurar a segurança, consulte [segurança](../../../../docs/framework/wcf/feature-details/security.md).  
  
 Para a cópia de origem deste exemplo, consulte [hospedagem do IIS usando código embutido](../../../../docs/framework/wcf/samples/iis-hosting-using-inline-code.md).  
  
### <a name="to-create-a-service-hosted-by-iis"></a>Para criar um serviço hospedado pelo IIS  
  
1. Confirme se o IIS está instalado e em execução no computador. Para obter mais informações sobre como instalar e configurar o IIS, consulte [Instalando e Configurando o iis 7,0](https://go.microsoft.com/fwlink/?LinkID=132128)  
  
2. Crie uma nova pasta para os arquivos de aplicativo chamados "IISHostedCalcService", verifique se ASP.NET tem acesso ao conteúdo da pasta e use a ferramenta de gerenciamento do IIS para criar um novo aplicativo do IIS que está localizado fisicamente nesse diretório de aplicativo. Ao criar um alias para o diretório do aplicativo, use “IISHostedCalc”.  
  
3. Crie um novo arquivo denominado “service.svc” no diretório do aplicativo. Edite esse arquivo adicionando o seguinte @ServiceHost elemento.  
  
   ```
   <%@ServiceHost language=c# Debug="true" Service="Microsoft.ServiceModel.Samples.CalculatorService"%>
   ```  
  
4. Crie um subdiretório App_Code no diretório do aplicativo.  
  
5. Crie um novo arquivo de código denominado Service.cs no subdiretório App_Code.  
  
6. Adicione as seguintes instruções de uso na parte superior do arquivo Service.cs.  
  
    ```csharp  
    using System;  
    using System.ServiceModel;  
    ```  
  
7. Adicione a seguinte declaração de namespace depois das instruções de uso.  
  
    ```csharp  
    namespace Microsoft.ServiceModel.Samples  
    {  
    }  
    ```  
  
8. Defina o contrato de serviço na declaração do namespace conforme mostrado no código a seguir.  
  
     [!code-csharp[c_HowTo_HostInIIS#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#11)]
     [!code-vb[c_HowTo_HostInIIS#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#11)]  
  
9. Implemente o contrato de serviço depois da definição do contrato de serviço conforme mostrado no código a seguir.  
  
     [!code-csharp[c_HowTo_HostInIIS#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#12)]
     [!code-vb[c_HowTo_HostInIIS#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#12)]  
  
10. Crie um arquivo denominado "Web.config" no diretório do aplicativo e adicione o seguinte código de configuração no arquivo. Em tempo de execução, a infraestrutura do WCF usa as informações para construir um ponto de extremidade com o qual os aplicativos cliente podem se comunicar.  
  
     [!code-xml[c_HowTo_HostInIIS#100](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/common/web.config#100)]      
  
     Este exemplo especifica explicitamente pontos de extremidade no arquivo de configuração. Se você não adicionar nenhum ponto de extremidade ao serviço, o tempo de execução adicionará pontos de extremidade padrão para você. Para obter mais informações sobre pontos de extremidade padrão, associações e comportamentos, consulte [configuração simplificada](../../../../docs/framework/wcf/simplified-configuration.md) e [configuração simplificada para serviços WCF](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
11. Para verificar se o serviço está hospedado corretamente, abra uma instância do Internet Explorer e navegue para a URL do serviço: `http://localhost/IISHostedCalc/Service.svc`  
  
## <a name="example"></a>Exemplo  
 A listagem a seguir relaciona todo o código do serviço de calculadora hospedado no IIS.  
  
 [!code-csharp[C_HowTo_HostInIIS#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#1)] 
 [!code-vb[C_HowTo_HostInIIS#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#1)] 
 [!code-xml[c_HowTo_HostInIIS#100](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/common/web.config#100)]  
  
## <a name="see-also"></a>Consulte também

- [Hospedagem nos Serviços de Informações da Internet](../../../../docs/framework/wcf/feature-details/hosting-in-internet-information-services.md)
- [Hospedando serviços](../../../../docs/framework/wcf/hosting-services.md)
- [Serviços do WCF e ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)
- [Segurança](../../../../docs/framework/wcf/feature-details/security.md)
- [Recursos de hospedagem do Windows Server app Fabric](https://go.microsoft.com/fwlink/?LinkId=201276)
