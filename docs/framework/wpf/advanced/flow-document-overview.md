---
title: Vue d'ensemble des documents dynamiques
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- 'documents [WPF], flow documents [WPF], , '
- ', '
- flow documents [WPF]
ms.assetid: ef236a50-d44f-43c8-ba7c-82b0c733c0b7
ms.openlocfilehash: 0cf8944298af62a512599fc52998a046c66fed9b
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33549735"
---
# <a name="flow-document-overview"></a>Vue d'ensemble des documents dynamiques
Les documents dynamiques sont conçus pour optimiser l’affichage et la lisibilité. Au lieu d’avoir une disposition prédéfinie, ces documents dynamiques ajustent et refluent dynamiquement leur contenu en fonction des variables d’exécution telles que la taille de la fenêtre, la résolution de l’appareil et les préférences facultatives de l’utilisateur. En outre, les documents dynamiques offrent des fonctionnalités de document avancées, telles que la pagination et les colonnes. Cette rubrique fournit une vue d’ensemble des documents dynamiques et explique comment les créer.  
  

  
<a name="what_is_a_flow_document"></a>   
## <a name="what-is-a-flow-document"></a>Description d’un document dynamique  
 Un document dynamique est conçu pour « redisposer le contenu » en fonction de la taille de la fenêtre, de la résolution de l’appareil et d’autres variables d’environnement. En outre, les documents dynamiques possèdent plusieurs fonctionnalités intégrées, notamment la recherche, les modes d’affichage qui optimisent la lisibilité et la possibilité de changer la taille et l’apparence des polices. Les documents dynamiques sont utilisés surtout quand la facilité de lecture est le scénario principal de consommation des documents. À l’inverse, les documents fixes sont conçus pour avoir une présentation statique. Ces documents sont utiles quand le contenu source doit être fidèlement respecté. Consultez [Documents dans WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md) pour plus d’informations sur les différents types de documents.  
  
 L’illustration suivante montre un exemple de document dynamique affiché dans des fenêtres de différentes tailles. Chaque fois que la zone d’affichage change, le contenu est redisposé pour utiliser de façon optimale l’espace disponible.  
  
 ![Redisposition du contenu du document dynamique](../../../../docs/framework/wpf/advanced/media/edocs-flowdocument.png "eDocs_FlowDocument")  
  
 Comme illustré dans l’image ci-dessus, le contenu dynamique peut comprendre plusieurs composants, notamment des paragraphes, des listes, des images et bien plus encore. Ces composants correspondent à des éléments dans le balisage et à des objets dans le code procédural. Nous allons ces classes en détail ultérieurement dans le [flux des Classes connexes](#flow_related_classes) section de cette vue d’ensemble. Pour l’instant, Voici un exemple de code simple qui crée un document de flux composé d’un paragraphe avec du texte en gras et une liste.
  
 [!code-xaml[FlowOvwSnippets_snip#SimpleFlowExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SimpleFlowExample.xaml#simpleflowexamplewholepage)]  
  
 [!code-csharp[FlowOvwSnippets_procedural_snip#SimpleFlowCodeOnlyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/SimpleFlowExample.cs#simpleflowcodeonlyexamplewholepage)]
 [!code-vb[FlowOvwSnippets_procedural_snip#SimpleFlowCodeOnlyExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/SimpleFlowExample.vb#simpleflowcodeonlyexamplewholepage)]  
  
 Cet extrait de code est illustré ci-dessous.  
  
 ![Capture d’écran : exemple d’affichage de FlowDocument](../../../../docs/framework/wpf/advanced/media/flow-ovw-first-example.png "Flow_Ovw_First_Example")  
  
 Dans cet exemple, le <xref:System.Windows.Controls.FlowDocumentReader> contrôle est utilisé pour héberger le contenu de flux. Consultez [les Types de Document de flux](#flow_document_types) pour plus d’informations sur l’hébergement de contrôles de contenu de flux. <xref:System.Windows.Documents.Paragraph>, <xref:System.Windows.Documents.List>, <xref:System.Windows.Documents.ListItem>, et <xref:System.Windows.Documents.Bold> éléments sont utilisés pour contrôler la mise en forme du contenu, selon leur ordre dans le balisage. Par exemple, le <xref:System.Windows.Documents.Bold> élément s’étend uniquement sur une partie du texte dans le paragraphe ; par conséquent, seule la partie du texte en gras. Si vous avez déjà utilisé le langage HTML, cela doit vous sembler familier.  
  
 Mise en évidence dans l’illustration ci-dessus, il existe plusieurs fonctionnalités intégrées dans les Documents de flux :
  
-   Recherche : permet à l’utilisateur d’effectuer une recherche en texte intégral sur l’ensemble d’un document.  
  
-   Mode d’affichage : l’utilisateur peut sélectionner son mode d’affichage préféré parmi le mode d’affichage page unique (page par page), deux pages à la fois (format livre ouvert) ou défilement continu (sans marge inférieure).  Pour plus d’informations sur les modes d’affichage, consultez <xref:System.Windows.Controls.FlowDocumentReaderViewingMode>.  
  
-   Contrôles de navigation des pages : si le mode d’affichage du document utilise des pages, les contrôles de navigation des pages incluent un bouton pour accéder à la page suivante (flèche Bas) ou à la page précédente (flèche Haut), ainsi qu’une indication du numéro de la page active et du nombre total de pages. Vous pouvez aussi faire défiler les pages à l’aide des touches de direction du clavier.  
  
-   Zoom : les contrôles de zoom permettent à l’utilisateur d’augmenter ou de diminuer le niveau de zoom en cliquant sur les boutons plus ou moins, respectivement. Les contrôles de zoom incluent également un curseur pour ajuster le niveau de zoom. Pour plus d'informations, consultez <xref:System.Windows.Controls.FlowDocumentReader.Zoom%2A>.  
  
 Ces fonctionnalités peuvent être modifiées selon le contrôle utilisé pour héberger le contenu dynamique. La section suivante décrit les différents contrôles.  
  
<a name="flow_document_types"></a>   
## <a name="flow-document-types"></a>Types de documents dynamiques  
 L’affichage et l’apparence du contenu des documents dynamiques dépendent de l’objet utilisé pour héberger le contenu dynamique. Il existe quatre contrôles qui prennent en charge l’affichage de contenu de flux : <xref:System.Windows.Controls.FlowDocumentReader>, <xref:System.Windows.Controls.FlowDocumentPageViewer>, <xref:System.Windows.Controls.RichTextBox>, et <xref:System.Windows.Controls.FlowDocumentScrollViewer>. Ces contrôles sont brièvement décrits ci-dessous.  
  
 **Remarque :** <xref:System.Windows.Documents.FlowDocument> est nécessaire pour directement le contenu de flux hôte, par conséquent, tous ces contrôles d’affichage consomment un <xref:System.Windows.Documents.FlowDocument> pour activer l’hébergement du contenu dynamique.  
  
### <a name="flowdocumentreader"></a>FlowDocumentReader  
 <xref:System.Windows.Controls.FlowDocumentReader> inclut des fonctionnalités qui permettent aux utilisateurs de choisir dynamiquement entre plusieurs modes d’affichage, y compris un mode d’affichage de page unique (page-à-un-time), deux page-à-un à la fois (format livre) un mode de défilement continu (sans marge inférieure) et du mode d’affichage. Pour plus d’informations sur les modes d’affichage, consultez <xref:System.Windows.Controls.FlowDocumentReaderViewingMode>. Si vous n’avez pas besoin de la possibilité de basculer dynamiquement entre les différents modes d’affichage, <xref:System.Windows.Controls.FlowDocumentPageViewer> et <xref:System.Windows.Controls.FlowDocumentScrollViewer> fournissent les flux légère afficheurs de contenu qui sont résolus dans un mode d’affichage particulier.  
  
### <a name="flowdocumentpageviewer-and-flowdocumentscrollviewer"></a>FlowDocumentPageViewer et FlowDocumentScrollViewer  
 <xref:System.Windows.Controls.FlowDocumentPageViewer> Affiche le contenu dans la page au moment mode d’affichage, tandis que <xref:System.Windows.Controls.FlowDocumentScrollViewer> affiche le contenu en mode de défilement continu. Les deux <xref:System.Windows.Controls.FlowDocumentPageViewer> et <xref:System.Windows.Controls.FlowDocumentScrollViewer> sont fixés pour un mode d’affichage particulier. Comparer à <xref:System.Windows.Controls.FlowDocumentReader>, qui inclut des fonctionnalités qui permettent aux utilisateurs de choisir dynamiquement entre plusieurs modes d’affichage (tel que fourni par le <xref:System.Windows.Controls.FlowDocumentReaderViewingMode> énumération), au détriment de la plus performante que celle de ressources <xref:System.Windows.Controls.FlowDocumentPageViewer> ou <xref:System.Windows.Controls.FlowDocumentScrollViewer>.  
  
 Par défaut, une barre de défilement verticale est toujours affichée et une barre de défilement horizontale apparaît si nécessaire. La valeur par défaut l’interface utilisateur pour <xref:System.Windows.Controls.FlowDocumentScrollViewer> n’inclut pas d’une barre d’outils ; Toutefois, le <xref:System.Windows.Controls.FlowDocumentScrollViewer.IsToolBarVisible%2A> propriété peut être utilisée pour activer une barre d’outils.  
  
### <a name="richtextbox"></a>RichTextBox  
 Vous utilisez un <xref:System.Windows.Controls.RichTextBox> lorsque vous souhaitez autoriser l’utilisateur à modifier le contenu de flux. Par exemple, si vous souhaitez créer un éditeur qui autorise l’utilisateur à manipuler des choses comme les tables, italique et en gras de la mise en forme, etc., vous devez utiliser un <xref:System.Windows.Controls.RichTextBox>. Consultez [vue d’ensemble de RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md) pour plus d’informations.  
  
 **Remarque :** du contenu à l’intérieur d’un <xref:System.Windows.Controls.RichTextBox> ne se comporte pas exactement comme le contenu de flux contenu dans d’autres contrôles. Par exemple, il n’existe aucune colonne dans un <xref:System.Windows.Controls.RichTextBox> et donc pas de redimensionnement automatique. En outre, les fonctionnalités généralement intégrées de contenu de flux comme la recherche, affichage du mode de navigation entre les pages et zoom ne sont pas disponibles dans un <xref:System.Windows.Controls.RichTextBox>.  
  
<a name="creating_flow_content"></a>   
## <a name="creating-flow-content"></a>Création de contenu dynamique  
 Le contenu de flux peut être complexe, consistant de différents éléments, y compris le texte, des images, des tables et même <xref:System.Windows.UIElement> dérivées des classes telles que des contrôles. Pour comprendre comment créer du contenu dynamique complexe, les points suivants sont essentiels :  
  
-   **Classes liées au contenu dynamique** : chaque classe utilisée dans le contenu dynamique a un rôle spécifique. En outre, la relation hiérarchique entre les classes vous permet de comprendre comment elles sont utilisées. Par exemple, les classes dérivées de la <xref:System.Windows.Documents.Block> classe sont utilisés pour contenir d’autres objets alors que les classes dérivées de <xref:System.Windows.Documents.Inline> contiennent les objets sont affichés.  
  
-   **Schéma du contenu** : un document dynamique peut nécessiter un nombre important d’éléments imbriqués. Le schéma du contenu indique les relations parent/enfant possibles entre les éléments.  
  
 Les sections suivantes décrivent en détail chacun des points ci-dessus.  
  
<a name="flow_related_classes"></a>   
## <a name="flow-related-classes"></a>Classes liées au contenu dynamique  
 Le diagramme ci-dessous contient les objets les plus souvent utilisés avec du contenu dynamique :  
  
 ![Diagramme : hiérarchie de classes d’éléments de contenu dynamique](../../../../docs/framework/wpf/advanced/media/flow-class-hierarchy.png "Flow_Class_Hierarchy")  
  
 Pour faciliter la gestion du contenu dynamique, il existe deux catégories principales :  
  
1.  **Classes dérivées de Block** : elles sont également appelées « éléments de contenu Block » ou simplement « éléments Block ». Les éléments qui héritent de <xref:System.Windows.Documents.Block> peut être utilisé pour grouper des éléments sous un parent commun ou appliquer des attributs communs à un groupe.  
  
2.  **Classes dérivées d’Inline** : elles sont également appelées « éléments de contenu Inline » ou simplement « éléments Inline ». Les éléments qui héritent de <xref:System.Windows.Documents.Inline> soit contenus dans un élément de bloc ou d’un autre Inline élément. Les éléments Inline sont souvent utilisés comme conteneur direct du contenu restitué à l’écran. Par exemple, un <xref:System.Windows.Documents.Paragraph> (élément Block) peut contenir un <xref:System.Windows.Documents.Run> (Inline élément), mais le <xref:System.Windows.Documents.Run> réellement contient le texte est restitué à l’écran.  
  
 Chaque classe de ces deux catégories est brièvement décrite ci-dessous.  
  
### <a name="block-derived-classes"></a>Classes dérivées de Block  
 **Paragraph**  
  
 <xref:System.Windows.Documents.Paragraph> est généralement utilisé pour grouper le contenu dans un paragraphe. L’utilisation la plus courante et la plus simple de Paragraph consiste à créer un paragraphe de texte.  
  
 [!code-xaml[FlowOvwSnippets_snip#ParagraphExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/ParagraphExample.xaml#paragraphexamplewholepage)]  
  
 [!code-csharp[FlowOvwSnippets_procedural_snip#ParagraphCodeOnlyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/ParagraphExample.cs#paragraphcodeonlyexamplewholepage)]
 [!code-vb[FlowOvwSnippets_procedural_snip#ParagraphCodeOnlyExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/ParagraphExample.vb#paragraphcodeonlyexamplewholepage)]  
  
 Toutefois, vous pouvez également inclure des autres éléments dérivés d’inline comme vous le verrez ci-dessous. 
  
 **Section**  
  
 <xref:System.Windows.Documents.Section> est utilisé uniquement pour contenir d’autres <xref:System.Windows.Documents.Block>-éléments dérivés. Il n’applique aucune mise en forme par défaut aux éléments qu’il contient. Toutefois, les valeurs de propriété set sur un <xref:System.Windows.Documents.Section> s’applique à ses éléments enfants. Une section vous permet également d’itérer par programmation dans sa collection enfant. <xref:System.Windows.Documents.Section> est utilisé d’une manière similaire à la \<DIV > balise HTML.  
  
 Dans l’exemple ci-dessous, trois paragraphes sont définis sous un <xref:System.Windows.Documents.Section>. La section comporte un <xref:System.Windows.Documents.TextElement.Background%2A> valeur de propriété de rouge, par conséquent, la couleur d’arrière-plan des paragraphes est également rouge.  
  
 [!code-xaml[FlowOvwSnippets_snip#SectionExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SectionExample.xaml#sectionexamplewholepage)]  
  
 [!code-csharp[FlowOvwSnippets_procedural_snip#SectionCodeOnlyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/SectionExample.cs#sectioncodeonlyexamplewholepage)]
 [!code-vb[FlowOvwSnippets_procedural_snip#SectionCodeOnlyExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/SectionExample.vb#sectioncodeonlyexamplewholepage)]  
  
 **BlockUIContainer**  
  
 <xref:System.Windows.Documents.BlockUIContainer> permet de <xref:System.Windows.UIElement> éléments (c'est-à-dire un <xref:System.Windows.Controls.Button>) à incorporer dans le contenu de flux dérivé d’un bloc. <xref:System.Windows.Documents.InlineUIContainer> (voir ci-dessous) est utilisé pour incorporer <xref:System.Windows.UIElement> éléments de contenu de flux inline. <xref:System.Windows.Documents.BlockUIContainer> et <xref:System.Windows.Documents.InlineUIContainer> sont importantes, car il est impossible d’utiliser un <xref:System.Windows.UIElement> dans le flux de contenu, sauf si elle est contenue dans une de ces deux éléments.  
  
 L’exemple suivant montre comment utiliser le <xref:System.Windows.Documents.BlockUIContainer> élément hôte <xref:System.Windows.UIElement> objets dans le contenu de flux.  
  
 [!code-xaml[SpanSnippets#_BlockUIXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml#_blockuixaml)]  
  
 La figure suivante montre le rendu de cet exemple.  
  
 ![Capture d’écran : UIElement incorporé dans le contenu dynamique](../../../../docs/framework/wpf/advanced/media/blockuicontainer.png "BlockUIContainer")  
  
 **List**  
  
 <xref:System.Windows.Documents.List> est utilisé pour créer une liste à puces ou numérique. Définir le <xref:System.Windows.Documents.List.MarkerStyle%2A> propriété un <xref:System.Windows.TextMarkerStyle> valeur d’énumération pour déterminer le style de la liste. L’exemple ci-dessous montre comment créer une liste simple.  
  
 [!code-xaml[FlowOvwSnippets_snip#ListExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/ListExample.xaml#listexamplewholepage)]  
  
 [!code-csharp[FlowOvwSnippets_procedural_snip#ListCodeOnlyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/ListExample.cs#listcodeonlyexamplewholepage)]
 [!code-vb[FlowOvwSnippets_procedural_snip#ListCodeOnlyExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/ListExample.vb#listcodeonlyexamplewholepage)]  
  
 **Remarque :** <xref:System.Windows.Documents.List> est le seul élément de flux qui utilise le <xref:System.Windows.Documents.ListItemCollection> pour gérer les éléments enfants.  
  
 **Table**  
  
 <xref:System.Windows.Documents.Table> est utilisé pour créer une table. <xref:System.Windows.Documents.Table> est similaire à la <xref:System.Windows.Controls.Grid> élément mais il présente davantage de fonctions et, par conséquent, requiert une charge importante de ressources. Étant donné que <xref:System.Windows.Controls.Grid> est un <xref:System.Windows.UIElement>, il ne peut pas être utilisé dans le contenu de flux, sauf si elle est contenue dans un <xref:System.Windows.Documents.BlockUIContainer> ou <xref:System.Windows.Documents.InlineUIContainer>. Pour plus d’informations sur <xref:System.Windows.Documents.Table>, consultez [vue d’ensemble de la Table](../../../../docs/framework/wpf/advanced/table-overview.md).  
  
### <a name="inline-derived-classes"></a>Classes dérivées d’Inline  
 **Exécuter**  
  
 <xref:System.Windows.Documents.Run> est utilisé pour contenir du texte sans mise en forme. Vous pouvez vous attendre <xref:System.Windows.Documents.Run> objets à être largement utilisé dans le contenu de flux. Toutefois, dans le balisage, <xref:System.Windows.Documents.Run> éléments ne doivent pas être utilisés de manière explicite. <xref:System.Windows.Documents.Run> est requis pour être utilisé lorsque vous créez ou manipulez des documents dynamiques à l’aide de code. Par exemple, dans le balisage ci-dessous, le premier <xref:System.Windows.Documents.Paragraph> Spécifie le <xref:System.Windows.Documents.Run> n’est pas le cas de l’élément explicitement lors de la seconde. Les deux paragraphes génèrent le même résultat.  
  
 [!code-xaml[FlowOvwSnippets_snip#RunExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/RunSnippetsExample.xaml#runexample1)]  
  
 **Remarque :** à partir de la [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)], le <xref:System.Windows.Documents.Run.Text%2A> propriété de la <xref:System.Windows.Documents.Run> objet est une propriété de dépendance. Vous pouvez lier le <xref:System.Windows.Documents.Run.Text%2A> source de propriété à des données, par exemple un <xref:System.Windows.Controls.TextBlock>. Le <xref:System.Windows.Documents.Run.Text%2A> propriété prend entièrement en charge la liaison unidirectionnelle. Le <xref:System.Windows.Documents.Run.Text%2A> propriété prend également en charge la liaison bidirectionnelle, à l’exception de <xref:System.Windows.Controls.RichTextBox>. Pour obtenir un exemple, consultez <xref:System.Windows.Documents.Run.Text%2A?displayProperty=nameWithType>.  
  
 **Span**  
  
 <xref:System.Windows.Documents.Span> regroupe les autres éléments de contenu inline. Aucun rendu inhérent n’est appliqué au contenu dans un <xref:System.Windows.Documents.Span> élément. Toutefois, les éléments hérités de <xref:System.Windows.Documents.Span> notamment <xref:System.Windows.Documents.Hyperlink>, <xref:System.Windows.Documents.Bold>, <xref:System.Windows.Documents.Italic> et <xref:System.Windows.Documents.Underline> s’appliquent à la mise en forme de texte.  
  
 Voici un exemple d’un <xref:System.Windows.Documents.Span> est utilisé pour contenir du contenu inline comprenant du texte, un <xref:System.Windows.Documents.Bold> élément et un <xref:System.Windows.Controls.Button>.  
  
 [!code-xaml[FlowOvwSnippets_snip#SpanExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SpanExample.xaml#spanexamplewholepage)]  
  
 La capture d’écran suivante montre le rendu de cet exemple.  
  
 ![Capture d’écran : exemple d’affichage de Span](../../../../docs/framework/wpf/advanced/media/flow-spanexample.gif "Flow_SpanExample")  
  
 **InlineUIContainer**  
  
 <xref:System.Windows.Documents.InlineUIContainer> permet de <xref:System.Windows.UIElement> éléments (par exemple, un contrôle tel que <xref:System.Windows.Controls.Button>) à incorporer dans un <xref:System.Windows.Documents.Inline> élément de contenu. Cet élément est l’équivalent inline <xref:System.Windows.Documents.BlockUIContainer> décrit ci-dessus. Voici un exemple qui utilise <xref:System.Windows.Documents.InlineUIContainer> pour insérer un <xref:System.Windows.Controls.Button> inline dans un <xref:System.Windows.Documents.Paragraph>.  
  
 [!code-xaml[FlowOvwSnippets_snip#InlineUIContainerExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/InlineUIContainerExample.xaml#inlineuicontainerexamplewholepage)]  
  
 [!code-csharp[FlowOvwSnippets_procedural_snip#InlineUIContainerCodeOnlyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/InlineUIContainerExample.cs#inlineuicontainercodeonlyexamplewholepage)]
 [!code-vb[FlowOvwSnippets_procedural_snip#InlineUIContainerCodeOnlyExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/InlineUIContainerExample.vb#inlineuicontainercodeonlyexamplewholepage)]  
  
 **Remarque :** <xref:System.Windows.Documents.InlineUIContainer> ne doivent pas être utilisés de manière explicite dans le balisage. Si vous l’omettez, un <xref:System.Windows.Documents.InlineUIContainer> est créé quand même lorsque le code est compilé.  
  
 **Figure et Floater**  
  
 <xref:System.Windows.Documents.Figure> et <xref:System.Windows.Documents.Floater> sont utilisés pour incorporer le contenu dans les Documents dynamiques avec les propriétés de positionnement qui peuvent être personnalisées indépendamment du flux de contenu principal. <xref:System.Windows.Documents.Figure> ou <xref:System.Windows.Documents.Floater> éléments sont souvent utilisés pour mettre en surbrillance ou accentuer des parties de contenu, héberger des images ou autres contenus dans le flux de contenu principal ou injecter du contenu tels que des publications lié.  
  
 L’exemple suivant montre comment incorporer un <xref:System.Windows.Documents.Figure> dans un paragraphe de texte.  
  
 [!code-xaml[FlowOvwSnippets_snip#FigureExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/FigureExample.xaml#figureexamplewholepage)]  
  
 [!code-csharp[FlowOvwSnippets_procedural_snip#FigureCodeOnlyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/FigureExample.cs#figurecodeonlyexamplewholepage)]
 [!code-vb[FlowOvwSnippets_procedural_snip#FigureCodeOnlyExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/FigureExample.vb#figurecodeonlyexamplewholepage)]  
  
 L’illustration suivante montre le rendu de cet exemple.  
  
 ![Capture d’écran : exemple de figure](../../../../docs/framework/wpf/advanced/media/flow-ovw-figure-example.png "Flow_Ovw_Figure_Example")  
  
 <xref:System.Windows.Documents.Figure> et <xref:System.Windows.Documents.Floater> différentes et sont utilisés pour différents scénarios.  
  
 **Figure :**  
  
-   Positionnable : vous pouvez placer ses ancres horizontale et verticale de façon à l’ancrer par rapport à la page, au contenu, à la colonne ou au paragraphe. Vous pouvez également utiliser ses <xref:System.Windows.Documents.Figure.HorizontalOffset%2A> et <xref:System.Windows.Documents.Figure.VerticalOffset%2A> des propriétés pour spécifier des offsets arbitraires.  
  
-   Dimensionnable sur plusieurs colonnes : vous pouvez définir <xref:System.Windows.Documents.Figure> hauteur et la largeur à des multiples de page ou la largeur, hauteur de contenu ou de colonne. Notez que, dans les deux premiers cas, les multiples supérieurs à 1 ne sont pas autorisés. Par exemple, vous pouvez définir la largeur d’un <xref:System.Windows.Documents.Figure> pour être « page 0.5 » ou « contenu 0.25 » ou « colonne 2 ». Vous pouvez également définir des valeurs en pixels absolues pour la hauteur et la largeur.  
  
-   Non paginable : si le contenu à l’intérieur d’un <xref:System.Windows.Documents.Figure> ne tient pas dans le <xref:System.Windows.Documents.Figure>, il doit rendre le contenu ne tient pas et le reste du contenu est perdu  
  
 **Floater :**  
  
-   Non positionnable : cet élément s’affiche dans l’espace disponible, quel qu’il soit. Vous ne pouvez pas définir l’offset ou ancrer un <xref:System.Windows.Documents.Floater>.  
  
-   Ne peut pas être redimensionnée à plusieurs colonnes : par défaut, <xref:System.Windows.Documents.Floater> tailles sur une colonne. Il a un <xref:System.Windows.Documents.Floater.Width%2A> propriété qui peut être définie sur une valeur absolue en pixels, mais si cette valeur est supérieure à une largeur de colonne qu’il est ignoré et la palette est dimensionnée à une colonne. Vous pouvez la redimensionner à moins d’une colonne en définissant la largeur en pixels correcte, mais le dimensionnement n’est pas relatif à la colonne, donc « 0.5Column » n’est pas une expression valide pour <xref:System.Windows.Documents.Floater> largeur. <xref:System.Windows.Documents.Floater> n’a aucune propriété de hauteur et elle est la hauteur ne peut pas être définie, sa hauteur dépend du contenu  
  
-   <xref:System.Windows.Documents.Floater> pagine : si son contenu à la largeur spécifiée s’étend à la hauteur de colonne supérieure à 1, la palette s’arrête et pagine à la colonne suivante, de la page suivante, etc.  
  
 <xref:System.Windows.Documents.Figure> est un bon emplacement pour placer le contenu autonome où vous souhaitez contrôler la taille et de positionnement et êtes certain que le contenu ne puisse être à la taille spécifiée. <xref:System.Windows.Documents.Floater> est un bon emplacement de contenu plus libre semblable au contenu de la page principale, mais est séparé à partir de celui-ci.  
  
 **LineBreak**  
  
 <xref:System.Windows.Documents.LineBreak> provoque un saut de ligne dans le contenu de flux. L'exemple suivant montre l'utilisation de <xref:System.Windows.Documents.LineBreak>.  
  
 [!code-xaml[FlowOvwSnippets_snip#LineBreakExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/LineBreakExample.xaml#linebreakexamplewholepage)]  
  
 La capture d’écran suivante montre le rendu de cet exemple.  
  
 ![Capture d’écran : exemple de LineBreak](../../../../docs/framework/wpf/advanced/media/flow-ovw-linebreakexample.png "Flow_Ovw_LineBreakExample")  
  
### <a name="flow-collection-elements"></a>Éléments de collection de flux  
 Dans la plupart des exemples ci-dessus, le <xref:System.Windows.Documents.BlockCollection> et <xref:System.Windows.Documents.InlineCollection> sont utilisés pour construire le contenu de flux par programme. Par exemple, pour ajouter des éléments à un <xref:System.Windows.Documents.Paragraph>, vous pouvez utiliser la syntaxe :  
  
 `…`  
  
 `myParagraph.Inlines.Add(new Run("Some text"));`  
  
 `…`  
  
 Cette opération ajoute une <xref:System.Windows.Documents.Run> à la <xref:System.Windows.Documents.InlineCollection> de la <xref:System.Windows.Documents.Paragraph>.  Il est identique à implicite <xref:System.Windows.Documents.Run> trouvé à l’intérieur d’un <xref:System.Windows.Documents.Paragraph> dans le balisage :  
  
 `…`  
  
 `<Paragraph>`  
  
 `Some Text`  
  
 `</Paragraph>`  
  
 `…`  
  
 Comme un exemple d’utilisation de la <xref:System.Windows.Documents.BlockCollection>, l’exemple suivant crée un nouveau <xref:System.Windows.Documents.Section> , puis utilise le **ajouter** méthode pour ajouter un nouveau <xref:System.Windows.Documents.Paragraph> à la <xref:System.Windows.Documents.Section> contenu.  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksAdd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksadd)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksAdd](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksadd)]  
  
 En plus d’ajouter des éléments à une collection de flux, vous pouvez aussi en supprimer.  L’exemple suivant supprime le dernier <xref:System.Windows.Documents.Inline> élément dans le <xref:System.Windows.Documents.Span>.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesRemoveLast](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesremovelast)]
 [!code-vb[SpanSnippets#_SpanInlinesRemoveLast](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesremovelast)]  
  
 L’exemple suivant efface tout le contenu (<xref:System.Windows.Documents.Inline> éléments) à partir de la <xref:System.Windows.Documents.Span>.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesClear](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesclear)]
 [!code-vb[SpanSnippets#_SpanInlinesClear](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesclear)]  
  
 Quand vous utilisez du contenu dynamique par programmation, vous employez certainement très souvent ces collections.  
  
 Indique si un élément de flux utilise un <xref:System.Windows.Documents.InlineCollection> (incorporations) ou <xref:System.Windows.Documents.BlockCollection> (blocs) pour contenir ses enfants éléments dépend du type d’éléments enfants (<xref:System.Windows.Documents.Block> ou <xref:System.Windows.Documents.Inline>) peut être contenu par le parent. Les règles relatives à la relation contenant-contenu pour les éléments de contenu dynamique sont résumées dans le schéma du contenu présenté à la section suivante.  
  
 **Remarque :** il existe un troisième type de collection utilisée avec le contenu de flux, le <xref:System.Windows.Documents.ListItemCollection>, mais cette collection est utilisée uniquement avec un <xref:System.Windows.Documents.List>. En outre, il existe plusieurs collections utilisées avec <xref:System.Windows.Documents.Table>. Consultez [vue d’ensemble de la Table](../../../../docs/framework/wpf/advanced/table-overview.md) pour plus d’informations.  
  
<a name="content_schema"></a>   
## <a name="content-schema"></a>Schéma du contenu  
 Étant donné le nombre d’éléments de contenu dynamique, il est parfois difficile de savoir quel type d’éléments enfants peut être contenu dans un élément. Le diagramme suivant récapitule les règles relatives à la relation contenant-contenu pour les éléments de contenu dynamique. Les flèches représentent les relations parent/enfant possibles.  
  
 ![Diagramme : schéma de relation contenant-contenu pour le contenu dynamique](../../../../docs/framework/wpf/advanced/media/flow-content-schema.png "Flow_Content_Schema")  
  
 Comme le montre le diagramme ci-dessus, les enfants autorisés pour un élément ne sont pas nécessairement déterminés par le fait qu’il est un <xref:System.Windows.Documents.Block> élément ou un <xref:System.Windows.Documents.Inline> élément. Par exemple, un <xref:System.Windows.Documents.Span> (une <xref:System.Windows.Documents.Inline> élément) ne peut avoir <xref:System.Windows.Documents.Inline> des éléments enfants lors de l’un <xref:System.Windows.Documents.Figure> (également une <xref:System.Windows.Documents.Inline> élément) ne peut avoir <xref:System.Windows.Documents.Block> des éléments enfants. Un diagramme est donc utile pour déterminer rapidement quel élément peut être contenu dans un autre. Par exemple, utilisons le schéma pour déterminer comment construire le contenu dynamique d’un <xref:System.Windows.Controls.RichTextBox>.  
  
 **1.** A <xref:System.Windows.Controls.RichTextBox> doit contenir un <xref:System.Windows.Documents.FlowDocument> qui doit contenir un <xref:System.Windows.Documents.Block>-objet dérivé. Voici le segment correspondant extrait du diagramme ci-dessus.  
  
 ![Diagramme : règles relatives à la relation contenant-contenu pour RichTextBox](../../../../docs/framework/wpf/advanced/media/flow-ovw-schemawalkthrough1.png "Flow_Ovw_SchemaWalkThrough1")  
  
 À ce stade, le balisage peut ressembler à ceci.  
  
 [!code-xaml[FlowOvwSnippets_snip#SchemaWalkThrough1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/MiscSnippets.xaml#schemawalkthrough1)]  
  
 **2.** Selon le schéma, il y en a plusieurs <xref:System.Windows.Documents.Block> éléments, notamment <xref:System.Windows.Documents.Paragraph>, <xref:System.Windows.Documents.Section>, <xref:System.Windows.Documents.Table>, <xref:System.Windows.Documents.List>, et <xref:System.Windows.Documents.BlockUIContainer> (voir les classes dérivées de Block ci-dessus). Supposons que nous souhaitons un <xref:System.Windows.Documents.Table>. Le schéma ci-dessus, un <xref:System.Windows.Documents.Table> contient un <xref:System.Windows.Documents.TableRowGroup> contenant <xref:System.Windows.Documents.TableRow> éléments qui contiennent des <xref:System.Windows.Documents.TableCell> les éléments qui contiennent un <xref:System.Windows.Documents.Block>-objet dérivé. Voici le segment correspondant pour <xref:System.Windows.Documents.Table> extrait du schéma ci-dessus.  
  
 ![Diagramme : schéma parent&#47;enfant pour Table](../../../../docs/framework/wpf/advanced/media/flow-ovw-schemawalkthrough2.png "Flow_Ovw_SchemaWalkThrough2")  
  
 Le balisage correspondant est indiqué ci-dessous.  
  
 [!code-xaml[FlowOvwSnippets_snip#SchemaWalkThrough2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/MiscSnippets.xaml#schemawalkthrough2)]  
  
 **3.** Là encore, un ou plusieurs <xref:System.Windows.Documents.Block> éléments sont requis sous un <xref:System.Windows.Documents.TableCell>. Pour simplifier, insérons du texte dans la cellule. Nous pouvons faire cela à l’aide un <xref:System.Windows.Documents.Paragraph> avec un <xref:System.Windows.Documents.Run> élément. Voici les segments correspondants à partir du diagramme montrant qu’un <xref:System.Windows.Documents.Paragraph> peut prendre une <xref:System.Windows.Documents.Inline> élément et qu’un <xref:System.Windows.Documents.Run> (un <xref:System.Windows.Documents.Inline> élément) peut prendre uniquement en texte brut.  
  
 ![Diagramme : schéma parent&#47;enfant pour Paragraph](../../../../docs/framework/wpf/advanced/media/flow-ovw-schemawalkthrough3.png "Flow_Ovw_SchemaWalkThrough3")  
  
 ![Diagramme : schéma parent/enfant pour Run](../../../../docs/framework/wpf/advanced/media/flow-ovw-schemawalkthrough4.png "Flow_Ovw_SchemaWalkThrough4")  
  
 Le balisage de l’exemple complet est indiqué ci-dessous.  
  
 [!code-xaml[FlowOvwSnippets_snip#SchemaExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SchemaExample.xaml#schemaexamplewholepage)]  
  
<a name="customizing_text"></a>   
## <a name="customizing-text"></a>Personnalisation du texte  
 Généralement, le texte est le type de contenu le plus fréquent dans un document dynamique. Même si les objets décrits ci-dessus permettent de contrôler la plupart des aspects concernant la restitution du texte, il existe d’autres méthodes, décrites dans cette section, destinées à personnaliser le texte.  
  
### <a name="text-decorations"></a>Ornements de texte  
 Les ornements de texte vous permettent d’appliquer au texte les effets suivants : souligné, ligne au-dessus, ligne de base et barré (consultez les images ci-dessous). Ces ornements sont ajoutés à l’aide de la <xref:System.Windows.Documents.Inline.TextDecorations%2A> propriété qui est exposée par un nombre d’objets, y compris <xref:System.Windows.Documents.Inline>, <xref:System.Windows.Documents.Paragraph>, <xref:System.Windows.Controls.TextBlock>, et <xref:System.Windows.Controls.TextBox>.  
  
 L'exemple suivant montre comment définir la propriété <xref:System.Windows.Documents.Paragraph.TextDecorations%2A> d'un <xref:System.Windows.Documents.Paragraph>.  
  
 [!code-xaml[InlineSnippets#_Paragraph_TextDecXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InlineSnippets/CSharp/Window1.xaml#_paragraph_textdecxaml)]  
  
 [!code-csharp[InlineSnippets#_Paragraph_TextDec](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InlineSnippets/CSharp/Window1.xaml.cs#_paragraph_textdec)]
 [!code-vb[InlineSnippets#_Paragraph_TextDec](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InlineSnippets/visualbasic/window1.xaml.vb#_paragraph_textdec)]  
  
 La figure suivante montre le rendu de cet exemple.  
  
 ![Capture d’écran : texte avec effet barré par défaut](../../../../docs/framework/wpf/advanced/media/inline-textdec-strike.png "Inline_TextDec_Strike")  
  
 Les illustrations suivantes montrent comment les **surligné**, **base**, et **Underline** des ornements.  
  
 ![Capture d’écran : TextDecorator avec ligne au-dessus](../../../../docs/framework/wpf/advanced/media/inline-textdec-over.png "Inline_TextDec_Over")  
  
 ![Capture d’écran : effet de la ligne de base par défaut sur le texte](../../../../docs/framework/wpf/advanced/media/inline-textdec-base.png "Inline_TextDec_Base")  
  
 ![Capture d’écran : texte avec effet souligné par défaut](../../../../docs/framework/wpf/advanced/media/inline-textdec-under.png "Inline_TextDec_Under")  
  
### <a name="typography"></a>Typographie  
 Le <xref:System.Windows.Documents.TextElement.Typography%2A> est exposée par la plupart des liés au flux de contenu, y compris <xref:System.Windows.Documents.TextElement>, <xref:System.Windows.Documents.FlowDocument>, <xref:System.Windows.Controls.TextBlock>, et <xref:System.Windows.Controls.TextBox>. Cette propriété est utilisée pour contrôler les caractéristiques/variations typographiques de texte (en d’autres termes, petites ou grandes majuscules, exposants et indices, etc).  
  
 L’exemple suivant montre comment définir la <xref:System.Windows.Documents.TextElement.Typography%2A> d’attribut, à l’aide de <xref:System.Windows.Documents.Paragraph> en tant que l’élément de l’exemple.  
  
 [!code-xaml[TextElementSnippets#_TextElement_TypogXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextElementSnippets/CSharp/Window1.xaml#_textelement_typogxaml)]  
  
 La figure suivante montre le rendu de cet exemple.  
  
 ![Capture d’écran : texte avec typographie altérée](../../../../docs/framework/wpf/advanced/media/textelement-typog.png "TextElement_Typog")  
  
 Par contraste, l’illustration suivante montre comment s’affiche un exemple similaire avec des propriétés typographiques par défaut.  
  
 ![Capture d’écran : texte avec typographie altérée](../../../../docs/framework/wpf/advanced/media/textelement-typog-default.png "TextElement_Typog_Default")  
  
 L’exemple suivant montre comment définir le <xref:System.Windows.Controls.TextBox.Typography%2A> propriété par programmation.  
  
 [!code-csharp[TextElementSnippets#_TextElement_Typog](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextElementSnippets/CSharp/Window1.xaml.cs#_textelement_typog)]
 [!code-vb[TextElementSnippets#_TextElement_Typog](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextElementSnippets/visualbasic/window1.xaml.vb#_textelement_typog)]  
  
 Consultez [typographie dans WPF](../../../../docs/framework/wpf/advanced/typography-in-wpf.md) pour plus d’informations sur la typographie.  
  
## <a name="see-also"></a>Voir aussi  
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)  
 [Typographie dans WPF](../../../../docs/framework/wpf/advanced/typography-in-wpf.md)  
 [Rubriques de guide pratique](../../../../docs/framework/wpf/advanced/flow-content-elements-how-to-topics.md)  
 [Vue d'ensemble du modèle de contenu de TextElement](../../../../docs/framework/wpf/advanced/textelement-content-model-overview.md)  
 [Vue d’ensemble de RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)  
 [Documents dans WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)  
 [Vue d’ensemble de Table](../../../../docs/framework/wpf/advanced/table-overview.md)  
 [Vue d’ensemble des annotations](../../../../docs/framework/wpf/advanced/annotations-overview.md)
