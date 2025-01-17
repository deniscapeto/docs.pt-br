---
title: Criar um novo projeto ASP.NET Core gRPC-gRPC para desenvolvedores do WCF
description: Saiba como criar um projeto do gRPC usando o Visual Studio ou a linha de comando.
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: a0fcc3f9c4e32e87260a6bc79205c909ea3800e0
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184564"
---
# <a name="create-a-new-aspnet-core-grpc-project"></a>Criar um novo projeto ASP.NET Core gRPC

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

O .NET Core vem com uma poderosa ferramenta CLI `dotnet`,, que permite criar e gerenciar projetos e soluções na linha de comando. A ferramenta está intimamente integrada ao Visual Studio, de modo que tudo também está disponível por meio da interface GUI familiar. Este capítulo mostrará as duas maneiras de criar um novo projeto ASP.NET Core gRPC: primeiro com o Visual Studio e, em seguida, com o CLI do .NET Core.

## <a name="create-the-project-using-visual-studio"></a>Criar o projeto usando o Visual Studio

> [!IMPORTANT]
> Para desenvolver qualquer aplicativo ASP.NET Core 3,0, você precisa do Visual Studio 2019,3 ou posterior com a ASP.NET e a carga de trabalho de **desenvolvimento Web** instaladas.

Crie uma solução vazia chamada **Traders** a partir do modelo de *solução em branco* . Adicione uma pasta de solução `src`chamada, clique com o botão direito do mouse na pasta e escolha **Adicionar** > **novo projeto** no menu de contexto. Digite `grpc` na caixa de pesquisa de modelo e você deverá ver um modelo de `gRPC Service`projeto chamado.

![Caixa de diálogo Adicionar novo projeto mostrando o modelo de projeto do serviço gRPC](media/create-project/new-grpc-project.png)

Clique em **Avançar** para continuar na caixa de diálogo **Configurar projeto** e nomeie `TraderSys.Portfolios`o projeto e adicione `src` um subdiretório ao **local**.

![Caixa de diálogo Configurar projeto](media/create-project/configure-project.png)

Clique em **Avançar** para ir para a caixa de diálogo **novo projeto gRPC** .

![Caixa de diálogo novo projeto gRPC](media/create-project/create-new-grpc-service.png)

No momento, há opções limitadas para a criação do serviço. O Docker será introduzido posteriormente no livro, portanto, deixe essa caixa de seleção desmarcada por enquanto e clique em **criar**. Seu primeiro projeto ASP.NET Core gRPC 3,0 é gerado e adicionado à solução. Se você não quiser saber sobre como trabalhar com o `dotnet CLI`, pule para a seção [limpar o exemplo de código](#clean-up-the-example-code) .

## <a name="create-the-project-using-the-net-core-cli"></a>Criar o projeto usando o CLI do .NET Core

Esta seção aborda a criação de soluções e projetos da linha de comando.

Crie a solução, conforme mostrado abaixo. O `-o` sinalizador ( `--output`ou) especifica o diretório de saída, que será criado no diretório atual se ele não existir. A solução receberá o mesmo nome que o diretório, ou seja `TraderSys.sln`,. Você pode fornecer um nome diferente usando o `-n` sinalizador ( `--name`ou).

```dotnetcli
dotnet new sln -o TraderSys
cd TraderSys
```

ASP.NET Core 3,0 vem com um modelo de CLI para serviços gRPCs. Crie o novo projeto usando este modelo, colocando-o em `src` um subdiretório como é a Convenção para projetos de ASP.NET Core. O projeto será nomeado após o diretório (ou seja `TraderSys.Portfolios.csproj`,), a menos que você especifique um nome diferente com o `-n` sinalizador.

```dotnetcli
dotnet new grpc -o src/TraderSys.Portfolios
```

Por fim, adicione o projeto à solução usando o `dotnet sln` comando.

```dotnetcli
dotnet sln add src/TraderSys.Portfolios
```

> [!TIP]
> Como o diretório fornecido contém apenas um único `.csproj` arquivo, você pode deixar de especificar apenas o diretório para salvar a digitação.

Agora você pode abrir essa solução no Visual Studio 2019, Visual Studio Code ou em qualquer editor que preferir.

## <a name="clean-up-the-example-code"></a>Limpar o código de exemplo

Agora você criou um serviço de exemplo usando o modelo gRPC, que foi revisado anteriormente no livro. Isso não é útil em nosso contexto de comércio de ações, portanto, vamos editar as coisas para nosso primeiro projeto.

### <a name="rename-and-edit-the-proto-file"></a>Renomear e editar o arquivo proto

Vá em frente e renomeie `Protos/portfolios.proto` o arquivo para e abra-o `Protos/greet.proto` em seu editor. Exclua tudo após `package` a linha e, em `option csharp_namespace`seguida, `service` altere os nomes, `package` e remova `SayHello` o serviço padrão, para que o código tenha esta aparência.

```protobuf
syntax = "proto3";

option csharp_namespace = "TraderSys.Portfolios.Protos";

package PortfolioServer;

service Portfolios {
  // RPCs will go here
}
```

> [!TIP]
> O modelo não adiciona a `Protos` parte de namespace por padrão, mas adicioná-la torna mais fácil manter classes gRPC e suas próprias classes claramente separadas em seu código.

Se você renomear o arquivo em um ambiente de desenvolvimento integrado (IDE) como o `greet.proto` Visual Studio, uma referência a esse arquivo será atualizada automaticamente `.csproj` no arquivo. Mas, em algum outro editor, como Visual Studio Code, essa referência não é atualizada automaticamente, portanto, você precisa editar o arquivo de projeto manualmente.

Nos destinos de compilação gRPC, há um `Protobuf` elemento item que permite especificar quais `.proto` arquivos devem ser compilados e qual forma de geração de código é necessária (ou seja, "Server" ou "Client").

```xml
<ItemGroup>
  <Protobuf Include="Protos\portfolios.proto" GrpcServices="Server" />
</ItemGroup>
```

### <a name="rename-the-greeterservice-class"></a>Renomeie a classe GreeterService

A `GreeterService` classe está `Services` na pasta e herda de `Greeter.GreeterBase`. Renomeie `PortfolioService` -o como e altere a `Portfolios.PortfoliosBase`classe base para. Exclua `override` os métodos.

```csharp
public class PortfolioService : Portfolios.PortfoliosBase
{
}
```

Houve uma referência à `GreeterService` classe `Configure` no método na `Startup` classe. Se você usou a refatoração para renomear a classe, essa referência deverá ter sido atualizada automaticamente. No entanto, se você não tiver, precisará editá-lo manualmente.

```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    app.UseRouting();

    app.UseEndpoints(endpoints =>
    {
        endpoints.MapGrpcService<PortfolioService>();
    });
}
```

Na próxima seção, adicionaremos funcionalidade a esse novo serviço.

>[!div class="step-by-step"]
>[Anterior](migrate-wcf-to-grpc.md)
>[Próximo](migrate-request-reply.md)
