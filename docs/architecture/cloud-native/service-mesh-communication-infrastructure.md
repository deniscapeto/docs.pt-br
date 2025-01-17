---
title: Infraestrutura de comunicação de malha de serviço
description: Saiba mais sobre como as tecnologias de malha de serviço simplificam a comunicação de microserviço nativa na nuvem
author: robvet
ms.date: 09/10/2019
ms.openlocfilehash: 884b3bf9afd80144a36d3328af916f1c1f12bf4f
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71214342"
---
# <a name="service-mesh-communication-infrastructure"></a>Infraestrutura de comunicação de malha de serviço

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Ao longo deste capítulo, exploramos os desafios da comunicação de microserviço. Dissemos que as equipes de desenvolvimento precisam ser sensíveis à forma como os serviços de back-end se comunicam entre si. Idealmente, quanto menos comunicação entre serviços, melhor. No entanto, evitar nem sempre é possível, pois os serviços de back-end muitas vezes dependem uns dos outros para concluir as operações.

Exploramos abordagens diferentes para implementar comunicação HTTP síncrona e mensagens assíncronas. Em cada um dos casos, o desenvolvedor está sobrecarregado com a implementação do código de comunicação. O código de comunicação é complexo e demorado. Decisões incorretas podem levar a problemas de desempenho significativos.

Uma abordagem mais moderna para os centros de comunicação de microserviço em uma nova e rápida evolução de uma tecnologia de *serviço*qualificada. Uma [malha de serviço](https://www.nginx.com/blog/what-is-a-service-mesh/) é uma camada de infraestrutura configurável com recursos internos para lidar com a comunicação de serviço a serviço, resiliência e muitas preocupações abrangentes. Ele move a responsabilidade por essas preocupações dos microserviços e da camada de malha de serviço. A comunicação é abstrata fora dos seus microserviços.

Um componente-chave de uma malha de serviço é um proxy. Em um aplicativo nativo de nuvem, uma instância de um proxy é normalmente colocalizada com cada microserviço. Enquanto eles são executados em processos separados, os dois estão fortemente vinculados e compartilham o mesmo ciclo de vida. Esse padrão, conhecido como o [padrão sidecar](https://docs.microsoft.com/azure/architecture/patterns/sidecar), e é mostrado na Figura 4-23.

![Malha de serviço com um carro lateral](./media/service-mesh-with-side-car.png)

**Figura 4-23**. Malha de serviço com um carro lateral

Observe na figura anterior como as mensagens são interceptadas por um proxy que é executado junto com cada microserviço. Cada proxy pode ser configurado com regras de tráfego específicas para o microserviço. Ele compreende mensagens e pode roteá-las entre seus serviços e o mundo exterior. 

Juntamente com o gerenciamento de comunicação serviço a serviço, a malha de serviço fornece suporte para descoberta de serviço e balanceamento de carga. 

Uma vez configurado, uma malha de serviço é altamente funcional. A malha recupera um pool de instâncias correspondente de um ponto de extremidade de descoberta de serviço. Ele envia uma solicitação para uma instância de serviço específica, registrando a latência e o tipo de resposta do resultado. Ele escolhe a instância mais provável de retornar uma resposta rápida com base em diferentes fatores, incluindo a latência observada para solicitações recentes.

Uma malha de serviço gerencia o tráfego, a comunicação e as preocupações de rede no nível do aplicativo. Ele compreende mensagens e solicitações. Uma malha de serviço normalmente se integra a um orquestrador de contêiner. O kubernetes dá suporte a uma arquitetura extensível na qual uma malha de serviço pode ser adicionada.

No capítulo 6, aprofundamos-se nas tecnologias de malha de serviço, incluindo uma discussão sobre sua arquitetura e implementações de software livre disponíveis.

## <a name="summary"></a>Resumo

Neste capítulo, discutimos padrões de comunicação nativos de nuvem. Começamos examinando como os clientes front-end se comunicam com os microserviços de back-end. Ao longo do caminho, falamos sobre plataformas de gateway de API e comunicação em tempo real. Em seguida, vimos como os microserviços se comunicam com outros serviços de back-end. Examinamos a comunicação HTTP síncrona e as mensagens assíncronas entre serviços. Abordamos o gRPC, uma tecnologia futura no mundo nativo da nuvem. Por fim, apresentamos uma nova e rápida evolução tecnológica qualificada para malha de serviço que pode simplificar a comunicação de microserviço. 

A ênfase especial foi nos serviços gerenciados do Azure que podem ajudar a implementar a comunicação em sistemas nativos de nuvem:

- [Aplicativo Azure gateway](https://docs.microsoft.com/azure/application-gateway/overview)
- [Gerenciamento de API do Azure](https://azure.microsoft.com/services/api-management/)
- [Serviço Azure SignalR](https://azure.microsoft.com/services/signalr-service/)
- [Filas do armazenamento do Azure](https://docs.microsoft.com/azure/storage/queues/storage-queues-introduction)
- [Barramento de Serviço do Azure](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview)
- [Grade de Eventos do Azure](https://docs.microsoft.com/azure/event-grid/overview)
- [Hub de eventos do Azure](https://azure.microsoft.com/services/event-hubs/)

Em seguida, mudamos para os dados distribuídos em sistemas nativos de nuvem e os benefícios e os desafios que ele apresenta.

### <a name="references"></a>Referências 

- [Microsserviços do .NET: Arquitetura para aplicativos .NET em contêineres](https://dotnet.microsoft.com/download/thank-you/microservices-architecture-ebook)
  
- [Criando comunicação entre serviços para microserviços](https://docs.microsoft.com/azure/architecture/microservices/design/interservice-communication)

- [Serviço do Azure Signalr, um serviço totalmente gerenciado para adicionar funcionalidade em tempo real](https://azure.microsoft.com/blog/azure-signalr-service-a-fully-managed-service-to-add-real-time-functionality/)
  
- [Controlador de entrada do gateway de API do Azure](https://azure.github.io/application-gateway-kubernetes-ingress/)
  
- [Sobre a entrada no serviço de kubernetes do Azure (AKS)](https://vincentlauzon.com/2018/10/10/about-ingress-in-azure-kubernetes-service-aks/)
 
- [GRPC prático](https://www.worldcat.org/title/practical-grpc/oclc/1042342319)

- [Documentação do gRPC](https://grpc.io/docs/guides/)

- [gRPC para desenvolvedores do WCF](https://bing.com) [Livro de gRPC do Mark]
  
- [Comparando serviços gRPCs com APIs HTTP](https://docs.microsoft.com/en-us/aspnet/core/grpc/comparison?view=aspnetcore-3.0)

>[!div class="step-by-step"]
>[Anterior](rest-grpc.md)
>[Próximo](distributed-data.md)
