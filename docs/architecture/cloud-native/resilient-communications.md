---
title: Comunicação resiliente
description: Arquitetando aplicativos .NET nativos da nuvem para o Azure | Comunicação resiliente
ms.date: 06/30/2019
ms.openlocfilehash: d7fd4552059f527ad5166dcb6be04248bfad8e4a
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71214497"
---
# <a name="resilient-communications"></a><span data-ttu-id="11cc5-103">Comunicações resilientes</span><span class="sxs-lookup"><span data-stu-id="11cc5-103">Resilient communications</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="11cc5-104">Em todo este livro, nós evangelizedmos os méritos de se moverem além do design de aplicativo monolítico tradicional e adotando uma arquitetura baseada em microserviço em que um conjunto de serviços distribuídos e independentes é executado de forma independente e se comunica com cada um outros usando protocolos de comunicação padrão, como HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="11cc5-104">Throughout this book, we've evangelized the merits of moving beyond traditional monolithic application design and embracing a microservice-based architecture where a set of distributed, self-contained services run independently and communicate with each other using standard communication protocols such as HTTP and HTTPS.</span></span> <span data-ttu-id="11cc5-105">Embora essa arquitetura seja comprada por muitos benefícios importantes, ela também apresenta muitos desafios.</span><span class="sxs-lookup"><span data-stu-id="11cc5-105">While such an architecture buys you many important benefits, it also presents many challenges.</span></span> <span data-ttu-id="11cc5-106">Considere, por exemplo, as seguintes preocupações:</span><span class="sxs-lookup"><span data-stu-id="11cc5-106">Consider, for example, the following concerns:</span></span>

- <span data-ttu-id="11cc5-107">*Comunicação de rede fora do processo.*</span><span class="sxs-lookup"><span data-stu-id="11cc5-107">*Out-of-process network communication.*</span></span> <span data-ttu-id="11cc5-108">Cada serviço se comunica em um protocolo de rede que apresenta congestionamento de rede, latência e falhas transitórias.</span><span class="sxs-lookup"><span data-stu-id="11cc5-108">Each service communicates over a network protocol that introduces network congestion, latency, and transient faults.</span></span>
- <span data-ttu-id="11cc5-109">*Descoberta de serviço.*</span><span class="sxs-lookup"><span data-stu-id="11cc5-109">*Service discovery.*</span></span> <span data-ttu-id="11cc5-110">Com cada serviço em execução em um cluster de computadores com seu próprio endereço IP e porta, como os serviços são descobertos e se comunicam entre si?</span><span class="sxs-lookup"><span data-stu-id="11cc5-110">With each service running across a cluster of machines with its own IP address and port, how do services discover and communicate with each other?</span></span>
- <span data-ttu-id="11cc5-111">*Resiliência.*</span><span class="sxs-lookup"><span data-stu-id="11cc5-111">*Resiliency.*</span></span> <span data-ttu-id="11cc5-112">Como gerenciar falhas de curta duração e manter o sistema estável?</span><span class="sxs-lookup"><span data-stu-id="11cc5-112">How do you manage short-lived failures and keep the system stable?</span></span>
- <span data-ttu-id="11cc5-113">*Balanceamento de carga.*</span><span class="sxs-lookup"><span data-stu-id="11cc5-113">*Load balancing.*</span></span> <span data-ttu-id="11cc5-114">Como o tráfego de entrada é distribuído entre várias instâncias de um serviço?</span><span class="sxs-lookup"><span data-stu-id="11cc5-114">How does inbound traffic get distributed across multiple instances of a service?</span></span>
- <span data-ttu-id="11cc5-115">*Segurança.*</span><span class="sxs-lookup"><span data-stu-id="11cc5-115">*Security.*</span></span> <span data-ttu-id="11cc5-116">Como as questões de segurança, como criptografia de nível de transporte e gerenciamento de certificados, são impostas?</span><span class="sxs-lookup"><span data-stu-id="11cc5-116">How are security concerns such as transport-level encryption and certificate management enforced?</span></span>
- <span data-ttu-id="11cc5-117">\* Monitoramento distribuído.</span><span class="sxs-lookup"><span data-stu-id="11cc5-117">\*Distributed Monitoring.</span></span> <span data-ttu-id="11cc5-118">-Como correlacionar e capturar a rastreabilidade e o monitoramento de uma única solicitação entre vários serviços de consumo?</span><span class="sxs-lookup"><span data-stu-id="11cc5-118">- How do you correlate and capture traceability and monitoring for a single request across multiple consuming services?</span></span>

<span data-ttu-id="11cc5-119">Embora essas preocupações possam ser tratadas com várias bibliotecas e estruturas, implementá-las dentro de sua base de código pode ser cara, complexa e demorada.</span><span class="sxs-lookup"><span data-stu-id="11cc5-119">While these concerns can be addressed with various libraries and frameworks, implementing them inside your codebase can be expensive, complex, and time-consuming.</span></span> <span data-ttu-id="11cc5-120">Além disso, você acaba com uma solução em que as preocupações com a infraestrutura são ligadas à lógica de negócios.</span><span class="sxs-lookup"><span data-stu-id="11cc5-120">Moreover, you end up with a solution where infrastructure concerns are coupled to business logic.</span></span>

## <a name="service-mesh"></a><span data-ttu-id="11cc5-121">Malha de serviço</span><span class="sxs-lookup"><span data-stu-id="11cc5-121">Service mesh</span></span>

<span data-ttu-id="11cc5-122">Uma abordagem melhor é considerar uma nova e rápida evolução da malha de *serviço*qualificada.</span><span class="sxs-lookup"><span data-stu-id="11cc5-122">A better approach is to consider a new and rapidly evolving technology entitled *Service Mesh*.</span></span> <span data-ttu-id="11cc5-123">Uma [malha de serviço](https://www.nginx.com/blog/what-is-a-service-mesh/) é uma camada de infraestrutura configurável com recursos internos para lidar com a comunicação do serviço e com muitos dos desafios mencionados acima.</span><span class="sxs-lookup"><span data-stu-id="11cc5-123">A [service mesh](https://www.nginx.com/blog/what-is-a-service-mesh/) is a configurable infrastructure layer with built-in capabilities to handle service communication and many of the challenges mentioned above.</span></span> <span data-ttu-id="11cc5-124">Ele separa essas preocupações de seu código comercial e as move para um proxy de serviço, uma instância do que acompanha cada um de seus serviços.</span><span class="sxs-lookup"><span data-stu-id="11cc5-124">It decouples these concerns from your business code and moves them into a service proxy, an instance of which accompanies each of your services.</span></span> <span data-ttu-id="11cc5-125">Geralmente conhecido como o [padrão sidecar](https://docs.microsoft.com/azure/architecture/patterns/sidecar), o proxy de malha de serviço é implantado em um processo separado para fornecer isolamento e encapsulamento do seu código comercial.</span><span class="sxs-lookup"><span data-stu-id="11cc5-125">Often referred to as the [Sidecar pattern](https://docs.microsoft.com/azure/architecture/patterns/sidecar), the service mesh proxy is deployed into a separate process to provide isolation and encapsulation from your business code.</span></span> <span data-ttu-id="11cc5-126">No entanto, o proxy está fortemente vinculado ao serviço que está sendo criado junto com ele e compartilhando seu ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="11cc5-126">However, the proxy is closely linked to the service being created along with it and sharing its lifecycle.</span></span> <span data-ttu-id="11cc5-127">A Figura 6-9 mostra esse cenário.</span><span class="sxs-lookup"><span data-stu-id="11cc5-127">Figure 6-9 shows this scenario.</span></span>

![Malha de serviço com um carro lateral](./media/service-mesh-with-side-car.png)

<span data-ttu-id="11cc5-129">**Figura 6-9**.</span><span class="sxs-lookup"><span data-stu-id="11cc5-129">**Figure 6-9**.</span></span> <span data-ttu-id="11cc5-130">Malha de serviço com um carro lateral</span><span class="sxs-lookup"><span data-stu-id="11cc5-130">Service mesh with a side car</span></span>

<span data-ttu-id="11cc5-131">Na figura anterior, observe como o proxy intercepta e gerencia a comunicação entre os microserviços e o cluster.</span><span class="sxs-lookup"><span data-stu-id="11cc5-131">In the previous figure, note how the proxy intercepts and manages communication among the microservices and the cluster.</span></span>

<span data-ttu-id="11cc5-132">Uma malha de serviço é dividida logicamente em dois componentes diferentes: Um plano de [dados](https://blog.envoyproxy.io/service-mesh-data-plane-vs-control-plane-2774e720f7fc) e um [plano de controle](https://blog.envoyproxy.io/service-mesh-data-plane-vs-control-plane-2774e720f7fc).</span><span class="sxs-lookup"><span data-stu-id="11cc5-132">A service mesh is logically split into two disparate components: A [data plane](https://blog.envoyproxy.io/service-mesh-data-plane-vs-control-plane-2774e720f7fc) and [control plane](https://blog.envoyproxy.io/service-mesh-data-plane-vs-control-plane-2774e720f7fc).</span></span> <span data-ttu-id="11cc5-133">A Figura 6-10 mostra esses componentes e suas responsabilidades.</span><span class="sxs-lookup"><span data-stu-id="11cc5-133">Figure 6-10 shows these components and their responsibilities.</span></span>

![Controle de malha de serviço e plano de dados](./media/istio-control-and-data-plane.png)

<span data-ttu-id="11cc5-135">**Figura 6-10.**</span><span class="sxs-lookup"><span data-stu-id="11cc5-135">**Figure 6-10.**</span></span> <span data-ttu-id="11cc5-136">Controle de malha de serviço e plano de dados</span><span class="sxs-lookup"><span data-stu-id="11cc5-136">Service mesh control and data plane</span></span>

<span data-ttu-id="11cc5-137">Uma vez configurado, uma malha de serviço é altamente funcional.</span><span class="sxs-lookup"><span data-stu-id="11cc5-137">Once configured, a service mesh is highly functional.</span></span> <span data-ttu-id="11cc5-138">Ele pode recuperar um pool correspondente de instâncias de um ponto de extremidade de descoberta de serviço.</span><span class="sxs-lookup"><span data-stu-id="11cc5-138">It can retrieve a corresponding pool of instances from a service discovery endpoint.</span></span> <span data-ttu-id="11cc5-139">Em seguida, ele pode enviar uma solicitação para uma instância específica, registrando a latência e o tipo de resposta do resultado.</span><span class="sxs-lookup"><span data-stu-id="11cc5-139">It can then send a request to a specific instance, recording the latency and response type of the result.</span></span> <span data-ttu-id="11cc5-140">Uma malha pode escolher a instância mais provável de retornar uma resposta rápida com base em vários fatores, incluindo sua latência observada para solicitações recentes.</span><span class="sxs-lookup"><span data-stu-id="11cc5-140">A mesh can choose the instance most likely to return a fast response based on many factors, including its observed latency for recent requests.</span></span>

<span data-ttu-id="11cc5-141">Se uma instância não estiver respondendo ou falhar, a malha poderá repetir a solicitação em outra instância.</span><span class="sxs-lookup"><span data-stu-id="11cc5-141">If an instance is unresponsive or fails, the mesh can retry the request on another instance.</span></span> <span data-ttu-id="11cc5-142">Se um pool retornar erros de forma consistente, uma malha poderá removê-lo do pool de balanceamento de carga para ser repetido periodicamente mais tarde depois de ser reparado.</span><span class="sxs-lookup"><span data-stu-id="11cc5-142">If a pool consistently returns errors, a mesh can evict it from the load-balancing pool to be retried periodically later after it heals.</span></span> <span data-ttu-id="11cc5-143">Se uma solicitação atingir o tempo limite, uma malha poderá falhar e, em seguida, repetir a solicitação.</span><span class="sxs-lookup"><span data-stu-id="11cc5-143">If a request times out, a mesh can fail and then retry the request.</span></span> <span data-ttu-id="11cc5-144">Uma malha captura o comportamento na forma de métricas e no rastreamento distribuído, que pode ser emitido para um sistema de métricas centralizado.</span><span class="sxs-lookup"><span data-stu-id="11cc5-144">A mesh captures behavior in the form of metrics and distributed tracing, which then can be emitted to a centralized metrics system.</span></span>

## <a name="istio-and-envoy"></a><span data-ttu-id="11cc5-145">İSTİO e Envoy</span><span class="sxs-lookup"><span data-stu-id="11cc5-145">Istio and Envoy</span></span>

<span data-ttu-id="11cc5-146">Embora algumas opções de malha de serviço existam atualmente, a [İSTİO](https://istio.io/docs/concepts/what-is-istio/) é a mais popular no momento da elaboração deste artigo.</span><span class="sxs-lookup"><span data-stu-id="11cc5-146">While a few service mesh options currently exist, [Istio](https://istio.io/docs/concepts/what-is-istio/) is the most popular as of the time of this writing.</span></span> <span data-ttu-id="11cc5-147">Uma joint venture da IBM, do Google e do lyft, é uma oferta de software livre que pode ser integrada a um aplicativo distribuído novo ou existente.</span><span class="sxs-lookup"><span data-stu-id="11cc5-147">A joint venture from IBM, Google, and Lyft, it's an open-source offering that can be integrated into a new or existing distributed application.</span></span> <span data-ttu-id="11cc5-148">Ele fornece uma solução consistente e completa para proteger, conectar e monitorar os microserviços.</span><span class="sxs-lookup"><span data-stu-id="11cc5-148">It provides a consistent and complete solution to secure, connect, and monitor microservices.</span></span> <span data-ttu-id="11cc5-149">Seus recursos incluem:</span><span class="sxs-lookup"><span data-stu-id="11cc5-149">Its features include:</span></span>

- <span data-ttu-id="11cc5-150">Proteja a comunicação entre serviços em um cluster com autenticação e autorização baseadas em identidade forte.</span><span class="sxs-lookup"><span data-stu-id="11cc5-150">Secure service-to-service communication in a cluster with strong identity-based authentication and authorization.</span></span>
- <span data-ttu-id="11cc5-151">Balanceamento de carga automático para tráfego HTTP, [gRPC](https://grpc.io/), WebSocket e TCP.</span><span class="sxs-lookup"><span data-stu-id="11cc5-151">Automatic load balancing for HTTP, [gRPC](https://grpc.io/), WebSocket, and TCP traffic.</span></span>
- <span data-ttu-id="11cc5-152">Controle refinado do comportamento de tráfego com regras de roteamento avançadas, repetições, failovers e injeção de falha.</span><span class="sxs-lookup"><span data-stu-id="11cc5-152">Fine-grained control of traffic behavior with rich routing rules, retries, failovers, and fault injection.</span></span>
- <span data-ttu-id="11cc5-153">Uma camada de política conectável e uma API de configuração que dão suporte a controles de acesso, limites de taxa e cotas.</span><span class="sxs-lookup"><span data-stu-id="11cc5-153">A pluggable policy layer and configuration API supporting access controls, rate limits, and quotas.</span></span>
- <span data-ttu-id="11cc5-154">Métricas, logs e rastreamentos automáticos para todo o tráfego em um cluster, incluindo a entrada e saída do cluster.</span><span class="sxs-lookup"><span data-stu-id="11cc5-154">Automatic metrics, logs, and traces for all traffic within a cluster, including cluster ingress and egress.</span></span>

<span data-ttu-id="11cc5-155">Um componente fundamental para uma implementação de İSTİO é um serviço de proxy intitulado The [Envoy proxy](https://www.envoyproxy.io/docs/envoy/latest/intro/what_is_envoy).</span><span class="sxs-lookup"><span data-stu-id="11cc5-155">A key component for an Istio implementation is a proxy service entitled the [Envoy proxy](https://www.envoyproxy.io/docs/envoy/latest/intro/what_is_envoy).</span></span> <span data-ttu-id="11cc5-156">Provenientes de lyft e subsequentemente contribuíram para a [base de computação nativa de nuvem](https://www.cncf.io/) (discutida no capítulo 1), o proxy Envoy é executado junto com cada serviço e fornece uma base independente de plataforma para os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="11cc5-156">Originating from Lyft and subsequently contributed to the [Cloud Native Computing Foundation](https://www.cncf.io/) (discussed in chapter 1), the Envoy proxy runs alongside each service and provides a platform-agnostic foundation for the following features:</span></span>

- <span data-ttu-id="11cc5-157">Descoberta dinâmica de serviço.</span><span class="sxs-lookup"><span data-stu-id="11cc5-157">Dynamic service discovery.</span></span>
- <span data-ttu-id="11cc5-158">Balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="11cc5-158">Load balancing.</span></span>
- <span data-ttu-id="11cc5-159">Término do TLS.</span><span class="sxs-lookup"><span data-stu-id="11cc5-159">TLS termination.</span></span>
- <span data-ttu-id="11cc5-160">Proxies HTTP e gRPC.</span><span class="sxs-lookup"><span data-stu-id="11cc5-160">HTTP and gRPC proxies.</span></span>
- <span data-ttu-id="11cc5-161">Resiliência do disjuntor.</span><span class="sxs-lookup"><span data-stu-id="11cc5-161">Circuit breaker resiliency.</span></span>
- <span data-ttu-id="11cc5-162">Verificações de integridade.</span><span class="sxs-lookup"><span data-stu-id="11cc5-162">Health checks.</span></span>
- <span data-ttu-id="11cc5-163">Atualizações sem interrupção com implantações do [canário](https://martinfowler.com/bliki/CanaryRelease.html) .</span><span class="sxs-lookup"><span data-stu-id="11cc5-163">Rolling updates with [canary](https://martinfowler.com/bliki/CanaryRelease.html) deployments.</span></span>

<span data-ttu-id="11cc5-164">Conforme discutido anteriormente, o Envoy é implantado como um sidecar para cada microserviço no cluster.</span><span class="sxs-lookup"><span data-stu-id="11cc5-164">As previously discussed, Envoy is deployed as a sidecar to each microservice in the cluster.</span></span>

## <a name="integration-with-azure-kubernetes-services"></a><span data-ttu-id="11cc5-165">Integração com os serviços Kubernetess do Azure</span><span class="sxs-lookup"><span data-stu-id="11cc5-165">Integration with Azure Kubernetes Services</span></span>

<span data-ttu-id="11cc5-166">A nuvem do Azure adota o İSTİO e fornece suporte direto para ele nos serviços Kubernetess do Azure.</span><span class="sxs-lookup"><span data-stu-id="11cc5-166">The Azure cloud embraces Istio and provides direct support for it within Azure Kubernetes Services.</span></span> <span data-ttu-id="11cc5-167">Os links a seguir podem ajudá-lo a começar:</span><span class="sxs-lookup"><span data-stu-id="11cc5-167">The following links can help you get started:</span></span>

- [<span data-ttu-id="11cc5-168">Instalando o İSTİO no AKS</span><span class="sxs-lookup"><span data-stu-id="11cc5-168">Installing Istio in AKS</span></span>](https://docs.microsoft.com/azure/aks/istio-install)
- [<span data-ttu-id="11cc5-169">Usando AKS e İSTİO</span><span class="sxs-lookup"><span data-stu-id="11cc5-169">Using AKS and Istio</span></span>](https://docs.microsoft.com/azure/aks/istio-scenario-routing)

>[!div class="step-by-step"]
><span data-ttu-id="11cc5-170">[Anterior](infrastructure-resiliency-azure.md)
>[Próximo](monitoring-health.md)</span><span class="sxs-lookup"><span data-stu-id="11cc5-170">[Previous](infrastructure-resiliency-azure.md)
[Next](monitoring-health.md)</span></span>