---
ms.openlocfilehash: 9605352c66f85b6942ba24942cb07c88bdd81f2a
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67857505"
---
### <a name="connection-pool-blocking-period-for-azure-sql-databases-is-removed"></a>Período de bloqueio do pool de conexões para bancos de dados SQL do Azure removido

|   |   |
|---|---|
|Detalhes|A partir do .NET Framework 4.6.2, para solicitações de abertura da conexão com bancos de dados SQL do Azure conhecidos (*.database.windows.net, *.database.chinacloudapi.cn, *.database.usgovcloudapi.net, *.database.cloudapi.de), o período de bloqueio do pool de conexões foi removido e os erros de abertura da conexão não são armazenados em cache. As tentativas de repetir as solicitações de abertura de conexão ocorrerão quase que imediatamente após os erros de conexão transitórios. Essa alteração permite que a tentativa de abertura da conexão seja repetida imediatamente para bancos de dados SQL do Azure, melhorando, assim, o desempenho dos aplicativos habilitados para a nuvem. Para todas as outras tentativas de conexão, o período de bloqueio do pool de conexões continuará sendo imposto.<p/>No .NET Framework 4.6.1 e nas versões anteriores, quando um aplicativo encontra uma falha de conexão transitória ao conectar-se a um banco de dados, a tentativa de conexão não pode ser repetida rapidamente porque o pool de conexões armazena o erro em cache e gera-o novamente por um tempo que varia de 5 segundos a 1 minuto. Para obter mais informações, confira [Pooling de conexão do SQL Server (ADO.NET)](~/docs/framework/data/adonet/sql-server-connection-pooling.md). Esse comportamento é problemático para conexões com bancos de dados SQL do Azure que, muitas vezes, falham com erros transitórios que normalmente são recuperados em alguns segundos. O recurso de bloqueio do pool de conexões significa que o aplicativo não pode se conectar ao banco de dados por um período extenso, mesmo que o banco de dados esteja disponível e o aplicativo precise ser renderizado em alguns segundos.|
|Sugestão|Se esse comportamento for indesejável, o período de bloqueio do pool de conexões poderá ser configurado definindo a propriedade <xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod?displayProperty=name> introduzida no .NET Framework 4.6.2. O valor da propriedade é membro da enumeração <xref:System.Data.SqlClient.PoolBlockingPeriod?displayProperty=name> que pode assumir um dos três valores:<ul><li><xref:System.Data.SqlClient.PoolBlockingPeriod.AlwaysBlock></li><li><xref:System.Data.SqlClient.PoolBlockingPeriod.Auto></li><li><xref:System.Data.SqlClient.PoolBlockingPeriod.NeverBlock></li></ul>É possível restaurar o comportamento anterior definindo a propriedade <xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod?displayProperty=name> como <xref:System.Data.SqlClient.PoolBlockingPeriod.AlwaysBlock>.|
|Escopo|Secundário|
|Versão|4.6.2|
|Tipo|Tempo de execução|
|APIs afetadas|<ul><li><xref:System.Data.Common.DbConnection.OpenAsync?displayProperty=nameWithType></li><li><xref:System.Data.SqlClient.SqlConnection.Open?displayProperty=nameWithType></li><li><xref:System.Data.SqlClient.SqlConnection.OpenAsync(System.Threading.CancellationToken)?displayProperty=nameWithType></li></ul>|

