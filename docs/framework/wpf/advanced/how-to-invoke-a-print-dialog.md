---
title: 'Como: Invocar uma caixa de diálogo Imprimir'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- invoking print dialogs [WPF]
- print dialogs [WPF], invoking
ms.assetid: e3a2c84c-74fe-45a4-8501-5813f9dbfed2
ms.openlocfilehash: 4bad8158925fea8af529f70f92aad74e2a6bbec0
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70254106"
---
# <a name="how-to-invoke-a-print-dialog"></a>Como: Invocar uma caixa de diálogo Imprimir
Para fornecer a capacidade de imprimir a partir do seu aplicativo, você pode simplesmente criar e <xref:System.Windows.Controls.PrintDialog> abrir um objeto.  
  
## <a name="example"></a>Exemplo  
 O <xref:System.Windows.Controls.PrintDialog> controle fornece um único ponto de entrada [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]para o, configuração e envio de trabalho XPS. O controle é fácil de usar e pode ser instanciado usando marcação ou código [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]. O exemplo a seguir demonstra como instanciar e abrir o controle no código e como imprimir por meio dele. Também mostra como assegurar que o diálogo dê ao usuário a opção de definir um intervalo específico de páginas. O código do exemplo pressupõe que existe um arquivo FixedDocumentSequence.xps na raiz da unidade C:.  
  
 [!code-csharp[printdialog#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PrintDialog/CSharp/Window1.xaml.cs#1)]
 [!code-vb[printdialog#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrintDialog/visualbasic/window1.xaml.vb#1)]  
  
 Uma vez que a caixa de diálogo estiver aberta, os usuários poderão selecionar as impressoras instaladas em seu computador. Eles também terão a opção de selecionar o [Microsoft XPS Document Writer](https://go.microsoft.com/fwlink/?LinkId=147319) para criar um arquivo XPS (XML Paper Specification) em vez de imprimir.  
  
> [!NOTE]
> O <xref:System.Windows.Controls.PrintDialog?displayProperty=nameWithType> controle do [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], que é discutido neste tópico, não deve ser confundido com o <xref:System.Windows.Forms.PrintDialog?displayProperty=nameWithType> componente do Windows Forms.  
  
 Estritamente falando, você pode usar o <xref:System.Windows.Controls.PrintDialog.PrintDocument%2A> método sem nunca abrir a caixa de diálogo. Assim, o controle pode ser utilizado como um componente de impressão não visto. Mas, por motivos de desempenho, seria <xref:System.Printing.PrintQueue.AddJob%2A> melhor usar o método ou um dos muitos <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> e <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> métodos do <xref:System.Windows.Xps.XpsDocumentWriter>. Para saber mais, consulte [Impressão Programada de Arquivos XPS](how-to-programmatically-print-xps-files.md).  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Windows.Controls.PrintDialog>
- [Documentos no WPF](documents-in-wpf.md)
- [Visão Geral da Impressão](printing-overview.md)
- [Microsoft XPS Document Writer](https://go.microsoft.com/fwlink/?LinkId=147319)
