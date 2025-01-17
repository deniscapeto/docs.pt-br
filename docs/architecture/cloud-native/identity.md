---
title: Identidade
description: Arquitetando aplicativos .NET nativos da nuvem para o Azure | Identidade
ms.date: 09/23/2019
ms.openlocfilehash: 4cc7c04bf323d2589777df466321f6801f511b6f
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71183045"
---
# <a name="identity"></a>Identidade

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

A maioria dos aplicativos de software precisa ter algum conhecimento do usuário ou do processo que o está chamando. O usuário ou processo que interage com um aplicativo é conhecido como uma entidade de segurança, e o processo de autenticação e autorização dessas entidades é conhecido como gerenciamento de identidade ou simplesmente *identidade*. Aplicativos simples podem incluir todo o gerenciamento de identidade dentro do aplicativo, mas essa abordagem não é bem dimensionada com muitos aplicativos e muitos tipos de entidades de segurança. O Windows dá suporte ao uso de Active Directory para fornecer autenticação e autorização centralizadas.

<!-- (insert figure showing Windows AD auth model) -->

Embora essa solução esteja em vigor em redes corporativas, ela não é projetada para uso por usuários ou aplicativos que estão fora do domínio do AD. Com o crescimento de aplicativos baseados na Internet e o aumento dos aplicativos nativos de nuvem, os modelos de segurança evoluíram.

No modelo de identidade nativa em nuvem de hoje, a arquitetura é considerada distribuída. Os aplicativos podem ser implantados em qualquer lugar e podem se comunicar com outros aplicativos em qualquer lugar. Os clientes podem se comunicar com esses aplicativos de qualquer lugar e, na verdade, os clientes podem consistir em qualquer combinação de plataformas e dispositivos. As soluções de identidade nativas de nuvem aproveitam os padrões abertos para obter acesso de aplicativo seguro de clientes. Esses clientes variam de usuários humanos em computadores ou telefones, a outros aplicativos hospedados em qualquer lugar online, para definir caixas superiores e dispositivos IOT que executam qualquer plataforma de software em qualquer lugar do mundo.

As soluções de identidade nativas de nuvem modernas normalmente aproveitam os tokens de acesso emitidos por um serviço/servidor de token seguro (STS) para uma entidade de segurança depois que sua identidade é determinada. O token de acesso, normalmente um token Web JSON (JWT), inclui *declarações* sobre a entidade de segurança. Essas declarações incluem minimamente a identidade do usuário, mas também podem incluir declarações adicionais que podem ser usadas por aplicativos para determinar o nível de acesso para conceder a entidade de segurança.

<!-- (insert figure showing basic handshake involving a principal, an STS, and an app) -->

Normalmente, o STS só é responsável por autenticar a entidade de segurança. A determinação de seu nível de acesso aos recursos é deixada para outras partes do aplicativo.

## <a name="references"></a>Referências

- [Plataforma de identidade da Microsoft](https://docs.microsoft.com/azure/active-directory/develop/)

>[!div class="step-by-step"]
>[Anterior](azure-monitor.md)
>[Próximo](authentication-authorization.md)
