---
title: Personalizando quais objetos estão disponíveis em My (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- My namespace [Visual Basic], customizing
- My namespace
ms.assetid: 4e8279c2-ed5b-4681-8903-8a6671874000
ms.openlocfilehash: caddad463f7c525c8b715d70f49bf8bebcc7cfbd
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701260"
---
# <a name="customizing-which-objects-are-available-in-my-visual-basic"></a>Personalizando quais objetos estão disponíveis em My (Visual Basic)

Este tópico descreve como você pode controlar quais objetos `My` são habilitados definindo a constante de compilação condicional `_MYTYPE` do projeto. O IDE (ambiente de desenvolvimento integrado) do Visual Studio mantém a constante de compilação condicional `_MYTYPE` para um projeto em sincronia com o tipo do projeto.  
  
## <a name="predefined-_mytype-values"></a>Valores predefinidos de \_MYTYPE  

Você deve usar a opção de compilador `/define` para definir a constante de compilação condicional `_MYTYPE`. Ao especificar seu próprio valor para a constante `_MYTYPE`, você deve colocar o valor da cadeia de caracteres nas sequências de barra invertida/aspas (\\ "). Por exemplo, você pode usar:  
  
```console  
/define:_MYTYPE=\"WindowsForms\"  
```  
  
 Esta tabela mostra o que a constante de compilação condicional `_MYTYPE` está definida para vários tipos de projeto.  
  
|Tipo de projeto|valor de \_MYTYPE|  
|------------------|--------------------|  
|Biblioteca de Classes|Windows|  
|Aplicativo do Console|MMC|  
|Web|Site|  
|Biblioteca de controle da Web|WebControl|  
|Aplicativo do Windows|WindowsForms|  
|Aplicativo do Windows, ao iniciar com @no__t personalizado-0|"WindowsFormsWithCustomSubMain"|  
|Biblioteca de controle do Windows|Windows|  
|Serviço do Windows|MMC|  
|Vazio|Esvaziá|  
  
> [!NOTE]
> Todas as comparações de cadeia de caracteres de compilação condicional diferenciam maiúsculas de minúsculas, independentemente de como a instrução `Option Compare` é definida.  
  
## <a name="dependent-_my-compilation-constants"></a>Constantes de compilação \_MY dependentes  

A constante de compilação condicional `_MYTYPE`, por sua vez, controla os valores de várias outras constantes de compilação `_MY`:  
  
|\_MYTYPE|\_MYAPPLICATIONTYPE|\_MYCOMPUTERTYPE|\_MYFORMS|\_MYUSERTYPE|\_MYWEBSERVICES|  
|--------------|-------------------------|----------------------|---------------|------------------|---------------------|  
|MMC|MMC|Windows|Indefinido|Windows|TRUE|  
|Personalizar|Indefinido|Indefinido|Indefinido|Indefinido|Indefinido|  
|Esvaziá|Indefinido|Indefinido|Indefinido|Indefinido|Indefinido|  
|Site|Indefinido|Site|FALSE|Site|FALSE|  
|WebControl|Indefinido|Site|FALSE|Site|TRUE|  
|"Windows" ou ""|Windows|Windows|Indefinido|Windows|TRUE|  
|WindowsForms|WindowsForms|Windows|TRUE|Windows|TRUE|  
|"WindowsFormsWithCustomSubMain"|MMC|Windows|TRUE|Windows|TRUE|  
  
 Por padrão, as constantes de compilação condicional indefinidas são resolvidas como `FALSE`. Você pode especificar valores para as constantes indefinidas ao compilar seu projeto para substituir o comportamento padrão.  
  
> [!NOTE]
> Quando `_MYTYPE` é definido como "Custom", o projeto contém o namespace `My`, mas não contém objetos. No entanto, definir `_MYTYPE` como "Empty" impede que o compilador adicione o namespace `My` e seus objetos.  
  
 Esta tabela descreve os efeitos dos valores predefinidos das constantes de compilação `_MY`.  
  
|Constante|Significado|  
|--------------|-------------|  
|`_MYAPPLICATIONTYPE`|Habilita `My.Application`, se a constante for "console", Windows, "ou" WindowsForms ":<br /><br /> -A versão do "console" deriva de <xref:Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase>. e tem menos membros do que a versão "Windows".<br />-A versão "Windows" deriva de <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>. e tem menos membros do que a versão "WindowsForms".<br />-A versão "WindowsForms" de `My.Application` deriva de <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>. Se a constante `TARGET` for definida como "winexe", a classe incluirá um método `Sub Main`.|  
|`_MYCOMPUTERTYPE`|Habilita `My.Computer`, se a constante for "Web" ou "Windows":<br /><br /> -A versão "Web" deriva de <xref:Microsoft.VisualBasic.Devices.ServerComputer> e tem menos membros do que a versão "Windows".<br />-A versão "Windows" do `My.Computer` deriva de <xref:Microsoft.VisualBasic.Devices.Computer>.|  
|`_MYFORMS`|Habilita `My.Forms`, se a constante for `TRUE`.|  
|`_MYUSERTYPE`|Habilita `My.User`, se a constante for "Web" ou "Windows":<br /><br /> -A versão "Web" do `My.User` está associada à identidade do usuário da solicitação HTTP atual.<br />-A versão "Windows" do `My.User` está associada à entidade de segurança atual do thread.|  
|`_MYWEBSERVICES`|Habilita `My.WebServices`, se a constante for `TRUE`.|  
|`_MYTYPE`|Habilita `My.Log`, `My.Request` e `My.Response`, se a constante for "Web".|  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>
- <xref:Microsoft.VisualBasic.Devices.Computer>
- <xref:Microsoft.VisualBasic.Logging.Log>
- <xref:Microsoft.VisualBasic.ApplicationServices.User>
- [Como My depende do tipo de projeto](../../../visual-basic/developing-apps/development-with-my/how-my-depends-on-project-type.md)
- [Compilação Condicional](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
- [/define (Visual Basic)](../../../visual-basic/reference/command-line-compiler/define.md)
- [Objeto My.Forms](../../../visual-basic/language-reference/objects/my-forms-object.md)
- [Objeto My.Request](../../../visual-basic/language-reference/objects/my-request-object.md)
- [Objeto My.Response](../../../visual-basic/language-reference/objects/my-response-object.md)
- [Objeto My.WebServices](../../../visual-basic/language-reference/objects/my-webservices-object.md)
