---
title: 'Como: Excluir uma chave do Registro no Visual Basic'
ms.date: 07/20/2015
f1_keywords:
- vb.DeleteSetting
helpviewer_keywords:
- GetSetting function [Visual Basic]
- registry [Visual Basic], deleting values
- GetAllSettings function
- registry keys [Visual Basic], deleting
- registry [Visual Basic], deleting keys
- examples [Visual Basic], registry
ms.assetid: ab9aca0e-42b0-4ff7-8ff9-845a4bfdf9f2
ms.openlocfilehash: 2e0c8990fcc55bc4208b1c23690ff748b7167002
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662766"
---
# <a name="how-to-delete-a-registry-key-in-visual-basic"></a>Como: Excluir uma chave do Registro no Visual Basic
Os métodos <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%28System.String%29> e <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%28System.String%2CSystem.Boolean%29> podem ser usados para excluir chaves do Registro.  
  
## <a name="procedure"></a>Procedimento  
  
#### <a name="to-delete-a-registry-key"></a>Excluir uma chave do Registro  
  
- Use o método `DeleteSubKey` para excluir uma chave do Registro. Este exemplo exclui a chave Software/TestApp no hive CurrentUser. É possível alterar isso no código para a cadeia de caracteres apropriada ou fazer com que se baseie nas informações fornecidas pelo usuário.  
  
     [!code-vb[VbResourceTasks#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#19)]  
  
## <a name="robust-programming"></a>Programação robusta  
 O método `DeleteSubKey` retornará uma cadeia de caracteres vazia se o par chave-valor não existir.  
  
 As seguintes condições podem causar uma exceção:  
  
- O nome da chave é `Nothing` (<xref:System.ArgumentNullException>).  
  
- O usuário não tem permissões para excluir chaves do Registro (<xref:System.Security.SecurityException>).  
  
- O nome da chave excede o limite de 255 caracteres (<xref:System.ArgumentException>).  
  
- A chave do Registro é somente leitura (<xref:System.UnauthorizedAccessException>).  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 As chamadas do Registro falharão se as permissões suficientes de tempo de execução não forem concedidas (<xref:System.Security.Permissions.RegistryPermission>) ou se o usuário não tiver o acesso correto para (conforme determinado pelas ACLs) para criar ou gravar nas configurações. Por exemplo, um aplicativo local que tem a permissão de segurança de acesso do código pode não ter permissão do sistema operacional.  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%2A>
- <xref:Microsoft.Win32.RegistryKey>
- [Segurança e Registro](../../../../visual-basic/developing-apps/programming/computer-resources/security-and-the-registry.md)
- [Lendo e Gravando do Registro](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)
