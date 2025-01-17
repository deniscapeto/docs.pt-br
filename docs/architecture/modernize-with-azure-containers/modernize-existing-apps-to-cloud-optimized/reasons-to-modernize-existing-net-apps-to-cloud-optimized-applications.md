---
title: Motivos para modernizar aplicativos .NET existentes para aplicativos otimizados para a nuvem
description: Modernizar aplicativos .NET existentes com contêineres de nuvem e Windows do Azure | Motivos para modernizar aplicativos .NET existentes para aplicativos otimizados para a nuvem
ms.date: 04/28/2018
ms.openlocfilehash: aabce73efaae520a3b59c70d53519b847f2c6a94
ms.sourcegitcommit: c70542d02736e082e8dac67dad922c19249a8893
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70373928"
---
# <a name="reasons-to-modernize-existing-net-apps-to-cloud-optimized-applications"></a>Motivos para modernizar aplicativos .NET existentes para aplicativos otimizados para a nuvem

Com um aplicativo otimizado para a nuvem, você pode entregar aplicativos confiáveis de forma rápida e repetida aos seus clientes. Você obterá agilidade e confiabilidade essenciais ao adiar grande parte da complexidade operacional de seu aplicativo para a plataforma.

Se você não puder colocar seus aplicativos no mercado rapidamente, no momento em que enviar seu aplicativo, o mercado que você estava direcionando terá evoluído. Você pode estar muito tarde, independentemente de quão bem o aplicativo foi projetado ou projetado. Você pode estar falhando ou não atingindo seu potencial completo porque não é possível sincronizar a entrega do aplicativo com as necessidades do mercado.

A necessidade de inovação de negócios contínua envia as equipes de desenvolvimento e operações para o limite. A única maneira de atingir a agilidade de que você precisa na inovação de negócios contínua é modernizar seus aplicativos com tecnologias como contêineres e princípios específicos de aplicativos otimizados para nuvem.

O resultado final é que, quando uma organização cria e gerencia aplicativos que são otimizados para a nuvem, ele pode colocar soluções em mãos de clientes mais cedo e trazer novas ideias para o mercado quando forem relevantes.

## <a name="cloud-optimized-application-principles-and-tenets"></a>Princípios e filosofias de aplicativos otimizados para nuvem 

Os aprimoramentos na nuvem estão principalmente concentrados em atender a dois objetivos: Reduza os custos e melhore o crescimento dos negócios, melhorando a agilidade. Essas metas são obtidas simplificando os processos e reduzindo o conflito quando você libera e envia aplicativos.

Seu aplicativo será otimizado para a nuvem se você puder de uma maneira ágil – desenvolver seu aplicativo de forma autônoma de outros aplicativos locais e, em seguida, liberar, implantar, dimensionar automaticamente, monitorar e solucionar problemas de seu aplicativo na nuvem.

A chave é a *agilidade*. Não é possível enviar com agilidade, a menos que você reduza para um mínimo absoluto problemas de implantação para produção e problemas de ambiente de desenvolvimento/teste. Os contêineres (especificamente, o Docker, como um padrão de fato) e os serviços gerenciados foram projetados especificamente para essa finalidade.

Para obter agilidade, você também precisa de processos DevOps automatizados baseados em pipelines de CI/CD que são liberados para plataformas escalonáveis na nuvem. As plataformas de CI/CD (como Azure DevOps Services ou Jenkins) que são implantadas em uma plataforma de nuvem escalonável e resiliente (como o serviço Azure App ou o serviço kubernetes do Azure) são as principais tecnologias para alcançar a agilidade na nuvem.

A lista a seguir descreve as principais filosofias ou práticas para aplicativos otimizados para a nuvem. Observe que você pode adotar todos ou apenas alguns desses princípios, em uma abordagem progressiva ou incremental:

- **Contêineres**. Os contêineres oferecem a capacidade de incluir dependências de aplicativo com o próprio aplicativo. A Containerização reduz significativamente o número de problemas que você pode encontrar ao implantar em ambientes de produção ou teste em ambientes de preparo. Por fim, os contêineres melhoram a agilidade da entrega de aplicativos.

- **Nuvem resiliente e escalonável**. A nuvem fornece uma plataforma gerenciada, elástica, escalonável e resiliente. Essas características são fundamentais para obter melhorias de custos e enviar aplicativos altamente disponíveis e confiáveis em uma entrega contínua. Serviços gerenciados como bancos de dados gerenciados, CaaS (cache como serviço) gerenciado e armazenamento gerenciado são partes fundamentais para aliviar os custos de manutenção de seu aplicativo.

- **Monitoramento**. Você não pode ter um aplicativo confiável sem ter uma boa maneira de detectar e diagnosticar exceções e problemas de desempenho de aplicativos. Você precisa obter informações acionáveis por meio do gerenciamento de desempenho de aplicativos e análise instantânea.

- **Cultura DevOps e entrega contínua**. A adoção de práticas de DevOps requer uma alteração cultural na qual as equipes não trabalham mais em silos independentes. Os pipelines de CI/CD são possíveis apenas quando há uma colaboração maior entre as equipes de operações de desenvolvimento e de ti, com suporte de contêineres e de ferramentas de CI/CD.

A Figura 4-2 mostra os principais pilares opcionais de um aplicativo otimizado para a nuvem. Quanto mais pilares você implementar, o readier seu aplicativo será ter sucesso ao atender às expectativas dos clientes.

![Principais pilares de um aplicativo otimizado para nuvem](./media/image2.png)

**Figura 4-2.** Principais pilares de um aplicativo otimizado para nuvem

Para resumir, um aplicativo otimizado para a nuvem é uma abordagem para criar e gerenciar aplicativos que aproveitam o modelo de computação em nuvem, ao usar uma combinação de contêineres, infraestrutura de nuvem gerenciada, técnicas de aplicativos resilientes, monitoramento, entrega contínua e DevOps, tudo sem a necessidade de rearquitetar e recodificar seus aplicativos existentes.

Sua organização pode adotar essas tecnologias e abordagens gradualmente. Você não precisa adotar todos eles de uma só vez. Você pode adotá-los de forma incremental, dependendo das necessidades de usuários e das prioridades da empresa.

## <a name="benefits-of-a-cloud-optimized-application"></a>Benefícios de um aplicativo otimizado para a nuvem

Você pode obter os seguintes benefícios convertendo um aplicativo existente em um aplicativo otimizado para a nuvem (sem rearquitetar ou codificar):

- **Reduza os custos, pois a infraestrutura gerenciada é tratada pelo provedor de nuvem**. Os aplicativos otimizados para a nuvem obtêm os benefícios da nuvem usando a elasticidade, o dimensionamento automático e a alta disponibilidade prontos para uso da nuvem. Os benefícios estão relacionados não apenas aos recursos de computação (VMs e contêineres), mas também dependem dos recursos na nuvem, como DBaaS, CaaS e qualquer infraestrutura que um aplicativo possa precisar.

- **Aplicativo e infraestrutura resilientes**. Ao migrar para a nuvem, você precisa adotar falhas transitórias; as falhas ocorrerão na nuvem. Além disso, a infraestrutura de nuvem e o hardware são "substituíveis", o que aumenta as oportunidades de tempo de inatividade transitório. Ao mesmo tempo, os recursos de nuvem interna e determinadas técnicas de desenvolvimento de aplicativos que implementam resiliência e automatizam a recuperação facilitam muito a recuperação de falhas inesperadas na nuvem.

- **Informações aprofundadas**sobre o desempenho do aplicativo. Ferramentas de monitoramento de nuvem, como o Aplicativo Azure insights, fornecem visualização para gerenciamento de integridade, registro em log e notificações. Os logs de auditoria tornam os aplicativos fáceis de depurar e auditar, fundamentais para um aplicativo de nuvem confiável.

- **Portabilidade do aplicativo, com implantações Agile**. Os contêineres (contêineres do Linux ou do Windows baseados no mecanismo do Docker) oferecem a melhor solução para evitar um aplicativo bloqueado na nuvem. Usando contêineres, hosts do Docker e orquestradores de várias nuvens, você pode facilmente mover de um ambiente ou nuvem para outro. Os contêineres eliminam o conflito que normalmente ocorre em implantações em qualquer ambiente (estágio/teste/produção).

Em última análise, todos esses benefícios fornecem reduções de custo-chave para o ciclo de vida de seu aplicativo de ponta a ponta.

Nas seções a seguir, esses benefícios são explicados em mais detalhes e são vinculados a tecnologias específicas.

>[!div class="step-by-step"]
>[Anterior](index.md)
>[Próximo](microsoft-technologies-in-cloud-optimized-applications.md)
