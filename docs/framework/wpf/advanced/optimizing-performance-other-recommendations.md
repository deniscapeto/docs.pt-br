---
title: 'Otimizando desempenho: Outras recomendações'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Terminal Services rendering [WPF]
- opacity [WPF]
- hit-test objects [WPF]
- ScrollBarVisibility enumeration [WPF]
- brushes [WPF], performance
ms.assetid: d028cc65-7e97-4a4f-9859-929734eaf40d
ms.openlocfilehash: 9757a8c8327feb40018387473b479e467149f0ed
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64611901"
---
# <a name="optimizing-performance-other-recommendations"></a>Otimizando desempenho: Outras recomendações
<a name="introduction"></a> Este tópico apresenta recomendações de desempenho além daquelas abordadas pelos tópicos na seção [Otimizando o desempenho do aplicativo WPF](optimizing-wpf-application-performance.md).  
  
 Esse tópico contém as seguintes seções:  
  
- [Opacidade em pincéis versus opacidade em elementos](#Opacity)  
  
- [Navegação para objeto](#Navigation_Objects)  
  
- [Testes de clique em grandes superfícies 3D](#Hit_Testing)  
  
- [Evento CompositionTarget.Rendering](#CompositionTarget_Rendering_Event)  
  
- [Evite usar ScrollBarVisibility=Auto](#Avoid_Using_ScrollBarVisibility)  
  
- [Configurar o serviço de cache de fonte para reduzir o tempo de inicialização](#FontCache)  
  
<a name="Opacity"></a>   
## <a name="opacity-on-brushes-versus-opacity-on-elements"></a>Opacidade em pincéis versus opacidade em elementos  
 Quando você usa um <xref:System.Windows.Media.Brush> para definir o <xref:System.Windows.Shapes.Shape.Fill%2A> ou <xref:System.Windows.Shapes.Shape.Stroke%2A> de um elemento, é melhor definir a <xref:System.Windows.Media.Brush.Opacity%2A?displayProperty=nameWithType> em vez da configuração de valor do elemento <xref:System.Windows.UIElement.Opacity%2A> propriedade. Modificar um elemento <xref:System.Windows.UIElement.Opacity%2A> pode fazer com que uma propriedade [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] para criar uma superfície temporária.  
  
<a name="Navigation_Objects"></a>   
## <a name="navigation-to-object"></a>Navegação para objeto  
 O <xref:System.Windows.Navigation.NavigationWindow> objeto deriva <xref:System.Windows.Window> e a estende com suporte de navegação de conteúdo, principalmente agregando <xref:System.Windows.Navigation.NavigationService> e o diário. Você pode atualizar a área do cliente <xref:System.Windows.Navigation.NavigationWindow> , especificando a um [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] ou um objeto. O exemplo a seguir mostra os dois métodos:  
  
 [!code-csharp[Performance#PerformanceSnippet14](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/TestNavigation.xaml.cs#performancesnippet14)]
 [!code-vb[Performance#PerformanceSnippet14](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/testnavigation.xaml.vb#performancesnippet14)]  
  
 Cada <xref:System.Windows.Navigation.NavigationWindow> objeto tem um diário que registra o histórico de navegação do usuário na janela. Uma das finalidades do diário é permitir aos usuários rastrear seus passos.  
  
 Quando você navega usando um [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)], o diário armazena apenas a referência [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]. Isso significa que sempre que você revisita a página, ela é dinamicamente reconstruída, o que pode ser demorado, dependendo da complexidade da página. Nesse caso, o custo de armazenamento do diário é baixo, mas o tempo para reconstituir a página é potencialmente alto.  
  
 Quando você navega usando um objeto, o diário armazena toda a árvore visual do objeto. Isso significa que sempre que você revisita a página, ela é renderizada imediatamente sem precisar ser reconstruída. Nesse caso, o custo de armazenamento do diário é alto, mas o tempo para reconstituir a página é baixo.  
  
 Quando você usa o <xref:System.Windows.Navigation.NavigationWindow> do objeto, você precisará ter em mente como o suporte de diário afeta o desempenho do seu aplicativo. Para obter mais informações, consulte [Visão geral de navegação](../app-development/navigation-overview.md).  
  
<a name="Hit_Testing"></a>   
## <a name="hit-testing-on-large-3d-surfaces"></a>Testes de clique em grandes superfícies 3D  
 Teste de clique em grandes superfícies 3D é uma operação com uso intenso de desempenho em termos de consumo de CPU. Isso é especialmente verdadeiro quando a superfície 3D é animada. Se você não precisar de teste de clique nessas superfícies, desabilite-o. Objetos que são derivados de <xref:System.Windows.UIElement> pode desabilitar o teste de clique, definindo o <xref:System.Windows.UIElement.IsHitTestVisible%2A> propriedade `false`.  
  
<a name="CompositionTarget_Rendering_Event"></a>   
## <a name="compositiontargetrendering-event"></a>Evento CompositionTarget.Rendering  
 O <xref:System.Windows.Media.CompositionTarget.Rendering?displayProperty=nameWithType> faz com que o evento [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] animado continuamente. Se você usar esse evento, desanexe-o em cada oportunidade.  
  
<a name="Avoid_Using_ScrollBarVisibility"></a>   
## <a name="avoid-using-scrollbarvisibilityauto"></a>Evite usar ScrollBarVisibility=Auto  
 Sempre que possível, evite usar o <xref:System.Windows.Controls.ScrollBarVisibility.Auto?displayProperty=nameWithType> de valor para o `HorizontalScrollBarVisibility` e `VerticalScrollBarVisibility` propriedades. Essas propriedades são definidas para <xref:System.Windows.Controls.RichTextBox>, <xref:System.Windows.Controls.ScrollViewer>, e <xref:System.Windows.Controls.TextBox> objetos e como uma propriedade anexada para o <xref:System.Windows.Controls.ListBox> objeto. Em vez disso, defina <xref:System.Windows.Controls.ScrollBarVisibility> à <xref:System.Windows.Controls.ScrollBarVisibility.Disabled>, <xref:System.Windows.Controls.ScrollBarVisibility.Hidden>, ou <xref:System.Windows.Controls.ScrollBarVisibility.Visible>.  
  
 O <xref:System.Windows.Controls.ScrollBarVisibility.Auto> valor destina-se para casos quando o espaço é limitado e barras de rolagem devem ser exibidas somente quando necessário. Por exemplo, pode ser útil para usar esse <xref:System.Windows.Controls.ScrollBarVisibility> valor com um <xref:System.Windows.Controls.ListBox> de 30 itens em oposição a um <xref:System.Windows.Controls.TextBox> com centenas de linhas de texto.  
  
<a name="FontCache"></a>   
## <a name="configure-font-cache-service-to-reduce-start-up-time"></a>Configurar o serviço de cache de fonte para reduzir o tempo de inicialização  
 O serviço de Cache de Fontes [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] compartilha dados de fontes entre aplicativos [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]. O primeiro aplicativo [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] executado iniciará esse serviço se o serviço ainda não estiver em execução. Se você estiver usando [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)], você pode definir o serviço "Windows Presentation Foundation (WPF) fonte Cache 3.0.0.0" de "Manual" (o padrão) para "Automático (início atrasado)" para reduzir o tempo de inicialização inicial dos [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] aplicativos.  
  
## <a name="see-also"></a>Consulte também

- [Planejando para desempenho do aplicativo](planning-for-application-performance.md)
- [Aproveitando o hardware](optimizing-performance-taking-advantage-of-hardware.md)
- [Layout e design](optimizing-performance-layout-and-design.md)
- [Elementos gráficos e geração de imagens 2D](optimizing-performance-2d-graphics-and-imaging.md)
- [Comportamento do objeto](optimizing-performance-object-behavior.md)
- [Recursos do aplicativo](optimizing-performance-application-resources.md)
- [Texto](optimizing-performance-text.md)
- [Associação de dados](optimizing-performance-data-binding.md)
- [Dicas e truques de animação](../graphics-multimedia/animation-tips-and-tricks.md)
