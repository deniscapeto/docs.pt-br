---
title: 'Guia de migração para o .NET Framework 4.8, 4.7, 4.6 e 4.5 '
ms.custom: updateeachrelease
ms.date: 04/18/2019
helpviewer_keywords:
- .NET Framework, migrating applications to
- migration, .NET Framework
ms.assetid: 02d55147-9b3a-4557-a45f-fa936fadae3b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9b1cda82125a2d4a6eb3102b01bea639a4f3e3df
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65636082"
---
# <a name="migration-guide-to-the-net-framework-48-47-46-and-45"></a>Guia de migração para o .NET Framework 4.8, 4.7, 4.6 e 4.5

Se seu aplicativo foi criado usando uma versão anterior do .NET Framework, normalmente, é possível atualizá-lo com facilidade para o .NET Framework 4.5 e suas versões de correção (4.5.1 e 4.5.2), para o .NET Framework 4.6 e suas versões de correção (4.6.1 e 4.6.2), para o .NET Framework 4.7 e suas versões de correção (4.7.1 e 4.7.2) ou para o .NET Framework 4.8. Abra seu projeto no Visual Studio. Se o seu projeto tiver sido criado em uma versão anterior do Visual Studio, a caixa de diálogo **Compatibilidade do Projeto** abrirá automaticamente. Para saber mais sobre como atualizar um projeto no Visual Studio, consulte [Portar, migrar e atualizar projetos do Visual Studio](/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects) e [Direcionamento e compatibilidade da plataforma Visual Studio 2019](/visualstudio/releases/2019/compatibility).

 No entanto, algumas alterações feitas no .NET Framework exigem mudanças no seu código. Convém também aproveitar a nova funcionalidade no .NET Framework 4.5 e suas versões de correção, no .NET Framework 4.6 e suas versões de correção, no .NET Framework 4.7 e suas versões de correção ou no .NET Framework 4.8. Fazer esses tipos de mudanças para seu aplicativo de uma nova versão do .NET Framework costuma ser conhecido como *migração*. Se o aplicativo não precisar ser migrado, será possível executar o .NET Framework 4.5 ou versões posteriores sem recompilá-lo.

## <a name="migration-resources"></a>Recursos de migração

Examine os seguintes documentos antes de migrar seu aplicativo de versões anteriores do .NET Framework para as versões 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2 ou 4.8:

- Confira [Versões e dependências](versions-and-dependencies.md) para compreender a versão do CLR subjacente a cada versão do .NET Framework e examinar diretrizes para segmentação de seus aplicativos com êxito.

- Confira [Compatibilidade de aplicativos](application-compatibility.md) para saber mais sobre as alterações feitas no tempo de execução e no redirecionamento que podem afetar seu aplicativo e como lidar com eles.

- Confira [O que está obsoleto na Biblioteca de Classes](../whats-new/whats-obsolete.md) para determinar todos os tipos ou membros no seu código que ficaram obsoletos e as alternativas recomendadas.

- Confira [Novidades](../whats-new/index.md) para obter descrições dos novos recursos que você talvez queira adicionar ao seu aplicativo.

## <a name="see-also"></a>Consulte também

- [Compatibilidade de aplicativos](application-compatibility.md)
- [Migrando do .NET Framework 1.1](migrating-from-the-net-framework-1-1.md)
- [Compatibilidade de versão](version-compatibility.md)
- [Versões e dependências](versions-and-dependencies.md)
- [Como: configurar um aplicativo para oferecer suporte ao .NET Framework 4 ou versões posteriores](how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)
- [Novidades](../whats-new/index.md)
- [O que está obsoleto na Biblioteca de Classes](../whats-new/whats-obsolete.md)
- [Versão do .NET Framework e informações de Assembly](https://go.microsoft.com/fwlink/?LinkId=201701)
- [Política de ciclo de vida de suporte do Microsoft .NET Framework](https://go.microsoft.com/fwlink/?LinkId=196607)
- [Problemas de migração do .NET Framework 4](net-framework-4-migration-issues.md)
