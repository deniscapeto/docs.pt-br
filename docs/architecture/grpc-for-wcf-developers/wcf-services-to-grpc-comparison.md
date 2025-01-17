---
title: Comparando o WCF com o gRPC-gRPC para desenvolvedores do WCF
description: Uma comparação das estruturas do WCF e do gRPC para a criação de aplicativos distribuídos.
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: c763048d09e7ed5ca0a3d5240f6b3cf5262f897c
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184039"
---
# <a name="comparing-wcf-to-grpc"></a>Comparando o WCF com o gRPC

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

O capítulo anterior deve ter dado a você uma boa visão do Protobuf e como o gRPC lida com as mensagens. Antes de trabalhar em uma conversão detalhada do WCF para o gRPC, é importante observar como a variedade de recursos disponíveis atualmente no WCF é tratada em gRPC e quais soluções alternativas você pode usar quando não parece haver um equivalente gRPC. Em particular, este capítulo abordará os seguintes assuntos:

- Operações e métodos
- Associações e transportes
- Tipos de RPC
- Metadados
- Tratamento de erros
- WS-\* Protocols

## <a name="grpc-example"></a>exemplo de gRPC

Quando você cria um novo projeto ASP.NET Core 3,0 gRPC no Visual Studio 2019 ou na linha de comando, o equivalente de gRPC de "Olá, Mundo" é gerado para você. Ele consiste em um `greeter.proto` arquivo que define o serviço e suas mensagens, e um `GreeterService.cs` arquivo com uma implementação do serviço.

```protobuf
syntax = "proto3";

option csharp_namespace = "HelloGrpc";

package Greet;

// The greeting service definition.
service Greeter {
  // Sends a greeting
  rpc SayHello (HelloRequest) returns (HelloReply);
}

// The request message containing the user's name.
message HelloRequest {
  string name = 1;
}

// The response message containing the greetings.
message HelloReply {
  string message = 1;
}
```

```csharp
using System.Threading.Tasks;
using Grpc.Core;
using Microsoft.Extensions.Logging;

namespace HelloGrpc
{
    public class GreeterService : Greeter.GreeterBase
    {
        private readonly ILogger<GreeterService> _logger;
        public GreeterService(ILogger<GreeterService> logger)
        {
            _logger = logger;
        }

        public override Task<HelloReply> SayHello(HelloRequest request, ServerCallContext context)
        {
            return Task.FromResult(new HelloReply
            {
                Message = "Hello " + request.Name
            });
        }
    }
}
```

Este capítulo fará referência a este código de exemplo ao explicar vários conceitos e recursos do gRPC.

>[!div class="step-by-step"]
>[Anterior](protobuf-maps.md)
>[Próximo](wcf-endpoints-grpc-methods.md)
