---
title: Azure Monitor
description: Usar Azure Monitor para obter visibilidade do seu sistema está em execução.
ms.date: 09/23/2019
ms.openlocfilehash: 20048792e95ef1f6e75551cdd0d3571f972f6c14
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71214097"
---
# <a name="azure-monitor"></a>Azure Monitor 

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Nenhum outro provedor de nuvem tem o mesmo que uma solução de monitoramento de aplicativo em nuvem, como foi encontrada no Azure. Azure Monitor é um nome abrangente para uma coleção de ferramentas projetadas para fornecer visibilidade do estado do seu sistema, informações sobre quaisquer problemas e otimização do seu aplicativo. 

![Azure Monitor, uma coleção de ferramentas para fornecer informações sobre como um aplicativo nativo de nuvem está funcionando. **Figura 7-9**. ](./media/azure-monitor.png)
 Azure Monitor, uma coleção de ferramentas para fornecer informações sobre como um aplicativo nativo de nuvem está funcionando.

## <a name="gathering-logs-and-metrics"></a>Coletando logs e métricas

A primeira etapa em qualquer solução de monitoramento é reunir o máximo de dados possível. Quanto mais dados puderem ser coletados, mais detalhadamente as informações podem ser obtidas. Os sistemas de instrumentação tradicionalmente eram difíceis. O SNMP (Simple Network Management Protocol) era o protocolo Gold Standard para coletar informações no nível do computador, mas exigia um grande conhecimento e configuração. Felizmente, grande parte desse trabalho árduo foi eliminado, pois as métricas mais comuns são coletadas automaticamente pelo Azure Monitor.

Os eventos e as métricas de nível de aplicativo não são possíveis para instrumentar automaticamente porque são locais para o aplicativo que está sendo implantado. Para reunir essas métricas, há [SDKs e APIs disponíveis](https://docs.microsoft.com/azure/azure-monitor/app/api-custom-events-metrics) para relatar diretamente essas informações, como quando um cliente se inscreve ou conclui um pedido. As exceções também podem ser capturadas e relatadas de volta para Azure Monitor por meio de Application Insights. Os SDKs dão suporte à maioria de todos os idiomas encontrados em aplicativos nativos de nuvem, incluindo Go, Python, JavaScript e linguagens .NET.

O objetivo final da coleta de informações sobre o estado do seu aplicativo é garantir que seus usuários finais tenham uma boa experiência. Qual é a melhor maneira de saber se os usuários estão enfrentando problemas do que fazer [testes da Web externos](https://docs.microsoft.com/azure/azure-monitor/app/monitor-web-app-availability)? Esses testes podem ser tão simples quanto executar ping em seu site de locais em todo o mundo ou se envolver como os agentes fazem logon no site e executam ações.

## <a name="reporting-data"></a>Dados de relatórios

Depois que os dados são coletados, eles podem ser manipulados, resumidos e plotados em gráficos, o que permite que os usuários vejam instantaneamente quando há problemas. Esses gráficos podem ser coletados em painéis ou em pastas de trabalho, um relatório de várias páginas projetado para contar uma história sobre algum aspecto do sistema.

Nenhum aplicativo moderno estaria completo sem alguma inteligência artificial ou aprendizado de máquina. Para esse fim, os dados [podem ser passados](https://www.youtube.com/watch?v=Cuza-I1g9tw) para as várias ferramentas de aprendizado de máquina no Azure para permitir que você extraia tendências e informações que, de outra forma, seriam ocultas.

Application Insights fornece uma linguagem de consulta avançada chamada Kusto que pode ser usada para localizar registros, resumir-los e até mesmo gráficos de plotagem. Por exemplo, essa consulta localizará todos os registros do mês de novembro de 2007, agrupando-os por Estado e plotará os 10 primeiros como um gráfico de pizza.

```
StormEvents 
| where StartTime >= datetime(2007-11-01) and StartTime < datetime(2007-12-01)
| summarize count() by State
| top 10 by count_
| render piechart 
```

![O resultado da Application insights de consulta](./media/azure-monitor.png)
da**Figura 7-10**. O resultado da consulta de Application Insights.

Há um [playground para experimentar consultas Kusto](https://dataexplorer.azure.com/clusters/help/databases/Samples) , que é um lugar fantástico para gastar uma ou duas horas. A leitura de [consultas de exemplo](https://docs.microsoft.com/azure/kusto/query/samples) também pode ser instrutiva.

## <a name="dashboards"></a>Painéis

Há várias tecnologias de painel diferentes que podem ser usadas para trazer as informações de Azure Monitor. Talvez a mais simples seja apenas executar consultas em Application Insights e [plotar os dados em um gráfico](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-app-dashboards). 

![Um exemplo de gráficos de Application insights incorporados no painel](./media/azure-monitor.png)
principal do Azure,**Figura 7-11**. Um exemplo de gráficos de Application Insights incorporados no painel principal do Azure.

Esses gráficos podem então ser inseridos no portal do Azure apropriado pelo uso do recurso de painel. Para os usuários com mais requisitos de ação, como a possibilidade de fazer uma busca detalhada em várias camadas de dados Azure Monitor dados estão disponíveis para [Power bi](https://powerbi.microsoft.com/). Power BI é uma ferramenta de classe empresarial, líder do setor, business intelligence que pode agregar dados de várias fontes de dados diferentes.

![Um exemplo Power bi a](./media/azure-monitor.png)
**Figura 7-12**do painel. Um exemplo Power BI Dashboard.

## <a name="alerts"></a>Alertas

Às vezes, ter painéis de dados é insuficiente. Se ninguém estiver atento a assistir aos painéis, ele ainda poderá ser muitas horas antes que um problema seja resolvido ou até mesmo detectado. Para esse fim, Azure Monitor também fornece uma solução de [alerta](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview)de entalhe superior. Os alertas podem ser disparados por uma ampla gama de condições, incluindo:

* Valores de métrica
* Consultas de pesquisa de log
* Eventos do log de atividades
* Integridade da plataforma subjacente do Azure
* Testes de disponibilidade do site

Quando disparado, os alertas podem executar uma ampla variedade de tarefas. No lado simples, os alertas podem apenas enviar uma notificação por email para uma lista de endereçamento ou uma mensagem de texto para um indivíduo. Alertas mais envolvidos podem disparar um fluxo de trabalho em uma ferramenta como PagerDuty, que reconhece quem está em chamada para um determinado aplicativo. Os alertas podem disparar ações no [Microsoft Flow](https://flow.microsoft.com/) desbloqueando possibilidades ilimitadas para fluxos de trabalho.

Como as causas comuns dos alertas são identificadas, os alertas podem ser aprimorados com detalhes sobre as causas comuns dos alertas e as etapas a serem seguidas para resolvê-los. Implantações de aplicativos nativos de nuvem altamente maduras podem optar por disparar tarefas de auto-recuperação, que executam ações como remover nós com falha de um conjunto de dimensionamento ou disparar uma atividade de dimensionamento automático. Eventualmente, talvez não seja mais necessário ativar o pessoal de chamada em 2AM para resolver um problema de site ativo, pois o sistema poderá se ajustar para compensar ou pelo menos limp até que alguém chegue ao trabalho na manhã seguinte. 

Azure Monitor aproveita automaticamente o aprendizado de máquina para entender os parâmetros operacionais normais dos aplicativos implantados. Isso permite que ele detecte serviços que estão operando fora de seus parâmetros normais. Por exemplo, o tráfego de dia da semana típico no site pode ser 10.000 solicitações por minuto. E, em seguida, em uma determinada semana, repentinamente, o número de solicitações atinge um 20.000 de solicitações altamente incomuns por minuto. A [detecção inteligente](https://docs.microsoft.com/azure/azure-monitor/app/proactive-diagnostics) notará esse desvio da norma e disparará um alerta. Ao mesmo tempo, a análise de tendência é inteligente o suficiente para evitar o acionamento de falsos positivos quando a carga de tráfego é esperada.  

>[!div class="step-by-step"]
>[Anterior](monitoring-azure-kubernetes.md)
>[Próximo](identity.md)
