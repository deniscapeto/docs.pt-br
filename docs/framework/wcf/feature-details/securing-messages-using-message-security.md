---
title: Protegendo as mensagens com a segurança de mensagens
ms.date: 03/30/2017
ms.assetid: a17ebe67-836b-4c52-9a81-2c3d58e225ee
ms.openlocfilehash: 9ba8923d23140bb951a4993739ec267ad6f6a4c4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69911769"
---
# <a name="securing-messages-using-message-security"></a>Protegendo as mensagens com a segurança de mensagens
Esta seção aborda a segurança de mensagens do WCF <xref:System.ServiceModel.NetMsmqBinding>ao usar o.  
  
> [!NOTE]
> Antes de ler este tópico, é recomendável que você leia os [conceitos de segurança](../../../../docs/framework/wcf/feature-details/security-concepts.md).  
  
 A ilustração a seguir fornece um modelo conceitual de comunicação em fila usando o WCF. Esta ilustração e terminologia são usadas para explicar  
  
 conceitos de segurança de transporte.  
  
 ![Diagrama de aplicativo na fila](../../../../docs/framework/wcf/feature-details/media/distributed-queue-figure.jpg "Distributed-Queue-figura")  
  
 Ao enviar mensagens em fila usando o WCF, a mensagem WCF é anexada como um corpo da mensagem do serviço de enfileiramento de mensagens (MSMQ). Embora a segurança de transporte proteja toda a mensagem do MSMQ, a segurança de mensagem (ou SOAP) só protege o corpo da mensagem MSMQ.  
  
 O principal conceito de segurança de mensagem é que o cliente protege a mensagem para o aplicativo de recebimento (serviço), diferentemente da segurança de transporte em que o cliente protege a mensagem para a fila de destino. Dessa forma, o MSMQ não desempenha nenhuma parte ao proteger a mensagem do WCF usando a segurança da mensagem.  
  
 A segurança de mensagens do WCF adiciona cabeçalhos de segurança à mensagem do WCF que se integram a infraestruturas de segurança existentes, como um certificado ou o protocolo Kerberos.  
  
## <a name="message-credential-type"></a>Tipo de credencial da mensagem  
 Usando a segurança da mensagem, o serviço e o cliente podem apresentar credenciais para autenticar um ao outro. Você pode selecionar segurança de mensagem definindo o <xref:System.ServiceModel.NetMsmqBinding.Security%2A> modo como `Message` ou `Both` (ou seja, usar segurança de transporte e segurança de mensagem).  
  
 O serviço pode usar a <xref:System.ServiceModel.ServiceSecurityContext.Current%2A> propriedade para inspecionar a credencial usada para autenticar o cliente. Isso também pode ser usado para outras verificações de autorização que o serviço opta por implementar.  
  
 Esta seção explica os diferentes tipos de credenciais e como usá-los com filas do.  
  
### <a name="certificate"></a>Certificate  
 O tipo de credencial do certificado usa um certificado X. 509 para identificar o serviço e o cliente.  
  
 Em um cenário típico, o cliente e o serviço são emitidos um certificado válido por uma autoridade de certificação confiável. Em seguida, a conexão é estabelecida, o cliente autentica a validade do serviço usando o certificado do serviço para decidir se ele pode confiar no serviço. Da mesma forma, o serviço usa o certificado do cliente para validar a relação de confiança do cliente.  
  
 Considerando a natureza desconectada das filas, o cliente e o serviço podem não estar online ao mesmo tempo. Assim, o cliente e o serviço precisam trocar certificados fora de banda. Em particular, o cliente, em virtude de manter o certificado do serviço (que pode ser encadeado a uma autoridade de certificação) em seu repositório confiável, deve confiar que está se comunicando com o serviço correto. Para autenticar o cliente, o serviço usa o certificado X. 509 anexado à mensagem para que ele corresponda ao certificado em seu repositório para verificar a autenticidade do cliente. Novamente, o certificado deve ser encadeado a uma autoridade de certificação.  
  
 Em um computador que executa o Windows, os certificados são mantidos em vários tipos de armazenamentos. Para obter mais informações sobre os diferentes repositórios, consulte repositórios de [certificados](https://go.microsoft.com/fwlink/?LinkId=87787).  
  
### <a name="windows"></a>Windows  
 O tipo de credencial de mensagem do Windows usa o protocolo Kerberos.  
  
 O protocolo Kerberos é um mecanismo de segurança que autentica os usuários em um domínio e permite que os usuários autenticados estabeleçam contextos seguros com outras entidades em um domínio.  
  
 O problema com o uso do protocolo Kerberos para a comunicação em fila é que os tíquetes que contêm a identidade do cliente que o centro de distribuição de chaves (KDC) distribui são uma vida relativamente curta. Um *tempo de vida* é associado ao tíquete Kerberos que indica a validade do tíquete. Assim, dada latência alta, você não pode ter certeza de que o token ainda é válido para o serviço que autentica o cliente.  
  
 Observe que, ao usar esse tipo de credencial, o serviço deve estar em execução na conta de serviço.  
  
 O protocolo Kerberos é usado por padrão ao escolher a credencial da mensagem. Para obter mais informações, consulte [explorando o Kerberos, o protocolo para segurança distribuída no Windows 2000](https://go.microsoft.com/fwlink/?LinkId=87790).  
  
### <a name="username-password"></a>Senha do nome de usuário  
 Usando essa propriedade, o cliente pode se autenticar no servidor usando uma senha de nome de usuário no cabeçalho de segurança da mensagem.  
  
### <a name="issuedtoken"></a>IssuedToken  
 O cliente pode usar o serviço de token de segurança para emitir um token que pode ser anexado à mensagem para que o serviço autentique o cliente.  
  
## <a name="using-transport-and-message-security"></a>Usando segurança de mensagens e transporte  
 Ao usar a segurança de transporte e a segurança de mensagem, o certificado usado para proteger a mensagem no transporte e o nível de mensagem SOAP deve ser o mesmo.  
  
## <a name="see-also"></a>Consulte também

- [Protegendo mensagens usando a segurança do transporte](../../../../docs/framework/wcf/feature-details/securing-messages-using-transport-security.md)
- [Segurança de mensagem através do enfileiramento de mensagem](../../../../docs/framework/wcf/samples/message-security-over-message-queuing.md)
- [Conceitos de segurança](../../../../docs/framework/wcf/feature-details/security-concepts.md)
- [Protegendo serviços e clientes](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
