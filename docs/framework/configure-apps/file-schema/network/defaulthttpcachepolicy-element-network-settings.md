---
title: Elemento <defaultHttpCachePolicy> (Configurações de Rede)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/requestCaching/defaultHttpCachePolicy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#defaultHttpCachePolicy
helpviewer_keywords:
- defaultHttpCachePolicy element
- <defaultHttpCachePolicy> element
ms.assetid: 2c1247d0-39b0-4c12-919a-a925ce075c79
ms.openlocfilehash: f3b029e8b931e976bee85c98dd926e020c5b8743
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698273"
---
# <a name="defaulthttpcachepolicy-element-network-settings"></a>\<defaultHttpCachePolicy > elemento (configurações de rede)
Descreve se o cache HTTP está ativo e descreve a política de cache padrão.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t -4System. net >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3[ **\<requestCaching >** ](requestcaching-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3 @ no__t-4 @ no__t-5 **\<defaultHttpCachePolicy >**  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<defaultHttpCachePolicy  
  policyLevel="BypassCache|Default"  
  minimumFresh="d.hh:mm:ss|minValue|maxValue"  
  maximumAge="d.hh:mm:ss|minValue|maxValue"  
  maximumStale="d.hh:mm:ss|minValue|maxValue"  
/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`maximumAge`|Especifica o intervalo de tempo máximo antes que um objeto armazenado em cache seja marcado como expirado.|  
|`maximumStale`|Especifica o tempo máximo após o tempo de atualização computado antes que um objeto armazenado em cache seja marcado como expirado.|  
|`minimumFresh`|Especifica o tempo mínimo para um objeto em cache ser considerado atualizado.|  
|`policyLevel`|Especifica se a política de cache é automática ou se o cache é ignorado. O valor padrão é `BypassCache`.|  
  
### <a name="child-elements"></a>Elementos filho  
 Nenhum  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[requestCaching](requestcaching-element-network-settings.md)|Controla o mecanismo de cache para solicitações de rede.|  
  
## <a name="remarks"></a>Comentários  
 O valor do atributo `policyLevel` é `BypassCache` ou `Default`.  
  
 Os valores para os elementos `maximumAge`, `maximumStale` e `minimumFresh` são um intervalo de tempo explícito com um formato de *d*. *hh*:*mm*:*SS* (dias, horas, minutos e segundos) ou as constantes `minValue` ou `maxValue`, conforme apropriado.  
  
## <a name="configuration-files"></a>Arquivos de Configuração  
 Esse elemento pode ser usado no arquivo de configuração do aplicativo ou no arquivo de configuração do computador (Machine. config).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como especificar uma hora de atualização mínima de seis horas, um tempo de vida máximo de dois dias e um tempo máximo de obsoleto de quatro horas.  
  
```xml  
<configuration>  
  <system.net>  
    <requestCaching>  
      <defaultHttpCachePolicy  
        minimumFresh="0.06:00:00"  
        maximumAge="2.00:00:00"  
        maximumStale="0.04:00:00"
      />  
    </requestCaching>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Net.Cache>
- <xref:System.Net.WebRequest>
- <xref:System.Net.Cache.RequestCacheLevel>
- [Esquema de configurações de rede](index.md)
