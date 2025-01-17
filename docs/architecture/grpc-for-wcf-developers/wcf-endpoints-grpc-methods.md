---
title: Pontos de extremidade do WCF e métodos de gRPC – gRPC para desenvolvedores do WCF
description: Comparação de pontos de extremidade do WCF declarados com os atributos ServiceContract e OperationContract, e os métodos gRPC declarados em Protobuf
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: 08f2d0874417c0ca319b0c193e6108536376d693
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184060"
---
# <a name="wcf-endpoints-and-grpc-methods"></a>Pontos de extremidade do WCF e métodos gRPC

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

No WCF, quando você estiver escrevendo o código do aplicativo, use um dos seguintes métodos:

- Você escreve o código do aplicativo em uma classe e decora métodos com o atributo [OperationContract](xref:System.ServiceModel.OperationContractAttribute) .
- Você declara uma interface para o serviço e adiciona atributos [OperationContract](xref:System.ServiceModel.OperationContractAttribute) à interface.

Por exemplo, o equivalente do WCF do `greet.proto` serviço de saudação pode ser escrito da seguinte maneira:

```csharp
[ServiceContract]
public interface IGreeterService
{
    [OperationContract]
    string SayHello(string name);
}
```

O capítulo 3 mostrou que as definições de mensagem Protobuf são usadas para gerar classes de dados. Declarações de serviço e método são usadas para gerar classes base que você herda de para implementar o serviço. Você apenas declara os métodos a serem implementados no `.proto` arquivo e o compilador gera uma classe base com métodos virtuais que você deve substituir.

## <a name="operationcontract-properties"></a>Propriedades de OperationContract

O atributo [OperationContract](xref:System.ServiceModel.OperationContractAttribute) tem propriedades para controlar ou refinar como ele funciona. os métodos gRPC não oferecem esse tipo de controle. A tabela a seguir define essas `OperationContract` Propriedades e como a funcionalidade que elas especificam é (ou não) lida com o no gRPC:

| Propriedade `OperationContract` | gRPC                                             |
| ---------------------------- | ------------------------------------------------ |
| <xref:System.ServiceModel.OperationContractAttribute.Action>             | URI que identifica a operação. gRPC `package`usa o nome do `service` e `rpc` do `.proto` arquivo. |
| <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern>       | Todos os métodos de serviço `Task` gRPC retornam objetos. |
| <xref:System.ServiceModel.OperationContractAttribute.IsInitiating>       | Consulte a observação abaixo. |
| <xref:System.ServiceModel.OperationContractAttribute.IsOneWay>           | Métodos gRPC unidirecionais retornam `Empty` resultados ou usam o streaming de cliente. |
| <xref:System.ServiceModel.OperationContractAttribute.IsTerminating>      | Consulte a observação abaixo. |
| <xref:System.ServiceModel.OperationContractAttribute.Name>               | Relacionado ao SOAP, não há significado em gRPC. |
| <xref:System.ServiceModel.OperationContractAttribute.ProtectionLevel>    | Sem criptografia de mensagem; criptografia de rede tratada na camada de transporte (TLS sobre HTTP/2). |
| <xref:System.ServiceModel.OperationContractAttribute.ReplyAction>        | Relacionado ao SOAP, não há significado em gRPC. |

A `IsInitiating` propriedade permite que você indique que um método em um [ServiceContract](xref:System.ServiceModel.ServiceContractAttribute) não pode ser o primeiro método chamado como parte de uma sessão. A `IsTerminating` Propriedade faz com que o servidor feche a sessão depois que uma operação é chamada (ou o cliente, se usado em um cliente de retorno de chamada). No gRPC, os fluxos são criados por métodos únicos e fechados explicitamente. Consulte [streaming do gRPC](rpc-types.md#grpc-streaming).

Para obter mais informações sobre segurança e criptografia do gRPC, consulte o [capítulo 6](security.md).

>[!div class="step-by-step"]
>[Anterior](wcf-services-to-grpc-comparison.md)
>[Próximo](wcf-bindings.md)
