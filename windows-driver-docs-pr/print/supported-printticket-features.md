---
title: 支持的 PrintTicket 功能
description: 本部分提供有关标准 XPS 筛选器支持的 PrintTicket 功能的信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca84e44ae7595a70e659e70867625eb79d9df381
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806821"
---
# <a name="supported-printticket-features"></a>支持的 PrintTicket 功能

本部分提供有关标准 XPS 筛选器支持的 PrintTicket 功能的信息。

所有这些功能都可以使 XPS 筛选器改变生成的 PDL 命令。 无论 PDL 命令是由筛选器本身生成还是由设备 GPD/PPD 指定，这些功能仍会导致 XPS 筛选器改变 PDL 命令。 以下各节中引用的所有元素 (功能、选项、ScoredProperties、参数) 可在打印架构关键字 (psk) 命名空间中找到。

## <a name="pagemediasize"></a>PageMediaSize

此功能描述用于打印输出的媒体表的尺寸。 除了名称，每个选项还可以包含两个评分属性： MediaSizeWidth 和 MediaSizeHeight。 它们描述媒体的物理大小。 支持的选项是包含相应 GPD/PPD 文件项的任何选项。

对于 PCL6/GPD，如果 PrintTicket 选项为 CustomMediaSize，则使用 PageMediaSizeMediaSizeWith 和 PageMediaSizeMediaSizeHeight 参数获取媒体的尺寸。

对于 PostScript/PPD，如果 PrintTicket 选项为 PSCustomMediaSize，则使用 PageMediaSizePSWith 和 PageMediaSizePSHeight 参数获取介质的尺寸。 为所选媒体类型生成的 PCL6 由 GPD PageSize 功能值指定。 以下列表显示了检查 GPD 以确定要使用的 PageMediaSize 选项的顺序：

1. 如果指定了 PrintSchemaKeywordMap 并且与 PageMediaSize 选项的 name 属性匹配，则为。

1. 使用以下 [默认 PageMediaSize 映射](default-pagemediasize-mappings.md) 。

1. PageSize 选项的 name 属性与 GPD 中选项的名称相匹配。

在呈现过程中，筛选器会将任何 GPD 命令中的 PhysPaperWidth 替换为 MediaSizeWidth ScoredProperty 或 PageMediaSizeMediaSizeWidth 参数指定的纸张宽度。

筛选器还会将任何 GPD 命令中的 PhysPaperLength 替换为 MediaSizeHeight ScoredProperty 或 PageMediaSizeMediaSizeHeight 参数指定的纸张长度。

为所选媒体类型生成的 PostScript 由 PPD PageSize 功能指定。 将按以下顺序选择使用 PPD 中的选项：

1. 如果指定了 MSPrintSchemaKeywordMap 并且与 PageMediaSize 选项的 name 属性匹配，则为。

1. PageSize 选项的 name 属性与 PPD 中选项的名称相匹配。

## <a name="pagemediatype"></a>PageMediaType

此功能描述了可用于设备的媒体表的特征，例如 coatings、媒体材料和媒体重量。 支持的选项有对应的 GPD/PPD 条目。

为所选媒体类型生成的 PCL6 由 GPD 媒体类型功能指定。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 PageMediaType 选项的 name 属性匹配，则为。

1. 使用以下默认映射：

    | PageMediaType 值            | GPD/PPD 文件输入 |
    |--------------------------------|--------------------|
    | PrintTicket PhotographicGlossy | GPD 光泽         |
    | PrintTicket 普通              | GPD 标准       |
    | PrintTicket 透明度       | GPD 透明度   |

1. PageMediaType 选项的 name 属性与 GPD 中选项的名称相匹配。

为所选媒体类型生成的 PostScript 由 PPD 媒体类型功能指定。 将按以下顺序选择使用 PPD 中的选项：

1. 如果指定了 MSPrintSchemaKeywordMap 并且与 PageMediaType 选项的 name 属性匹配，则为。

1. PageMediaType 选项的 name 属性与 PPD 中选项的名称相匹配。

## <a name="pagemediacolor"></a>PageMediaColor

此功能描述介质工作表的颜色。 支持的选项有对应的 GPD/PPD 条目。

为所选媒体颜色生成的 PCL6 由包含 \* PrintSchemaKeywordMap： "PageMediaColor" 的 GPD 功能指定。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 PageMediaColor 选项的 name 属性匹配，则为。

1. PageMediaColor 选项的 name 属性与 GPD 中选项的名称相匹配。

为所选媒体颜色生成的 PostScript 是通过 PPD MediaColor 功能指定的。 将按以下顺序选择使用 PPD 中的选项：

1. 如果指定了 MSPrintSchemaKeywordMap 并且与 PageMediaColor 选项的 name 属性匹配，则为。

1. PageMediaColor 选项的 name 属性与 PPD 中选项的名称相匹配。

## <a name="jobinputbin"></a>JobInputBin

此功能描述了将媒体拉入打印设备的输入位置。 支持的选项为具有相应 GPD/PPD 条目的选项。

为选定输入送纸器生成的 PCL6 由 GPD InputBin 功能指定。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 JobInputBin 选项的 name 属性匹配，则为。

1. 使用以下默认映射：

    | JobInputBin 值      | GPD/PPD 文件输入                  |
    |------------------------|-------------------------------------|
    | PrintTicket 卡带   | GPD AUTO、卡带、ENVFEED、ENVMANUAL |
    | PrintTicket 自动 | GPD FORMSOURCE                      |
    | PrintTicket 高       | GPD LARGECAPACITY、LARGEFMT、LOWER    |
    | PrintTicket 手册     | GPD MANUAL，中间，SMALLFMT          |
    | PrintTicket 牵引车    | GPD 牵引车，上部                   |

1. PageMediaType 选项的 name 属性与 GPD 中选项的名称相匹配。

为选定输入送纸器生成的 PostScript 由 PPD InputSlot 功能指定。 将按以下顺序选择使用 PPD 中的选项：

1. 如果指定了 MSPrintSchemaKeywordMap 并且与 JobInputBin 选项的 name 属性匹配，则为。

1. JobInputBin 选项的 name 属性与 PPD 中选项的名称相匹配。

## <a name="pageorientation"></a>PageOrientation

此功能指示从内容坐标空间转换到工作表的媒体坐标空间时要使用的旋转转换。 支持的选项包括纵向、横向、ReversePortrait 和 ReverseLandscape。

为选定方向生成的 PCL6 由 "GPD 方向" 功能指定。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 PageOrientation 选项的 name 属性匹配，则为。

1. 使用以下默认映射：

    | PageOrientation 值        | GPD/PPD 文件输入   |
    |------------------------------|----------------------|
    | PrintTicket 纵向         | GPD 纵向         |
    | PrintTicket 横向        | GPD 横向 \_ CC90  |
    | PrintTicket ReverseLandscape | GPD 横向 \_ cc 1。0 |

1. PageOrientation 选项的 name 属性与 GPD 中选项的名称相匹配。

为选定方向生成的 PostScript 由筛选器决定。

## <a name="pageoutputcolor"></a>PageOutputColor

此功能控制 "目标文档" 页打印输出 (颜色、单色) 的颜色特征。 支持的选项为彩色、灰度和单色。

为所选输出颜色生成的 PCL6 由 GPD ColorMode 特性指定。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 PageOutputColor 选项的 name 属性匹配，则为。

1. PageOutputColor 选项的 name 属性与 GPD 中选项的名称相匹配。

为所选输出颜色生成的 PostScript 由筛选器决定。

## <a name="pageresolution"></a>PageResolution

此功能定义了可用的分辨率 (以每英寸点数为单位的) ，设备可以生成输出。 打印架构未为此功能的选项指定任何标准名称;但是，无论选项名称是什么，我们都支持两个 ScoredProperties： ResolutionX 和 ResolutionY。 支持的选项有对应的 GPD/PPD 条目。

为所选解析生成的 PCL6 由 GPD 分辨率功能指定。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 PageResolution 选项的 name 属性匹配，则为。

1. PageResolution 选项的 name 属性与 GPD 中选项的名称相匹配。

在呈现期间，筛选器会将任何 GPD 命令中的 GraphicsXRes 和 TextXRes 替换为 ResolutionX 指定的水平分辨率。
筛选器还会将任何 GPD 命令中的 GraphicsYRes 和 TextYRes 替换为 ResolutionY 指定的垂直分辨率。

为所选解决方案生成的 PostScript 是通过 PPD 分辨率或 JCLResolution 功能指定的。 将按以下顺序选择使用 PPD 中的选项：

1. 如果指定了 MSPrintSchemaKeywordMap 并且与 PageResolution 选项的 name 属性匹配，则为。

1. PageResolution 选项的 name 属性与 PPD 中选项的名称相匹配。

## <a name="pageoutputquality"></a>PageOutputQuality

此功能定义文档页面的打印质量。 支持的选项为具有相应 GPD/PPD 条目的选项。

为所选质量生成的 PCL6 由 GPD 功能指定，PrintSchemaKeywordMap 值为 PageOutputQuality。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 PageOutputQuality 选项的 name 属性匹配，则为。

1. PageOutputQuality 选项的 name 属性与 GPD 中选项的名称相匹配。

为所选质量生成的 PostScript 是通过 MSPrintSchemaKeywordMap 值为 PageOutputQuality 的 PPD 功能指定的。 将按以下顺序选择使用 PPD 中的选项：

1. 如果指定了 MSPrintSchemaKeywordMap 并且与 PageOutputQuality 选项的 name 属性匹配，则为。

1. PageOutputQuality 选项的 name 属性与 PPD 中选项的名称相匹配。

## <a name="jobcopiesalldocuments"></a>JobCopiesAllDocuments

此参数指定打印作业中的所有文档输出的次数。

为选定副本生成的 PCL6 由筛选器决定。 请参阅 JobCollateAllDocuments 功能以与此参数交互。

为选定副本生成的 PostScript 由筛选器决定。 请参阅 JobCollateAllDocuments 功能以与此参数交互。

## <a name="documentcopiesallpages"></a>DocumentCopiesAllPages

此参数指定打印作业中的关联文档应输出的页面副本数。

为选定副本生成的 PCL6 由筛选器决定。 请参阅 DocumentCollate 功能以与此参数交互。

为选定副本生成的 PostScript 由筛选器决定。 请参阅 DocumentCollate 功能以与此参数交互。

## <a name="pagecopies"></a>PageCopies

此参数指定文档内单个源文档页的副本数。 由于复制计数仅适用于当前页面，因此没有排序规则。

为选定副本生成的 PCL6 由筛选器决定。

为选定副本生成的 PostScript 由筛选器决定。

## <a name="documentcollate"></a>DocumentCollate

此功能指定打印作业中关联文档的页面在打印输出中的显示顺序。 支持的选项逐份打印和逐份打印。

为所选排序规则生成的 PCL6 由 "GPD 排序" 功能指定。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 DocumentCollate 选项的 name 属性匹配，则为。

1. 使用以下默认映射：

    | DocumentCollate 值  | GPD/PPD 文件输入 |
    |------------------------|--------------------|
    | PrintTicket | 关闭 GPD            |
    | PrintTicket 排序   | GPD             |

1. DocumentCollate 选项的 name 属性与 GPD 中选项的名称相匹配。

> [!NOTE]
> 如果将 DocumentCollate 设置为逐份打印并且 GPD Collate 选项包含一个命令，则假定设备可以生成逐份打印的副本。 *PCL6* 筛选器将仅生成作业的1个副本，并使用 GPD 命令指示设备生成逐份打印副本。 然后，筛选器会将 GPD 命令中的 NumOfCopies 替换为 JobCopiesAllDocuments 指定的副本数。

为所选排序规则生成的 PostScript 由 PPD 逐份打印功能指定。 将按以下顺序选择使用 PPD 中的选项：

1. 如果指定了 MSPrintSchemaKeywordMap 并且与 DocumentCollate 选项的 name 属性匹配，则为。

1. 使用以下默认映射：

    | DocumentCollate 值  | GPD/PPD 文件输入 |
    |------------------------|--------------------|
    | PrintTicket | PPD False          |
    | PrintTicket 排序   | PPD True           |

1. DocumentCollate 选项的 name 属性与 PPD 中选项的名称相匹配。

> [!NOTE]
> 当 DocumentCollate 设置为逐份打印并且 PPD 包含逐份打印功能或映射到 DocumentCollate 的关键字时，假定设备可以生成逐份打印副本。 XPS.PS 筛选器将仅生成作业的1个副本，并使用 PPD 命令指示设备生成逐份打印副本。

## <a name="jobduplexalldocumentscontiguously"></a>JobDuplexAllDocumentsContiguously

此功能指定打印作业的双面打印，而不考虑文档边界。 如果指定了双面打印，则打印作业中所有文档的所有页面都将连续打印，而不会在文档之间插入空白页面。 支持的选项包括 OneSided、TwoSidedShortEdge 和 TwoSidedLongEdge。

为选定的双工生成的 PCL6 由 GPD 双工功能指定。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 JobDuplexAllDocumentsContiguously 选项的 name 属性匹配，则为。

1. 使用以下默认映射：

    | JobDuplexAllDocumentsContiguously 值 | GPD/PPD 文件输入 |
    |-----------------------------------------|--------------------|
    | PrintTicket OneSided                    | 无 GPD           |
    | PrintTicket TwoSidedShortEdge           | 水平 GPD     |
    | PrintTicket TwoSidedLongEdge            | 垂直 GPD       |

1. JobDuplexAllDocumentsContiguously 选项的 name 属性与 GPD 中选项的名称相匹配。

为所选双工生成的 PostScript 由 PPD 双工功能指定，将使用 PPD 中的选项按以下顺序选择：

1. 如果指定了 MSPrintSchemaKeywordMap 并且与 JobDuplexAllDocumentsContiguously 选项的 name 属性匹配，则为。

1. 使用以下默认映射：

    | JobDuplexAllDocumentsContiguously 值 | GPD/PPD 文件输入 |
    |-----------------------------------------|--------------------|
    | PrintTicket OneSided                    | PPD 无           |
    | PrintTicket TwoSidedShortEdge           | PPD DuplexTumble   |
    | PrintTicket TwoSidedLongEdge            | PPD DuplexNoTumble |

1. JobDuplexAllDocumentsContiguously 选项的 name 属性与 PPD 中选项的名称相匹配。

## <a name="documentduplex"></a>DocumentDuplex

此功能控制打印作业中的关联文档的双工打印。 如果指定了此，则打印输出将从新的媒体工作表的正面开始。 支持的选项包括 OneSided、TwoSidedShortEdge 和 TwoSidedLongEdge。

为选定的双工生成的 PCL6 由 GPD 双工功能指定。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 DocumentDuplex 选项的 name 属性匹配，则为。

1. 使用以下默认映射：

    | DocumentDuplex 值          | GPD/PPD 文件输入 |
    |-------------------------------|--------------------|
    | PrintTicket OneSided          | 无 GPD           |
    | PrintTicket TwoSidedShortEdge | 水平 GPD     |
    | PrintTicket TwoSidedLongEdge  | 垂直 GPD       |

1. DocumentDuplex 选项的 name 属性与 GPD 中选项的名称相匹配。

为选定的双工生成的 PostScript 由 PPD 双工功能指定。 将按以下顺序选择使用 PPD 中的选项：

1. 如果指定了 MSPrintSchemaKeywordMap 并且与 DocumentDuplex 选项的 name 属性匹配，则为。

1. 使用以下默认映射：

    | DocumentDuplex 值          | GPD/PPD 文件输入 |
    |-------------------------------|--------------------|
    | PrintTicket OneSided          | PPD 无           |
    | PrintTicket TwoSidedShortEdge | PPD DuplexTumble   |
    | PrintTicket TwoSidedLongEdge  | PPD DuplexNoTumble |

1. DocumentDuplex 选项的 name 属性与 PPD 中选项的名称相匹配。

## <a name="documentnup"></a>DocumentNUp

此功能指定应将多个页面的内容打印到物理介质的每个纸张上。 打印应以这样一种方式进行：不同文档中的内容不会打印到相同的工作表中。 打印架构规范未指定此选项的名称;不过，此选项支持指定将放在物理介质一侧的页面数的 ScoredProperty 和 PagesPerSheet 值。 PagesPerSheet 支持的值为1、2、4、6、8、9、12、16、25和32，其中物理页面方向为2、6、8、12和32旋转。

为所选的 "N" 生成的 PCL6 由筛选器决定。

为所选的 "单向后" 生成的 PostScript 由筛选器决定。

### <a name="joboutputbin"></a>JobOutputBin

此功能描述打印设备打印后介质的位置。 支持的选项为具有相应 GPD/PPD 条目的选项。

为所选的输出 bin 生成的 PCL6 由 GPD OutputBin 功能指定。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并与作业的 name 属性匹配，则为 \[ |文档 |Page \] OutputBin 选项。

1. 作业的名称属性 \[ |文档 |Page \] OutputBin 选项与 GPD 中选项的名称匹配。

为选定的双工生成的 PostScript 由 PPD OutputBin 功能指定。 将按以下顺序选择使用 PPD 中的选项：

1. 如果指定了 MSPrintSchemaKeywordMap 并与作业的 name 属性匹配，则为 \[ |文档 |Page \] OutputBin 选项。

1. 作业的名称属性 \[ |文档 |Page \] OutputBin 选项与 PPD 中的选项名称匹配。

## <a name="jobbindalldocuments"></a>JobBindAllDocuments

此功能描述打印作业中打印的工作表的绑定方法。 打印作业中的所有文档都应该绑定在一起。 支持的选项包括： None、BindBottom、BindLeft、BindRight、BindTop、手册、EdgeStitchBottom、EdgeStitchLeft、EdgeStitchRight 和 EdgeStitchTop。

选择 "手册" 时，筛选器输出的格式设置为 "2"，页面将重新排序，以便在将作业的工作表的一半折叠为同一书籍的正确顺序。

如果为手册指定了 BindingGutter ScoredProperty，则筛选器将 (从纸张中心到缩放可打印区域的边缘) ，至少与 JobBindAllDocumentsGutter 参数指定的大小相同。

如果为 BindLeft 指定了 BindingGutter ScoredProperty，或 EdgeStitchLeft 筛选器将工作表的正面向右移动 JobBindAllDocumentsGutter 参数指定的位置。 现在，位于可打印区域外的内容会被剪切。 工作表背面的内容将在右边缘上按 JobBindAllDocumentsGutter 参数指定的方式进行裁剪。

如果为 BindTop 指定了 BindingGutter ScoredProperty，则筛选器会将纸张的正面和背面的内容沿 JobBindAllDocumentsGutter 参数指定的底部向下移动。 底部的内容将在可打印区域外进行剪辑。

如果为 BindRight 或 EdgeStitchRight 指定了 BindingGutter ScoredProperty，则筛选器将在右侧按 JobBindAllDocumentsGutter 参数指定的位置剪切页面正面的内容。 工作表背面的内容将移动到 JobBindAllDocumentsGutter 参数指定的左侧。 当前位于可打印区域外的内容会被剪切。

如果为 BindBottom 或 EdgeStitchBottom 指定了 BindingGutter ScoredProperty，则筛选器会将纸张的正面和背面沿 JobBindAllDocumentsGutter 参数指定的顶部向顶部移动。 顶部内容位于可打印区域外的内容将被剪裁掉。

> [!NOTE]
> 绑定边缘是指定的边缘，它基于作业中第一个文档的第一页的方向。 对于所有其他选项，将忽略 BindingGutter。

如果 GPD 文件未为所选选项指定命令，则为所选绑定生成的 PCL6 由筛选器决定。

如果 PPD 文件未指定所选选项的调用命令，则为所选绑定生成的 PostScript 由筛选器决定。

## <a name="documentbinding"></a>DocumentBinding

此功能描述在将关联文档的打印工作表绑定到打印作业时使用的方法。 文档中的所有页面都应绑定在一起。 支持的选项包括： None、BindBottom、BindLeft、BindRight、BindTop、手册、EdgeStitchBottom、EdgeStitchLeft、EdgeStitchRight 和 EdgeStitchTop。

选择 "手册" 时，筛选器输出的格式将设置为 "2"，页面将重新排序，以便在文档的工作表的一半以书籍的正确顺序折叠。

如果为手册指定了 BindingGutter ScoredProperty，则筛选器将 (从纸张中心到缩放可打印区域的边缘) ，至少与 DocumentBindingGutter 参数指定的大小相同。

如果为 BindLeft 或 EdgeStitchLeft 指定了 BindingGutter ScoredProperty，则筛选器会将工作表的正面向右移动 DocumentBindingGutter 参数指定的位置。 现在，位于可打印区域外的内容会被剪切。 工作表背面的内容将在右边缘上按 DocumentBindingGutter 参数指定的方式进行裁剪。

如果为 BindTop 或 EdgeStitchTop 指定了 BindingGutter ScoredProperty，则筛选器会将纸张的正面和背面都沿 DocumentBindingGutter 参数指定的底部向下移动。 底部的内容将在可打印区域外进行剪辑。

如果为 BindRight 或 EdgeStitchRight 指定了 BindingGutter ScoredProperty，则筛选器将在右侧通过 DocumentBindingGutter 参数指定的内容来剪裁工作表正面的内容。 工作表背面的内容将移动到 DocumentBindingGutter 参数指定的左侧。 当前位于可打印区域外的内容会被剪切。

如果为 BindBottom 或 EdgeStitchBottom 指定了 BindingGutter ScoredProperty，则筛选器会将纸张的正面和背面沿 DocumentBindingGutter 参数指定的顶部向顶部移动。 顶部内容位于可打印区域外的内容将被剪裁掉。

> [!NOTE]
> 绑定边缘是根据文档首页方向指定的边缘。 对于所有其他选项，将忽略 BindingGutter。

如果 GPD 文件未为所选选项指定命令，则为所选绑定生成的 PCL6 由筛选器决定。

如果 PPD 文件未指定所选选项的调用命令，则为所选绑定生成的 PostScript 由筛选器决定。

## <a name="jobstaplealldocuments"></a>JobStapleAllDocuments

此功能描述了在打印作业中装订打印纸张时使用的方法。 应将该作业中的所有文档一起装订。 支持的选项有对应的 GPD/PPD 条目。

为所选装订生成的 PCL6 由 "GPD 装订" 功能指定。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 JobStapleAllDocuments 选项的 name 属性匹配，则为。

1. JobStapleAllDocuments 选项的 name 属性与 GPD 中选项的名称相匹配。

为所选装订生成的 PostScript 是通过 MSPrintSchemaKeywordMap 值为 JobStapleAllDocuments 或 DocumentStaple 的 PPD 功能指定的。 将按以下顺序选择使用 PPD 中的选项：

1. 如果指定了 MSPrintSchemaKeywordMap 并且与 JobStapleAllDocuments 选项的 name 属性匹配，则为。

1. JobStapleAllDocuments 选项的 name 属性与 PPD 中选项的名称相匹配。

## <a name="jobholepunch"></a>JobHolePunch

此功能描述当打孔在打印作业中使用打印的纸张时使用的方法。 作业中的所有文档应同时打孔。 支持的选项有对应的 GPD/PPD 条目。

为选定的打孔指定的 PCL6 由 GPD 功能指定，PrintSchemaKeywordMap 值为 JobHolePunch 或 DocumentHolePunch。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 JobHolePunch 选项的 name 属性匹配，则为。

1. JobHolePunch 选项的 name 属性与 GPD 中选项的名称相匹配。

为选定的打孔指定的 PostScript 是由 PPD 功能指定的，其 MSPrintSchemaKeywordMap 值为 JobHolePunch 或 DocumentHolePunch。 将按以下顺序选择使用 PPD 中的选项：

1. 如果指定了 MSPrintSchemaKeywordMap 并且与 JobHolePunch 选项的 name 属性匹配，则为。

1. JobHolePunch 选项的 name 属性与 PPD 中选项的名称相匹配。

## <a name="documentholepunch"></a>DocumentHolePunch

此功能描述当打孔在打印作业中的关联文档的打印页上打孔时使用的方法。 文档中的所有页面都应打孔。 支持的选项有对应的 GPD/PPD 条目。

为选定的打孔指定的 PCL6 由 GPD 功能指定，PrintSchemaKeywordMap 值为 JobHolePunch 或 DocumentHolePunch。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 DocumentHolePunch 选项的 name 属性匹配，则为。

1. DocumentHolePunch 选项的 name 属性与 GPD 中选项的名称相匹配。

为选定的打孔指定的 PostScript 是由 PPD 功能指定的，其 MSPrintSchemaKeywordMap 值为 JobHolePunch 或 DocumentHolePunch。 将按以下顺序选择使用 PPD 中的选项：

1. 如果指定了 MSPrintSchemaKeywordMap 并且与 DocumentHolePunch 选项的 name 属性匹配，则为。

1. DocumentHolePunch 选项的 name 属性与 PPD 中选项的名称相匹配。

## <a name="pagemirrorimage"></a>PageMirrorImage

此功能指定是否应镜像页面内容。 支持的选项为 None 和 MirrorImageWidth。

为所选镜像生成的 PCL6 由 GPD 功能指定，PrintSchemaKeywordMap 值为 PageMirrorImage。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 PageMirrorImage 选项的 name 属性匹配，则为。

1. PageMirrorImage 选项的 name 属性与 GPD 中选项的名称相匹配。

为所选镜像生成的 PostScript 由 PPD MirrorPrint 功能指定。 将按以下顺序选择使用 PPD 中的选项：

1. 如果指定了 MSPrintSchemaKeywordMap 并且与 PageMirrorImage 选项的 name 属性匹配，则为。

1. 使用以下默认映射：

    | PageMirrorImage 值        | GPD/PPD 文件输入 |
    |------------------------------|--------------------|
    | PrintTicket 无             | PPD False          |
    | PrintTicket MirrorImageWidth | PPD True           |

1. PageMirrorImage 选项的 name 属性与 PPD 中选项的名称相匹配。

## <a name="pagenegativeimage"></a>PageNegativeImage

此功能指定页面内容是否应为负片图像。 支持的选项为 "无" 和 "负数"。

为所选负打印生成的 PCL6 由 GPD 功能指定，PrintSchemaKeywordMap 值为 PageNegativeImage。 将按以下顺序选择要使用的 GPD 中的选项：

1. 如果指定了 PrintSchemaKeywordMap 并且与 PageNegativeImage 选项的 name 属性匹配，则为。

1. PageNegativeImage 选项的 name 属性与 GPD 中选项的名称相匹配。

为所选负打印生成的 PostScript 由 PPD NegativePrint 功能指定。 将按以下顺序选择使用 PPD 中的选项：

1. 如果指定了 MSPrintSchemaKeywordMap 并且与 PageNegativeImage 选项的 name 属性匹配，则为。

1. 使用以下默认映射：

    | PageNegativeImage 值 | GPD/PPD 文件输入 |
    |-------------------------|--------------------|
    | PrintTicket 无        | PPD False          |
    | PrintTicket 负数    | PPD True           |

1. PageNegativeImage 选项的 name 属性与 PPD 中选项的名称相匹配。

## <a name="related-topics"></a>相关主题

[默认 PageMediaSize 映射](default-pagemediasize-mappings.md)  

[标准 XPS 筛选器](standard-xps-filters.md)  

可在此处下载打印架构规范：

[打印架构规范1。1](https://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/print-schema-spec-1-1.zip)

[打印架构规范2。0](https://download.microsoft.com/download/d/e/c/deca6e6b-3e81-48e7-b7ef-6d92a547d03c/print-schema-spec-2-0.zip)
