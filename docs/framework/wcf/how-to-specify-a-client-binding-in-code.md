---
title: 'Como: especificar uma associação de cliente no código'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6bee5da4-adf7-42e6-8f78-63a9e5c6dbad
ms.openlocfilehash: 37769a84ca623e2f7f246d36180aa17537e90bfa
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70990228"
---
# <a name="how-to-specify-a-client-binding-in-code"></a>Como: especificar uma associação de cliente no código
Neste exemplo, um cliente é criado para usar um serviço de calculadora e a associação para esse cliente é especificada imperativamente no código. O cliente acessa o `CalculatorService`, que implementa a `ICalculator` interface, e o serviço e o cliente usam a <xref:System.ServiceModel.BasicHttpBinding> classe.  
  
 Este procedimento pressupõe que o serviço de calculadora está em execução. Para obter informações sobre como criar o serviço [, consulte Como: Especifique uma associação de serviço na](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)configuração. Ele também usa a [ferramenta de utilitário de metadados ServiceModel (svcutil. exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)Windows Communication Foundation (WCF) fornece para gerar automaticamente os componentes do cliente. A ferramenta gera o código do cliente para acessar o serviço.  
  
 O cliente é criado em duas partes. Svcutil. exe gera o `ClientCalculator` que implementa a `ICalculator` interface. Esse aplicativo cliente é então construído pela construção de uma instância do `ClientCalculator` e, em seguida, pela especificação da associação e do endereço do serviço no código.  
  
 Para a cópia de origem deste exemplo, consulte o exemplo de [BasicBinding](../../../docs/framework/wcf/samples/basicbinding.md) .  
  
### <a name="to-specify-a-custom-binding-in-code"></a>Para especificar uma associação personalizada no código  
  
1. Use svcutil. exe da linha de comando para gerar código de metadados de serviço.  
  
    ```console  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2. O cliente gerado contém a `ICalculator` interface que define o contrato de serviço que a implementação do cliente deve satisfazer.  
  
     [!code-csharp[C_HowTo_CodeClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#1)]
     [!code-vb[C_HowTo_CodeClientBinding#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#1)]  
  
3. O cliente gerado também contém a implementação do `ClientCalculator`.  
  
     [!code-csharp[C_HowTo_CodeClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#2)]
     [!code-vb[C_HowTo_CodeClientBinding#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#2)]  
  
4. Crie uma instância do `ClientCalculator` que usa a <xref:System.ServiceModel.BasicHttpBinding> classe em um aplicativo cliente e, em seguida, chame as operações de serviço no endereço especificado.  
  
     [!code-csharp[C_HowTo_CodeClientBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#3)]
     [!code-vb[C_HowTo_CodeClientBinding#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#3)]  
  
5. Compile e execute o cliente.  
  
## <a name="see-also"></a>Consulte também

- [Usando associações para configurar serviços e clientes](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
