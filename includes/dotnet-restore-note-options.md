---
ms.openlocfilehash: 497ac09e5c9a10470d3ae1932d7e3dc114d121dd
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65632005"
---
> [!NOTE]
> A partir do .NET Core 2.0, não é necessário executar [`dotnet restore`](~/docs/core/tools/dotnet-restore.md), pois ele é executado de forma implícita por todos os comandos, como `dotnet build` e `dotnet run`, que exigem a ocorrência de uma restauração. Ainda é um comando válido em determinados cenários em que realizar uma restauração explícita faz sentido, como [builds de integração contínua no Azure DevOps Services](/azure/devops/build-release/apps/aspnet/build-aspnet-core) ou em sistemas de build que precisam controlar explicitamente o horário em que a restauração ocorrerá.
>
> Este comando também é compatível com as opções `dotnet restore` quando passado no formato longo (por exemplo, `--source`). Opções de formato curto, como `-s`, não são compatíveis.
