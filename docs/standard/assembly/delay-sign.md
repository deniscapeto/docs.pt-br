---
title: Assinar um assembly com atraso
ms.date: 08/19/2019
helpviewer_keywords:
- deferring assembly signing
- signing assemblies
- assemblies [.NET Framework], signing
- strong-named assemblies, delaying assembly signing
- partial assembly signing
ms.assetid: 9d300e17-5bf1-4360-97da-2aa55efd9070
author: rpetrusha
ms.author: ronpet
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: e7679520e246ab3eda03e6f0e0d092c7d09f1845
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991329"
---
# <a name="delay-sign-an-assembly"></a>Assinar um assembly com atraso

Uma organização pode ter um par de chaves bem protegido que os desenvolvedores não podem acessar diariamente. A chave pública normalmente está disponível, mas o acesso à chave privada é restrito a apenas algumas pessoas. Ao desenvolver assemblies com nomes fortes, cada assembly que referencia o assembly de destino com nome forte contém o token da chave pública usada para fornecer ao assembly de destino um nome forte. Isso requer que a chave pública esteja disponível durante o processo de desenvolvimento.

Você pode usar a assinatura atrasada ou parcial no momento da compilação para reservar espaço no arquivo executável portátil (PE) para a assinatura de nome forte, mas adiar a assinatura real até algum estágio posterior, geralmente antes de enviar o assembly.

Para assinar um assembly com atraso:

1. Obtenha a parte da chave pública do par de chaves da organização que fará a assinatura eventual. Normalmente, essa chave está na forma de um arquivo *. SNK* , que pode ser criado usando a [ferramenta de nome forte (SN. exe)](../../framework/tools/sn-exe-strong-name-tool.md) fornecida pelo SDK do Windows.

2. Anote o código-fonte para o assembly com dois atributos personalizados de <xref:System.Reflection>:

   - <xref:System.Reflection.AssemblyKeyFileAttribute>, que passa o nome do arquivo que contém a chave pública como um parâmetro para seu construtor.

   - <xref:System.Reflection.AssemblyDelaySignAttribute>, que indica que esse atraso na assinatura está sendo usado passando **true** como um parâmetro para seu construtor.

   Por exemplo:

   ```cpp
   [assembly:AssemblyKeyFileAttribute("myKey.snk")];
   [assembly:AssemblyDelaySignAttribute(true)];
   ```

   ```csharp
   [assembly:AssemblyKeyFileAttribute("myKey.snk")]
   [assembly:AssemblyDelaySignAttribute(true)]
   ```

   ```vb
   <Assembly:AssemblyKeyFileAttribute("myKey.snk")>
   <Assembly:AssemblyDelaySignAttribute(True)>
   ```

3. O compilador insere a chave pública no manifesto do assembly e reserva espaço no arquivo PE para a assinatura de nome forte completo. A chave pública real deve ser armazenada enquanto o assembly é compilado para que outros assemblies que referenciam esse assembly possam obter a chave para armazenar em sua própria referência do assembly.

4. Como o assembly não tem uma assinatura de nome forte válida, a verificação dessa assinatura deve ser desativada. Você pode fazer isso usando a opção **– Vr** com a ferramenta Nome Forte.

     O exemplo a seguir desativa a verificação para um assembly chamado *myAssembly. dll*.

   ```console
   sn –Vr myAssembly.dll
   ```

   Para desligar a verificação em plataformas em que você não pode executar a ferramenta Nome Forte, como microprocessadores ARM (Advanced RISC Machine), use a opção **–Vk** para criar um arquivo de Registro. Importe o arquivo de Registro para o Registro no computador em que você deseja desligar a verificação. O exemplo a seguir cria um arquivo de Registro para `myAssembly.dll`.

   ```console
   sn –Vk myRegFile.reg myAssembly.dll
   ```

   Com a opção **– VR** ou **– VK** , você pode, opcionalmente, incluir um arquivo *. SNK* para assinatura de chave de teste.

   > [!WARNING]
   > Por segurança, não confie em nomes fortes. Eles apenas fornecem uma identidade exclusiva.

   > [!NOTE]
   > Se você usar o atraso de assinatura durante o desenvolvimento com o Visual Studio em um computador de 64 bits e compilar um assembly para **Qualquer CPU**, talvez seja necessário aplicar a opção **-Vr** duas vezes. (No Visual Studio, **Qualquer CPU** é um valor da propriedade de build **Destino de Plataforma**, quando você compila da linha de comando, esse é o padrão.) Para executar o aplicativo na linha de comando ou no explorador de arquivos, use a versão de 64 bits do [sn. exe (Strong Name Tool)](../../framework/tools/sn-exe-strong-name-tool.md) para aplicar a opção **-VR** ao assembly. Para carregar o assembly no Visual Studio no tempo de design (por exemplo, se o assembly contiver componentes que são usados por outros assemblies em seu aplicativo), use a versão de 32 bits da ferramenta de nome forte. Isso ocorre porque o compilador JIT (Just-in-time) compila o assembly para código nativo de 64 bits quando o assembly é executado da linha de comando e para código nativo de 32 bits quando o assembly é carregado no ambiente de tempo de design.

5. Posteriormente, normalmente imediatamente antes do envio, você envia o assembly para a autoridade de assinatura da sua organização para a assinatura de nome forte real usando a opção **–R** com a ferramenta Nome Forte.

   O exemplo a seguir assina um assembly chamado *myAssembly. dll* com um nome forte usando o par de chaves *sgKey. SNK* .

   ```console
   sn -R myAssembly.dll sgKey.snk
   ```

## <a name="see-also"></a>Consulte também

- [Criar assemblies](create.md)
- [Como: Criar um par de chaves pública/privada](create-public-private-key-pair.md)
- [Sn. exe (ferramenta Strong Name)](../../framework/tools/sn-exe-strong-name-tool.md)
- [Programa com assemblies](program.md)
