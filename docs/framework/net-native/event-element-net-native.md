---
title: <Event> (.NET Nativo)
ms.date: 03/30/2017
ms.assetid: e53b029c-9d6d-4c0a-9cdc-5cfca8a5ca47
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7fb0245c50677da0397ba9c4918f171dcb217ba6
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049841"
---
# <a name="event-element-net-native"></a>\<Elemento de > de evento (.NET Native)
Aplica a política de reflexão de tempo de execução a um evento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<Event Name="event_name"   
       Browse="policy_type"   
       Dynamic="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Tipo de atributo|Descrição|  
|---------------|--------------------|-----------------|  
|`Name`|Geral|Atributo obrigatório. Especifica o nome do evento.|  
|`Browse`|Reflexão|Atributo opcional. Controla consultas para obter informações sobre o evento ou para enumerá-lo, mas não permite qualquer acesso dinâmico no tempo de execução.|  
|`Dynamic`|Reflexão|Atributo opcional. Controla o acesso do tempo de execução ao evento para habilitar programação dinâmica. Essa política garante que um evento pode ser tratado dinamicamente no tempo de execução.|  
  
## <a name="name-attribute"></a>Atributo de nome  
  
|Valor|Descrição|  
|-----------|-----------------|  
|*method_name*|O nome do evento. O tipo do evento é definido pelo elemento pai [\<Type>](type-element-net-native.md) ou [\<TypeInstantiation>](typeinstantiation-element-net-native.md).|  
  
## <a name="all-other-attributes"></a>Todos os outros atributos  
  
|Valor|Descrição|  
|-----------|-----------------|  
|*policy_setting*|A configuração a ser aplicada a este tipo de política para o evento. Os valores possíveis são `Auto`, `Excluded`, `Included` e `Required`. Para obter mais informações, consulte [Configurações da política da diretiva de tempo de execução](runtime-directive-policy-settings.md).|  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<Type>](type-element-net-native.md)|Aplica a política de reflexão a um tipo e todos os seus membros.|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|Aplica a política de reflexão a um tipo genérico construído e todos os seus membros.|  
  
## <a name="remarks"></a>Comentários  
 Se uma política do evento não for definida explicitamente, ele herdará a política de tempo de execução do seu elemento pai.  
  
## <a name="see-also"></a>Consulte também

- [Referência do arquivo de configuração das diretivas de tempo de execução (rd.xml)](runtime-directives-rd-xml-configuration-file-reference.md)
- [Elementos da diretiva de tempo de execução](runtime-directive-elements.md)
- [Configurações da política da diretiva de tempo de execução](runtime-directive-policy-settings.md)
