---
title: 支持的 PrintTicket 功能
description: 本部分提供有关支持的标准 XPS 筛选器 PrintTicket 功能的信息。
ms.assetid: 6D1AD770-D4BA-4BDC-886A-C5C36A09BB0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3390095e14b175eb411bce8c4de07a490e727ed5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554256"
---
# <a name="supported-printticket-features"></a>支持的 PrintTicket 功能


本部分提供有关支持的标准 XPS 筛选器 PrintTicket 功能的信息。

所有这些功能有导致 XPS 筛选器来改变所生成的 PDL 命令的效果。 PDL 命令都由筛选器本身也由设备 GPD/PPD，这些功能仍会导致 XPS 筛选器，以改变 PDL 命令。 可以打印架构 (psk) 的关键字命名空间中找到的所有元素 （功能、 选项、 ScoredProperties、 参数） 的以下各节中引用。

## <a name="pagemediasize"></a>PageMediaSize


此功能描述用于打印输出媒体表的维度。 除了名称以外，每个选项可以包含两个评分属性：MediaSizeWidth 和 MediaSizeHeight。 这些过程描述媒体的物理大小。 支持的选项为带有相应 GPD/PPD 文件条目的任何选项。

为 PCL6/GPD，如果 PrintTicket 选项为 CustomMediaSize，然后 PageMediaSizeMediaSizeWith 和 PageMediaSizeMediaSizeHeight 参数用于获取媒体的维度。

对于 PostScript/PPD，如果 PrintTicket 选项为 PSCustomMediaSize 然后 PageMediaSizePSWith 和 PageMediaSizePSHeight 参数用于获取媒体的维度。 由 GPD PageSize 功能值指定为所选的媒体类型生成 PCL6。 以下列表显示 GPD 检查以确定要使用的 PageMediaSize 选项的顺序：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 PageMediaSize 选项的 name 属性。

2. 以下[默认 PageMediaSize 映射](default-pagemediasize-mappings.md)使用。

3. PageSize 选项的 name 属性匹配 GPD 中选项的名称。

在呈现过程中，筛选器将替换为 PhysPaperWidth 在任何 GPD 命令 MediaSizeWidth ScoredProperty 或 PageMediaSizeMediaSizeWidth 参数指定的纸张的宽度。

筛选器会还 PhysPaperLength 任何 GPD 命令中将替换为 MediaSizeHeight ScoredProperty 或 PageMediaSizeMediaSizeHeight 参数指定的纸张的长度。

为所选的媒体类型生成 PostScript PPD PageSize 功能由指定。 按以下顺序选择 PPD 中的使用选项：

1. 如果 MSPrintSchemaKeywordMap 指定，并且匹配 PageMediaSize 选项的 name 属性。

2. PageSize 选项的 name 属性匹配 PPD.中选项的名称

## <a name="pagemediatype"></a>PageMediaType


此功能描述媒体表可用于设备，如涂层处理、 媒体材料和媒体权重的特征。 支持的选项为任何与相应的 GPD/PPD 条目。

为所选的媒体类型生成 PCL6 GPD MediaType 功能由指定。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 PageMediaType 选项的 name 属性。

2. 使用以下默认映射：

| PageMediaType 值            | GPD/PPD 文件条目 |
|--------------------------------|--------------------|
| PrintTicket PhotographicGlossy | GPD 抛光         |
| PrintTicket 纯              | GPD 标准       |
| PrintTicket 透明度       | GPD 透明度   |

 

3. PageMediaType 选项的 name 属性匹配 GPD 中选项的名称。

为所选的媒体类型生成 PostScript PPD MediaType 功能由指定。 按以下顺序选择 PPD 中的使用选项：

1. 如果 MSPrintSchemaKeywordMap 指定，并且匹配 PageMediaType 选项的 name 属性。

2. PageMediaType 选项的 name 属性匹配 PPD.中选项的名称

## <a name="pagemediacolor"></a>PageMediaColor


此功能描述媒体表的颜色。 支持的选项为任何与相应的 GPD/PPD 条目。

为所选的媒体颜色由 GPD 功能指定生成 PCL6 包含\*PrintSchemaKeywordMap:"PageMediaColor"。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 PageMediaColor 选项的 name 属性。

2. PageMediaColor 选项的 name 属性匹配 GPD 中选项的名称。

为所选的媒体颜色生成 PostScript PPD MediaColor 功能由指定。 按以下顺序选择 PPD 中的使用选项：
1. 如果 MSPrintSchemaKeywordMap 指定，并且匹配 PageMediaColor 选项的 name 属性。

2. PageMediaColor 选项的 name 属性匹配 PPD.中选项的名称

## <a name="jobinputbin"></a>JobInputBin


此功能介绍到打印设备的输入的位置提取媒体的位置。 支持的选项为具有一个对应的 GPD/PPD 条目。

为所选的送纸器生成 PCL6 GPD InputBin 功能由指定。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 JobInputBin 选项的 name 属性。

2. 使用以下默认映射：

| JobInputBin value      | GPD/PPD 文件条目                  |
|------------------------|-------------------------------------|
| PrintTicket 盒式   | GPD 自动，磁带的一半，ENVFEED ENVMANUAL |
| PrintTicket 自动选择 | GPD FORMSOURCE                      |
| PrintTicket 高       | GPD LARGECAPACITY、 LARGEFMT，降低    |
| PrintTicket 手动     | GPD MANUAL,MIDDLE,SMALLFMT          |
| PrintTicket 牵引器送    | GPD 牵引上限                   |

 

3. PageMediaType 选项的 name 属性匹配 GPD 中选项的名称。

为所选的送纸器生成 PostScript PPD InputSlot 功能由指定。 按以下顺序选择 PPD 中的使用选项：
1. 如果 MSPrintSchemaKeywordMap 指定，并且匹配 JobInputBin 选项的 name 属性。

2. JobInputBin 选项的 name 属性匹配 PPD.中选项的名称

## <a name="pageorientation"></a>PageOrientation


此功能指示要从内容的坐标空间转换到工作表的媒体坐标空间时使用的旋转转换。 支持的选项为纵向、 横向、 ReversePortrait 和 ReverseLandscape。

为选定的方向生成 PCL6 指定 GPD 定向功能。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 PageOrientation 选项的 name 属性。

2. 使用以下默认映射：

| PageOrientation 值        | GPD/PPD 文件条目   |
|------------------------------|----------------------|
| PrintTicket 纵向         | GPD 纵向         |
| PrintTicket 横向        | GPD 横向\_CC90  |
| PrintTicket ReverseLandscape | GPD 横向\_CC270 |

 

3. PageOrientation 选项的 name 属性匹配 GPD 中选项的名称。

为选定的方向生成 PostScript 取决于筛选器。
## <a name="pageoutputcolor"></a>PageOutputColor


此功能控制目标文档页的打印输出的颜色特征 （颜色，单色）。 支持的选项为颜色、 灰度和单色。

为所选的输出颜色生成 PCL6 GPD ColorMode 功能由指定。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 PageOutputColor 选项的 name 属性。

2. PageOutputColor 选项的 name 属性匹配 GPD 中选项的名称。

为所选的输出颜色生成 PostScript 取决于筛选器。
## <a name="pageresolution"></a>PageResolution


此功能所定义的设备可以生成输出可用分辨率 （以每英寸点数为单位）。 打印架构未指定选项，此功能; 所有标准的名称但是，我们支持两个 ScoredProperties 而不考虑的选项名称：ResolutionX，和 ResolutionY。 支持的选项为任何与相应的 GPD/PPD 条目。

为所选解析生成 PCL6 指定 GPD 解析功能。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 PageResolution 选项的 name 属性。

2. PageResolution 选项的 name 属性匹配 GPD 中选项的名称。

在呈现期间，该筛选器将 GraphicsXRes 和 TextXRes 任何 GPD 命令中将替换为 ResolutionX 由指定的水平分辨率。
筛选器将还 GraphicsYRes 和 TextYRes 任何 GPD 命令中将替换为 ResolutionY 由指定的垂直分辨率。

为所选解析生成 PostScript 指定 PPD 解析或 JCLResolution 功能。 按以下顺序选择 PPD 中的使用选项：

1. 如果 MSPrintSchemaKeywordMap 指定，并且匹配 PageResolution 选项的 name 属性。

2. PageResolution 选项的 name 属性匹配 PPD.中选项的名称

## <a name="pageoutputquality"></a>PageOutputQuality


此功能所定义的文档页的打印质量。 支持的选项为具有一个对应的 GPD/PPD 条目。

为所选质量生成 PCL6 指定 PrintSchemaKeywordMap 值为 PageOutputQuality gpd 分析功能。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 PageOutputQuality 选项的 name 属性。

2. PageOutputQuality 选项的 name 属性匹配 GPD 中选项的名称。

为所选质量生成 PostScript PPD 功能以及 PageOutputQuality MSPrintSchemaKeywordMap 值指定。 按以下顺序选择 PPD 中的使用选项：
1. 如果 MSPrintSchemaKeywordMap 指定，并且匹配 PageOutputQuality 选项的 name 属性。

2. PageOutputQuality 选项的 name 属性匹配 PPD.中选项的名称

## <a name="jobcopiesalldocuments"></a>JobCopiesAllDocuments


此参数指定的输出中打印作业的所有文档的次数。

为所选副本生成 PCL6 取决于筛选器。 请参阅与此参数的交互的 JobCollateAllDocuments 功能。

为所选副本生成 PostScript 取决于筛选器。 请参阅与此参数的交互的 JobCollateAllDocuments 功能。

## <a name="documentcopiesallpages"></a>DocumentCopiesAllPages


此参数指定页副本应在输出中打印作业关联的文档的数。

为所选副本生成 PCL6 取决于筛选器。 请参阅与此参数的交互的 DocumentCollate 功能。

为所选副本生成 PostScript 取决于筛选器。 请参阅与此参数的交互的 DocumentCollate 功能。

## <a name="pagecopies"></a>PageCopies


此参数指定文档内的各个源文档页的副本数量应输出。 由于副本计数仅适用于当前页没有任何排序规则。

为所选副本生成 PCL6 取决于筛选器。

为所选副本生成 PostScript 取决于筛选器。

## <a name="documentcollate"></a>DocumentCollate


此功能在打印输出中指定的打印作业中关联的文档页的显示的顺序。 受支持的选项包括逐份打印和未逐份打印。

为所选的排序规则生成 PCL6 指定 GPD 逐份打印功能。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 DocumentCollate 选项的 name 属性。

2. 使用以下默认映射：

| DocumentCollate 值  | GPD/PPD 文件条目 |
|------------------------|--------------------|
| PrintTicket 非逐份打印 | 关闭 GPD            |
| PrintTicket 逐份打印   | GPD 上             |

 

3. DocumentCollate 选项的 name 属性匹配 GPD 中选项的名称。

**请注意**  时 DocumentCollate 设置为逐份打印并且 GPD 逐份打印选项包含一个命令，则假定设备可以生成已设置排序规则的副本。 *XPS.PCL6*筛选器将仅生成 1 份作业并使用 GPD 命令来指示设备来生成已设置排序规则的副本。 筛选器然后替换 NumOfCopies GPD 命令中指定的 JobCopiesAllDocuments 的份数。

 

为所选的排序规则生成 PostScript 指定 PPD 逐份打印功能。 按以下顺序选择 PPD 中的使用选项：
1. 如果 MSPrintSchemaKeywordMap 指定，并且匹配 DocumentCollate 选项的 name 属性。

2. 使用以下默认映射：

| DocumentCollate 值  | GPD/PPD 文件条目 |
|------------------------|--------------------|
| PrintTicket 非逐份打印 | PPD False          |
| PrintTicket 逐份打印   | PPD True           |

 

3. DocumentCollate 选项的 name 属性匹配 PPD.中选项的名称

**请注意**  时 DocumentCollate 设置为逐份打印和 PPD 包含逐份打印功能或功能，这是关键字映射到 DocumentCollate，则假定设备可以生成已设置排序规则的副本。 XPS.PS 筛选器仅将生成 1 份作业并使用 PPD 命令来指示设备来生成已设置排序规则的副本。

 

## <a name="jobduplexalldocumentscontiguously"></a>JobDuplexAllDocumentsContiguously


此功能指定打印作业而无需考虑文档边界的双面打印。 如果指定双面打印，则所有页面的打印作业中的所有文档都是双工而无需插入文档之间的空白页连续打印。 支持的选项为 OneSided、 TwoSidedShortEdge 和 TwoSidedLongEdge。

为所选双工生成 PCL6 GPD 双工功能由指定。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 JobDuplexAllDocumentsContiguously 选项的 name 属性。

2. 使用以下默认映射：

| JobDuplexAllDocumentsContiguously value | GPD/PPD 文件条目 |
|-----------------------------------------|--------------------|
| PrintTicket OneSided                    | GPD NONE           |
| PrintTicket TwoSidedShortEdge           | GPD 水平     |
| PrintTicket TwoSidedLongEdge            | GPD 垂直       |

 

3. JobDuplexAllDocumentsContiguously 选项的 name 属性匹配 GPD 中选项的名称。

为所选双工生成 PostScript 指定 PPD 中使用的选项选择按以下顺序 PPD 双工功能：
1. 如果 MSPrintSchemaKeywordMap 指定，并且匹配 JobDuplexAllDocumentsContiguously 选项的 name 属性。

2. 使用以下默认映射：

| JobDuplexAllDocumentsContiguously value | GPD/PPD 文件条目 |
|-----------------------------------------|--------------------|
| PrintTicket OneSided                    | PPD None           |
| PrintTicket TwoSidedShortEdge           | PPD DuplexTumble   |
| PrintTicket TwoSidedLongEdge            | PPD DuplexNoTumble |

 

3. JobDuplexAllDocumentsContiguously 选项的 name 属性匹配 PPD.中选项的名称

## <a name="documentduplex"></a>DocumentDuplex


此功能控制双面打印的打印作业中关联的文档。 如果指定此选项，将从前方的媒体的新工作表开始打印的输出。 支持的选项为 OneSided、 TwoSidedShortEdge 和 TwoSidedLongEdge。

为所选双工生成 PCL6 GPD 双工功能由指定。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 DocumentDuplex 选项的 name 属性。

2. 使用以下默认映射：

| DocumentDuplex value          | GPD/PPD 文件条目 |
|-------------------------------|--------------------|
| PrintTicket OneSided          | GPD NONE           |
| PrintTicket TwoSidedShortEdge | GPD 水平     |
| PrintTicket TwoSidedLongEdge  | GPD 垂直       |

 

3. DocumentDuplex 选项的 name 属性匹配 GPD 中选项的名称。

为所选双工生成 PostScript PPD 双工功能由指定。 按以下顺序选择 PPD 中的使用选项：
1. 如果 MSPrintSchemaKeywordMap 指定，并且匹配 DocumentDuplex 选项的 name 属性。

2. 使用以下默认映射：

| DocumentDuplex value          | GPD/PPD 文件条目 |
|-------------------------------|--------------------|
| PrintTicket OneSided          | PPD None           |
| PrintTicket TwoSidedShortEdge | PPD DuplexTumble   |
| PrintTicket TwoSidedLongEdge  | PPD DuplexNoTumble |

 

3. DocumentDuplex 选项的 name 属性匹配 PPD.中选项的名称

## <a name="documentnup"></a>DocumentNUp


此功能指定多个页面的内容应打印到的物理介质的每个工作表上。 而应在一种不同的文档中的内容不会打印到的同一个表上的方法中完成打印。 打印架构规范未指定此选项; 的名称但是选项支持指定将放在物理介质的一侧的页面数的 ScoredProperty 和 PagesPerSheet 值。 PagesPerSheet 的支持的值为 1、 2、 4、 6、 8、 9、 12、 16、 25 和 32 与物理页方向旋转为 2、 6、 8、 12 和 32。

为所选的每张生成 PCL6 取决于筛选器。

为所选的每张生成 PostScript 取决于筛选器。

**JobOutputBin**

此功能已打印后其中存放媒体在打印设备上描述的位置。 支持的选项为具有一个对应的 GPD/PPD 条目。

为所选的输出 bin 生成 PCL6 GPD OutputBin 功能由指定。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定且与相匹配的 name 属性\[作业 |文档 |页\]OutputBin 选项。

2. Name 属性\[作业 |文档 |页\]OutputBin 选项与 GPD 中选项的名称相匹配。

为所选双工生成 PostScript PPD OutputBin 功能由指定。 按以下顺序选择 PPD 中的使用选项：
1. 如果 MSPrintSchemaKeywordMap 指定且与相匹配的 name 属性\[作业 |文档 |页\]OutputBin 选项。

2. Name 属性\[作业 |文档 |页\]OutputBin 选项与 PPD.中选项的名称相匹配

## <a name="jobbindalldocuments"></a>JobBindAllDocuments


此功能介绍中打印作业已打印的纸张的绑定的方法。 打印作业中的所有文档应都绑定到一起。 支持的选项包括：None、 BindBottom、 BindLeft、 BindRight、 BindTop、 手册、 EdgeStitchBottom、 EdgeStitchLeft、 EdgeStitchRight 和 EdgeStitchTop。

选择手册时筛选器输出的格式为 2 向上使用的页重新排序，以便一半页面折叠表的作业的堆栈时的一本书的正确顺序。

当 BindingGutter ScoredProperty 指定手册时，筛选器强制实施至少 JobBindAllDocumentsGutter 参数指定的一样大的中心边距 （从缩放的可打印区域的边缘到纸张的中心）。

当为 BindLeft，指定 BindingGutter ScoredProperty 或 EdgeStitchLeft 筛选器将在工作表的正面 JobBindAllDocumentsGutter 参数指定的右移。 将剪切内容现在超出了可打印区域的右侧。 在工作表的后端上的内容将剪辑 JobBindAllDocumentsGutter 参数指定的右边缘上。

BindTop 指定 BindingGutter ScoredProperty，EdgeStitchTop 筛选器会转而底部 JobBindAllDocumentsGutter 参数指定的表的前端和后端方面的内容。 将剪切内容现在超出了可打印区域的底部。

当为 BindRight 指定 BindingGutter ScoredProperty 或 EdgeStitchRight 筛选器剪辑内容右侧 JobBindAllDocumentsGutter 参数指定的表的前端。 在工作表的后端上的内容将转移到 JobBindAllDocumentsGutter 参数指定的左侧。 将剪切内容现在超出了可打印区域的左侧。

BindingGutter ScoredProperty 指定 BindBottom 或 EdgeStitchBottom，筛选器会转而前端和后端的两面顶部附近的 JobBindAllDocumentsGutter 参数指定的表的内容。 将剪切内容现在超出了可打印区域的顶部。

**请注意**  绑定 edge 是基于作业中的第一个文档的第一页的方向将指定的边缘。 对于所有其他选项，将忽略 BindingGutter。

 

如果 GPD 文件未指定所选的选项的命令，为所选的绑定生成 PCL6 由筛选器。

如果 PPD 文件未指定所选的选项是调用命令，为所选的绑定生成 PostScript 由筛选器。

## <a name="documentbinding"></a>DocumentBinding


此功能介绍中打印作业的绑定关联的文档的打印工作表时要使用的方法。 文档中的所有页面应都绑定到一起。 支持的选项包括：None、 BindBottom、 BindLeft、 BindRight、 BindTop、 手册、 EdgeStitchBottom、 EdgeStitchLeft、 EdgeStitchRight 和 EdgeStitchTop。

选择手册时您将筛选器输出的格式为 2 向上使用的页重新排序，以便一半页面时的工作表文档堆栈折叠的一本书的正确顺序。

当 BindingGutter ScoredProperty 指定手册时，筛选器强制实施至少 DocumentBindingGutter 参数指定的一样大的中心边距 （从缩放的可打印区域的边缘到纸张的中心）。

为 BindLeft 或 EdgeStitchLeft 指定 BindingGutter ScoredProperty 筛选器会转而工作表的正面 DocumentBindingGutter 参数指定的右侧。 将剪切内容现在超出了可打印区域的右侧。 在工作表的后端上的内容将剪辑 DocumentBindingGutter 参数指定的右边缘上。

BindingGutter ScoredProperty 指定 BindTop 或 EdgeStitchTop，筛选器会转而底部 DocumentBindingGutter 参数指定的表的前端和后端方面的内容。 将剪切内容现在超出了可打印区域的底部。

当为 BindRight 指定 BindingGutter ScoredProperty 或 EdgeStitchRight 筛选器将右侧 DocumentBindingGutter 参数指定的表的前端上的剪辑内容。 在工作表的后端上的内容将转移到 DocumentBindingGutter 参数指定的左侧。 将剪切内容现在超出了可打印区域的左侧。

BindingGutter ScoredProperty 指定 BindBottom 或 EdgeStitchBottom，筛选器会转而前端和后端的两面顶部附近的 DocumentBindingGutter 参数指定的表的内容。 将剪切内容现在超出了可打印区域的顶部。

**请注意**  绑定 edge 是基于文档的第一页的方向将指定的边缘。 对于所有其他选项，将忽略 BindingGutter。

 

如果 GPD 文件未指定所选的选项的命令，为所选的绑定生成 PCL6 由筛选器。

如果 PPD 文件未指定所选的选项是调用命令，为所选的绑定生成 PostScript 由筛选器。

## <a name="jobstaplealldocuments"></a>JobStapleAllDocuments


此功能介绍中打印作业已打印的纸张的装订时要使用的方法。 作业中的所有文档应一起都装订。 支持的选项为任何与相应的 GPD/PPD 条目。

为所选的装订生成 PCL6 指定 GPD 处装订功能。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 JobStapleAllDocuments 选项的 name 属性。

2. JobStapleAllDocuments 选项的 name 属性匹配 GPD 中选项的名称。

为所选的装订生成 PostScript PPD 功能以及 JobStapleAllDocuments 或 DocumentStaple MSPrintSchemaKeywordMap 值指定。 按以下顺序选择 PPD 中的使用选项：
1. 如果 MSPrintSchemaKeywordMap 指定，并且匹配 JobStapleAllDocuments 选项的 name 属性。

2. JobStapleAllDocuments 选项的 name 属性匹配 PPD.中选项的名称

## <a name="jobholepunch"></a>JobHolePunch


此功能介绍的方法时要使用打孔打印作业中打印的纸张。 作业中的所有文档应都为打孔在一起。 支持的选项为任何与相应的 GPD/PPD 条目。

为所选的打孔生成 PCL6 指定 PrintSchemaKeywordMap 值为 JobHolePunch 或 DocumentHolePunch gpd 分析功能。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 JobHolePunch 选项的 name 属性。

2. JobHolePunch 选项的 name 属性匹配 GPD 中选项的名称。

为所选的打孔生成 PostScript PPD 功能以及 JobHolePunch 或 DocumentHolePunch MSPrintSchemaKeywordMap 值指定。 按以下顺序选择 PPD 中的使用选项：
1. 如果 MSPrintSchemaKeywordMap 指定，并且匹配 JobHolePunch 选项的 name 属性。

2. JobHolePunch 选项的 name 属性匹配 PPD.中选项的名称

## <a name="documentholepunch"></a>DocumentHolePunch


此功能介绍的方法时要使用的打印作业中关联的文档已打印的纸张打孔。 文档中的所有页面应都进行打孔在一起。 支持的选项为任何与相应的 GPD/PPD 条目。

为所选的打孔生成 PCL6 指定 PrintSchemaKeywordMap 值为 JobHolePunch 或 DocumentHolePunch gpd 分析功能。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 DocumentHolePunch 选项的 name 属性。

2. DocumentHolePunch 选项的 name 属性匹配 GPD 中选项的名称。

为所选的打孔生成 PostScript PPD 功能以及 JobHolePunch 或 DocumentHolePunch MSPrintSchemaKeywordMap 值指定。 按以下顺序选择 PPD 中的使用选项：
1. 如果 MSPrintSchemaKeywordMap 指定，并且匹配 DocumentHolePunch 选项的 name 属性。

2. DocumentHolePunch 选项的 name 属性匹配 PPD.中选项的名称

## <a name="pagemirrorimage"></a>PageMirrorImage


此功能指定的页面内容应进行镜像。 支持的选项为 None 和 MirrorImageWidth。

为所选镜像生成 PCL6 指定 PrintSchemaKeywordMap 值为 PageMirrorImage gpd 分析功能。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 PageMirrorImage 选项的 name 属性。

2. PageMirrorImage 选项的 name 属性匹配 GPD 中选项的名称。

为所选镜像生成 PostScript PPD MirrorPrint 功能由指定。 按以下顺序选择 PPD 中的使用选项：
1. 如果 MSPrintSchemaKeywordMap 指定，并且匹配 PageMirrorImage 选项的 name 属性。

2. 使用以下默认映射：

| PageMirrorImage 值        | GPD/PPD 文件条目 |
|------------------------------|--------------------|
| PrintTicket None             | PPD False          |
| PrintTicket MirrorImageWidth | PPD True           |

 

3. PageMirrorImage 选项的 name 属性匹配 PPD.中选项的名称

## <a name="pagenegativeimage"></a>PageNegativeImage


此功能指定的页面内容应为底片图像。 支持的选项包括无，并为负。

为所选的负打印生成 PCL6 指定 PrintSchemaKeywordMap 值为 PageNegativeImage gpd 分析功能。 按以下顺序选择 GPD 中的使用选项：

1. 如果 PrintSchemaKeywordMap 指定，并且匹配 PageNegativeImage 选项的 name 属性。

2. PageNegativeImage 选项的 name 属性匹配 GPD 中选项的名称。

为所选的负打印生成 PostScript PPD NegativePrint 功能由指定。 按以下顺序选择 PPD 中的使用选项：
1. 如果 MSPrintSchemaKeywordMap 指定，并且匹配 PageNegativeImage 选项的 name 属性。

2. 使用以下默认映射：

| PageNegativeImage value | GPD/PPD 文件条目 |
|-------------------------|--------------------|
| PrintTicket None        | PPD False          |
| PrintTicket 负    | PPD True           |

 

3. PageNegativeImage 选项的 name 属性匹配 PPD.中选项的名称

## <a name="related-topics"></a>相关主题

[默认 PageMediaSize 映射](default-pagemediasize-mappings.md)  

[标准 XPS 筛选器](standard-xps-filters.md)  

打印架构规范可以在此处下载：

[打印架构规范 1.1](http://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/print-schema-spec-1-1.zip)

[打印架构规范 2.0](http://download.microsoft.com/download/d/e/c/deca6e6b-3e81-48e7-b7ef-6d92a547d03c/print-schema-spec-2-0.zip)


