---
title: 'Como: Determinar quais atualizações de segurança e hotfixes do .NET Framework estão instalados'
description: Saiba como determinar quais atualizações de segurança e hotfixes do .NET Framework estão instaladas em um computador.
ms.date: 11/27/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- updates, determining for .NET Framework
- .NET Framework, determining updates
ms.assetid: 53c7b5f7-d47a-402a-b194-7244a696a88b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c4c505c679c46494f7dc2534c2bbe9f50243a7dd
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790070"
---
# <a name="how-to-determine-which-net-framework-security-updates-and-hotfixes-are-installed"></a>Como: Determinar quais atualizações de segurança e hotfixes do .NET Framework estão instalados

Este artigo mostra como descobrir quais atualizações de segurança e hotfixes do .NET Framework estão instaladas em um computador.

> [!NOTE]
> Todas as técnicas mostradas neste artigo exigem uma conta com privilégios administrativos.

## <a name="to-find-installed-updates-using-the-registry"></a>Para encontrar as atualizações instaladas usando o registro

As atualizações de segurança e os hotfixes instalados para cada versão do .NET Framework instalado em um computador estão listadas no Registro do Windows. Você pode usar o programa Editor do Registro (*regedit.exe*) para exibir essas informações.

1. Abra o programa **regedit.exe**. No Windows 8 e nas versões posteriores, clique com o botão direito do mouse em **Iniciar** ![Logotipo do Windows](../get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo") e, em seguida, selecione **Executar**. Na caixa **Abrir**, digite **regedit.exe** e selecione **OK**.

2. No Editor do Registro, abrir a seguinte subchave:

     `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Updates`

     As atualizações instaladas estão listadas nas subchaves que identificam a versão do .NET Framework a que se aplicam. Cada atualização é identificada por um número da Base de Dados de Conhecimento (KB).

No Editor do Registro, as versões do .NET Framework e as atualizações instaladas para cada versão são armazenadas em subchaves diferentes. Para obter informações sobre como detectar os números de versão instalados, confira [Como: Determinar quais versões do .NET Framework estão instaladas](how-to-determine-which-versions-are-installed.md).

## <a name="to-find-installed-updates-by-querying-the-registry-in-code"></a>Para encontrar as atualizações instaladas ao consultar o registro no código

O exemplo a seguir determina programaticamente as atualizações de segurança e os hotfixes do .NET Framework que estão instalados em um computador:

[!code-csharp[ListUpdates](../../../samples/snippets/csharp/VS_Snippets_CLR/listupdates/cs/program.cs)]
[!code-vb[ListUpdates](../../../samples/snippets/visualbasic/VS_Snippets_CLR/listupdates/vb/program.vb)]

O exemplo produz uma saída semelhante à seguinte:

```console
Microsoft .NET Framework 4 Client Profile
  KB2468871
  KB2468871v2
  KB2478063
  KB2533523
  KB2544514
  KB2600211
  KB2600217
Microsoft .NET Framework 4 Extended
  KB2468871
  KB2468871v2
  KB2478063
  KB2533523
  KB2544514
  KB2600211
  KB2600217
```

## <a name="to-find-installed-updates-by-querying-the-registry-in-powershell"></a>Para encontrar as atualizações instaladas ao consultar o registro no PowerShell

O exemplo a seguir mostra como determinar as atualizações de segurança e os hotfixes do .NET Framework que estão instalados em um computador usando o PowerShell:

```powershell
$DotNetVersions = Get-ChildItem HKLM:\SOFTWARE\WOW6432Node\Microsoft\Updates | Where-Object {$_.name -like
 "*.NET Framework*"}

ForEach($Version in $DotNetVersions){
    
   $Updates = Get-ChildItem $Version.PSPath
    $Version.PSChildName
    ForEach ($Update in $Updates){
       $Update.PSChildName
       }
}
```

O exemplo produz uma saída semelhante à seguinte:

```console
Microsoft .NET Framework 4 Client Profile
KB2468871
KB2468871v2
KB2478063
KB2533523
KB2544514
KB2600211
KB2600217
Microsoft .NET Framework 4 Extended
KB2468871
KB2468871v2
KB2478063
KB2533523
KB2544514
KB2600211
KB2600217
```

## <a name="see-also"></a>Consulte também

- [Como: Determinar quais versões do .NET Framework estão instaladas](how-to-determine-which-versions-are-installed.md)
- [Instalar o .NET Framework para desenvolvedores](../install/guide-for-developers.md)
- [Versões e dependências](versions-and-dependencies.md)
