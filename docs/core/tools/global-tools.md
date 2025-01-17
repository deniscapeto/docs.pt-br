---
title: Ferramentas Globais do .NET Core
description: Uma visão geral do que são as Ferramentas Globais do .NET Core e os comandos da CLI do .NET Core disponíveis para elas.
author: KathleenDollard
ms.date: 05/29/2018
ms.custom: seodec18
ms.openlocfilehash: 40a0aabcf523e8dac9a3ad226064bbb3c1b3ce5b
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71332014"
---
# <a name="net-core-global-tools-overview"></a>Visão geral das Ferramentas Globais do .NET Core

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

Uma Ferramenta Global do .NET Core é um pacote NuGet especial que contém um aplicativo de console. Uma Ferramenta Global pode ser instalada no computador em uma localização padrão que está incluída na variável de ambiente PATH ou em um local personalizado.

Caso deseje usar uma Ferramenta Global do .NET Core:

* Encontre informações sobre a ferramenta (geralmente um site ou uma página do GitHub).
* Verifique o autor e as estatísticas na página inicial do feed (geralmente, NuGet.org).
* Instale a ferramenta.
* Chame a ferramenta.
* Atualize a ferramenta.
* Desinstale a ferramenta.

> [!IMPORTANT]
> As Ferramentas Globais do .NET Core são exibidas no caminho e executadas com confiança total. Não instale as Ferramentas Globais do .NET Core, a menos que você confie no autor.

## <a name="find-a-net-core-global-tool"></a>Encontrar uma Ferramenta Global do .NET Core

Atualmente, há não uma funcionalidade de pesquisa de Ferramenta Global na CLI (interface de linha de comando) do .NET Core.

Encontre Ferramentas Globais do .NET Core no [NuGet](https://www.nuget.org). No entanto, o NuGet ainda não permite a pesquisa especificamente de Ferramentas Globais do .NET Core.

Você também pode encontrar recomendações de ferramentas em postagens no blog ou no repositório [natemcmaster/dotnet-tools](https://github.com/natemcmaster/dotnet-tools) do GitHub.

Veja também o código-fonte das Ferramentas Globais criadas pela equipe do ASP.NET no repositório [aspnet/DotNetTools](https://github.com/aspnet/DotNetTools/) do GitHub.

## <a name="check-the-author-and-statistics"></a>Verificar o autor e as estatísticas

Como as Ferramentas Globais do .NET Core são executadas em confiança total e geralmente são instaladas no caminho, elas podem ser muito eficientes. Não baixe ferramentas de pessoas em quem você não confia.

Se a ferramenta estiver hospedada no NuGet, você pode verificar o autor e as estatísticas pesquisando a ferramenta.

## <a name="install-a-global-tool"></a>Instalar uma Ferramenta Global

Para instalar uma Ferramenta Global, use o comando [dotnet tool install](dotnet-tool-install.md) da CLI do .NET Core. O seguinte exemplo mostra como instalar uma Ferramenta Global na localização padrão:

```dotnetcli
dotnet tool install -g dotnetsay
```

Se a ferramenta não puder ser instalada, mensagens de erro serão exibidas. Verifique se os feeds esperados estão sendo verificados.

Se estiver tentando instalar uma versão de pré-lançamento ou uma versão específica da ferramenta, especifique o número de versão usando o seguinte formato:

```dotnetcli
dotnet tool install -g <package-name> --version <version-number>
```

Se a instalação for bem-sucedida, será exibida uma mensagem mostrando o comando usado para chamar a ferramenta e a versão instalada, de maneira semelhante ao seguinte exemplo:

```output
You can invoke the tool using the following command: dotnetsay
Tool 'dotnetsay' (version '2.0.0') was successfully installed.
```

As Ferramentas Globais podem ser instaladas no diretório padrão ou em um local específico. Os diretórios padrão são:

| OS          | Path                          |
|-------------|-------------------------------|
| Linux/macOS | `$HOME/.dotnet/tools`         |
| Windows     | `%USERPROFILE%\.dotnet\tools` |

Esses locais são adicionados ao caminho do usuário quando o SDK é executado pela primeira vez e, portanto, as Ferramentas Globais instaladas nesses locais podem ser chamadas diretamente.

Observe que as Ferramentas Globais são específicas ao usuário e não globais no computador. Ser específico ao usuário significa que não é possível instalar uma Ferramenta Global que esteja disponível para todos os usuários do computador. A ferramenta só fica disponível para cada perfil de usuário no qual a ferramenta foi instalada.

As Ferramentas Globais também podem ser instaladas em um diretório específico. Quando elas forem instaladas em um diretório específico, o usuário precisará garantir que o comando esteja disponível, incluindo o diretório no caminho, chamando o comando com o diretório especificado ou chamando a ferramenta no diretório especificado.
Nesse caso, a CLI do .NET Core não adiciona esse local automaticamente à variável de ambiente PATH.

## <a name="use-the-tool"></a>Usar a ferramenta

Depois de instalar a ferramenta, chame-a usando seu comando. Observe que o comando pode não ser o mesmo que o nome do pacote.

Se o comando for `dotnetsay`, chame a ferramenta com:

```console
dotnetsay
```

Se o autor da ferramenta desejou que a ferramenta fosse exibida no contexto do prompt do `dotnet`, ele pode ter escrito a ferramenta de modo que você a chame como `dotnet <command>`, por exemplo:

```dotnetcli
dotnet doc
```

Encontre quais ferramentas estão incluídas em um pacote de Ferramentais Global instalado por meio da listagem dos pacotes instalados usando o comando [dotnet tool list](dotnet-tool-list.md).

Procure também instruções de uso no site da ferramenta ou digitando um dos seguintes comandos:

```console
<command> --help
dotnet <command> --help
```

## <a name="other-cli-commands"></a>Outros comandos da CLI

O SDK do .NET Core contém outros comandos que dão suporte às Ferramentas Globais do .NET Core. Use um dos comandos `dotnet tool` com uma das seguintes opções:

* `--global` ou `-g` especifica que o comando é aplicável às Ferramentas Globais de todos os usuários.
* `--tool-path` especifica um local personalizado para as Ferramentas Globais.

Para descobrir quais comandos estão disponíveis para as Ferramentas Globais:

```dotnetcli
dotnet tool --help
```

A atualização de uma Ferramenta Global envolve sua desinstalação e reinstalação com a última versão estável. Para atualizar uma Ferramenta Global, use o comando [dotnet tool update](dotnet-tool-update.md):

```dotnetcli
dotnet tool update -g <packagename>
```

Remova uma Ferramenta Global usando [dotnet tool uninstall](dotnet-tool-uninstall.md):

```dotnetcli
dotnet tool uninstall -g <packagename>
```

Para exibir todas as Ferramentas Globais atualmente instaladas no computador, junto com as versões e os comandos, use o comando [dotnet tool list](dotnet-tool-list.md):

```dotnetcli
dotnet tool list -g
```

## <a name="see-also"></a>Consulte também

* [Solucionar problemas de uso da ferramenta .NET Core](troubleshoot-usage-issues.md)
