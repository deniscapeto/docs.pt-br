---
title: Fluxo
ms.date: 03/30/2017
ms.assetid: 58a3db81-20ab-4627-bf31-39d30b70b4fe
ms.openlocfilehash: 3f52ba01dfd3290e4b0f728e5832a11f2f9c3eeb
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045467"
---
# <a name="stream"></a>Fluxo
O exemplo de fluxo demonstra o uso da comunicação do modo de transferência de streaming. O serviço expõe várias operações que enviam e recebem fluxos. Este exemplo é auto-hospedado. O cliente e o serviço são programas de console.  
  
> [!NOTE]
> O procedimento de instalação e as instruções de Build para este exemplo estão localizados no final deste tópico.  
  
 O Windows Communication Foundation (WCF) pode se comunicar em dois modos de transferência — em buffer ou streaming. No modo de transferência em buffer padrão, uma mensagem deve ser totalmente entregue antes que um receptor possa lê-la. No modo de transferência de streaming, o receptor pode começar a processar a mensagem antes de ser totalmente entregue. O modo de streaming é útil quando as informações que são passadas são demoradas e podem ser processadas em série. O modo de streaming também é útil quando a mensagem é muito grande para ser totalmente armazenada em buffer.  
  
## <a name="streaming-and-service-contracts"></a>Contratos de streaming e serviço  
 O streaming é algo a ser considerado ao criar um contrato de serviço. Se uma operação receber ou retornar grandes quantidades de dados, considere transmitir esses dados para evitar uma alta utilização de memória devido ao buffer de mensagens de entrada ou saída. Para transmitir dados, o parâmetro que mantém esses dados deve ser o único parâmetro na mensagem. Por exemplo, se a mensagem de entrada for aquela a ser transmitida, a operação deverá ter exatamente um parâmetro de entrada. Da mesma forma, se a mensagem de saída for para ser transmitida, a operação deverá ter exatamente um parâmetro de saída ou um valor de retorno. Em ambos os casos, o parâmetro ou o tipo de valor de `Stream`retorno `Message`deve ser `IXmlSerializable`, ou. Este é o contrato de serviço usado neste exemplo de streaming.  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IStreamingSample  
{  
    [OperationContract]  
    Stream GetStream(string data);  
    [OperationContract]  
    bool UploadStream(Stream stream);  
    [OperationContract]  
    Stream EchoStream(Stream stream);  
    [OperationContract]  
    Stream GetReversedStream();  
  
}  
```  
  
 A `GetStream` operação recebe alguns dados de entrada como uma cadeia de caracteres, que é armazenada em `Stream`buffer e retorna um, que é transmitido. Por outro lado, `UploadStream` o leva em `Stream` um (transmitido) e retorna `bool` um (em buffer). `EchoStream`Pega e retorna `Stream` e é um exemplo de uma operação cujas mensagens de entrada e saída são transmitidas. Por fim `GetReversedStream` , o não usa entradas e `Stream` retorna um (transmitido).  
  
## <a name="enabling-streamed-transfers"></a>Habilitando transferências em fluxo  
 Definir os contratos de operação conforme descrito anteriormente fornece streaming no nível de modelo de programação. Se você parar lá, o transporte ainda armazenará em buffer todo o conteúdo da mensagem. Para habilitar o streaming de transporte, selecione um modo de transferência no elemento de associação do transporte. O elemento Binding tem uma `TransferMode` propriedade que pode ser definida como `Buffered`, `Streamed`, `StreamedRequest`ou `StreamedResponse`. Definir o modo de transferência `Streamed` para habilita a comunicação de streaming em ambas as direções. Definir o modo de transferência `StreamedRequest` como `StreamedResponse` ou habilita a comunicação de streaming somente na solicitação ou resposta, respectivamente.  
  
 O `basicHttpBinding` expõe a `TransferMode` Propriedade na associação como faz `NetTcpBinding` e `NetNamedPipeBinding`. Para outros transportes, você deve criar uma associação personalizada para definir o modo de transferência.  
  
 O código de configuração a seguir do exemplo mostra a `TransferMode` configuração da propriedade como streaming `basicHttpBinding` no e uma associação http personalizada:  
  
```xml  
<!-- An example basicHttpBinding using streaming. -->  
<basicHttpBinding>  
  <binding name="HttpStreaming" maxReceivedMessageSize="67108864"  
           transferMode="Streamed"/>  
</basicHttpBinding>  
<!-- An example customBinding using HTTP and streaming.-->  
<customBinding>  
  <binding name="Soap12">  
    <textMessageEncoding messageVersion="Soap12WSAddressing10" />  
    <httpTransport transferMode="Streamed"  
                   maxReceivedMessageSize="67108864"/>  
  </binding>  
</customBinding>  
```  
  
 Além de definir `transferMode` como `Streamed`, o código de configuração anterior define o `maxReceivedMessageSize` para 64MB. Como um mecanismo de defesa `maxReceivedMessageSize` , o coloca um limite no tamanho máximo permitido de mensagens em recebimento. O padrão `maxReceivedMessageSize` é 64 KB, que geralmente é muito baixo para cenários de streaming.  
  
## <a name="processing-data-as-it-is-streamed"></a>Processando dados conforme são transmitidos  
 As operações `GetStream` `UploadStream` e`EchoStream` todas lidam com o envio de dados diretamente de um arquivo ou o salvamento de dados recebidos diretamente em um arquivo. No entanto, em alguns casos, há um requisito para enviar ou receber grandes quantidades de dados e executar algum processamento em partes dos dados à medida que eles são enviados ou recebidos. Uma maneira de abordar esses cenários é gravar um fluxo personalizado (uma classe derivada de <xref:System.IO.Stream>) que processa os dados conforme eles são lidos ou gravados. A `GetReversedStream` operação e `ReverseStream` a classe são um exemplo disso.  
  
 `GetReversedStream`Cria e retorna uma nova instância do `ReverseStream`. O processamento real ocorre quando o sistema lê a partir `ReverseStream` desse objeto. A `ReverseStream.Read` implementação lê um bloco de bytes do arquivo subjacente, reverte-os e retorna os bytes invertidos. Isso não reverte todo o conteúdo do arquivo; Ele reverte uma parte de bytes de cada vez. Este é um exemplo para mostrar como você pode executar o processamento de fluxo, pois o conteúdo está sendo lido ou gravado de e para o fluxo.  
  
```csharp
class ReverseStream : Stream  
{  
  
    FileStream inStream;  
    internal ReverseStream(string filePath)  
    {  
        //Opens the file and places a StreamReader around it.  
        inStream = File.OpenRead(filePath);  
    }  
  
    // Other methods removed for brevity.  
  
    public override int Read(byte[] buffer, int offset, int count)  
    {  
        int countRead=inStream.Read(buffer, offset,count);  
        ReverseBuffer(buffer, offset, countRead);  
        return countRead;  
    }  
  
    public override void Close()  
    {  
        inStream.Close();  
        base.Close();  
    }  
    protected override void Dispose(bool disposing)  
    {  
        inStream.Dispose();  
        base.Dispose(disposing);  
    }  
    void ReverseBuffer(byte[] buffer, int offset, int count)  
    {  
        int i, j;  
        for (i = offset, j = offset + count - 1; i < j; i++, j--)  
        {  
            byte currenti = buffer[i];  
            buffer[i] = buffer[j];  
            buffer[j] = currenti;  
        }  
  
    }  
}  
```  
  
## <a name="running-the-sample"></a>Executando o exemplo  
 Para executar o exemplo, primeiro crie o serviço e o cliente seguindo as instruções no final deste documento. Em seguida, inicie o serviço e o cliente em duas janelas de console diferentes. Quando o cliente for iniciado, ele aguardará que você pressione ENTER quando o serviço estiver pronto. Em seguida, o cliente chama `GetStream()`os `UploadStream()` métodos `GetReversedStream()` e primeiro por http e, em seguida, sobre TCP. Aqui está um exemplo de saída do serviço seguido por exemplo de saída do cliente:  
  
 Saída do serviço:  
  
```console  
The streaming service is ready.  
Press <ENTER> to terminate service.  
  
Saving to file D:\...\uploadedfile  
......................  
File D:\...\uploadedfile saved  
Saving to file D:\...\uploadedfile  
...............  
File D:\...\uploadedfile saved  
```  
  
 Saída do cliente:  
  
```console  
Press <ENTER> when service is ready  
------ Using HTTP ------   
Calling GetStream()  
Saving to file D:\...\clientfile  
......................  
Wrote 33405 bytes to stream  
  
File D:\...\clientfile saved  
Calling UploadStream()  
Calling GetReversedStream()  
Saving to file D:\...\clientfile  
......................  
Wrote 33405 bytes to stream  
  
File D:\...\clientfile saved  
------ Using Custom HTTP ------  
Calling GetStream()  
Saving to file D:\...\clientfile  
...............  
Wrote 33405 bytes to stream  
  
File D:\...\clientfile saved  
Calling UploadStream()  
Calling GetReversedStream()  
Saving to file D:\...\clientfile  
...............  
Wrote 33405 bytes to stream  
  
File D:\...\clientfile saved  
  
Press <ENTER> to terminate client.  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo  
  
1. Verifique se você executou o [procedimento de configuração única para os exemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Para compilar a C# edição do ou Visual Basic .NET da solução, siga as instruções em [criando os exemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3. Para executar o exemplo em uma configuração de computador único ou cruzado, siga as instruções em [executando os exemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!NOTE]
> Se você usar svcutil. exe para regenerar a configuração para este exemplo, certifique-se de modificar o nome do ponto de extremidade na configuração do cliente para corresponder ao código do cliente.  
  
> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para baixar todos os Windows Communication Foundation (WCF) [!INCLUDE[wf1](../../../../includes/wf1-md.md)] e exemplos. Este exemplo está localizado no seguinte diretório.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Service\Stream`  
