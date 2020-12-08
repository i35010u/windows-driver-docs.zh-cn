---
title: 支持用户定义的纸张大小
description: 支持用户定义的纸张大小
keywords:
- 用户定义的纸张大小 WDK Unidrv
- 自定义纸张大小 WDK Unidrv
- 最大纸张大小 WDK Unidrv
- 页边距 WDK 纸张大小
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abe105369f11b71dd28863e4ec543014f06e1fad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806783"
---
# <a name="supporting-user-defined-paper-sizes"></a>支持用户定义的纸张大小





用户定义的纸张大小可以特定于单个打印服务器，并且通常是针对特定应用程序自定义的。 因此它们通常称为自定义纸张大小。 系统管理员使用 "打印" 文件夹来定义自定义纸张大小。 如果打印机能够处理自定义纸张大小，则供应商必须使用打印机的 GPD 文件来指定大小可接受的范围。

提供了两种方法来描述自定义纸张的可接受大小范围：

-   可以显式指定大小范围。

-   可以指定相对于打印机最大纸张大小的大小范围。

### <a name="specifying-paper-size-ranges-explicitly"></a>显式指定纸张大小范围

若要使用此方法，GPD 文件的 PaperSize 功能必须包含 \* 带有 CUSTOMSIZE 参数的选项项。 此条目必须包含以下选项属性：

\*MinSize \* MaxSize \* MaxPrintableWidth \* MinLeftMargin \* TopMargin \* BottomMargin \* CenterPrintable？
\*CursorOrigin \* 命令您可以使用这些 GPD 条目为具有以下特征的打印机创建自定义纸张大小说明：

-   打印机支持通过命令显式选择自定义纸张大小 (通常是通过将光标原点移) 来进行的。

-   对于所有自定义纸张大小，光标原点保持固定，相对于纸张的左上角。  (对于横向模式打印，或对于中心送进或右送纸的打印机，这通常不是这样。 ) 

-   上边距和下边距独立于纸张大小。

-   如果纸张宽度小于为 MinLeftMargin 和 MaxPrintableWidth 指定的值的总和 \* **MinLeftMargin** \* *_MaxPrintableWidth_*，则没有右边距。 也就是说，打印机可以打印到纸张的右边缘。

\*如果使用 [标准变量表达式](standard-variable-expressions.md)（通常包括 PhysPaperLength 和 PhysPaperWidth 变量），则在 *_命令_*) 项中指定的命令参数 (可以在打印时计算。 这些变量表示应用程序指定的打印作业的实际纸张大小。

### <a name="specifying-paper-size-ranges-relative-to-the-printers-largest-paper-size"></a>指定纸张大小范围（相对于打印机的最大纸张大小）

对于不支持明确指定自定义纸张大小范围所需要的特性的打印机，提供了另一种方法，该方法指定纸张大小（相对于打印机的最大纸张大小）。

若要使用此方法，GPD 文件的 PaperSize 功能必须包含 \* 带有 CUSTOMSIZE 参数的选项项。 此条目必须包含以下选项属性：

\*MinSize \* MaxSize \* MaxPrintableWidth \* CustCursorOriginX \* CustCursorOriginX \* CustPrintableOriginX \* CustPrintableOriginY CustPrintableSizeX CustPrintableSizeY \* \* \* Command 指定相对于打印机最大纸张大小的大小范围时，请使用以下对齐规则：

-   对于左打印机，所有纸张大小的上边距和左边距必须对齐。

-   对于右送纸打印机，所有纸张大小的上边距和右边距必须对齐。

-   对于中心源打印机，必须对齐所有纸张大小的上边距和顶部中心点。

涉及以下步骤：

1.  确定打印机最大纸张大小的下列信息：
    -   选择最大纸张大小所需的命令。
    -   适用于最大纸张大小的 \* PageDimensions、 \* CursorOrigin、 \* PRINTABLEORIGIN 和 \* PrintableArea GPD 条目的值，就像它们将包含在 GPD 文件中一样。 但是，实际上不会将这些项放在文件中。

2.  创建指定或计算每个自定义纸张大小的下列信息的公式，相对于打印机的最大纸张大小。
    -   每个纸的可打印区域的原点和大小。
    -   每个纸的光标原点。

步骤2的公式必须是 [CUSTOMSIZE 参数表达式](option-attributes-for-the-papersize-feature.md#ddk-customsize-parameter-expressions-gg)，这些表达式指定为以下 GPD 条目的值：

\*CustCursorOriginX \* CustCursorOriginX \* CustPrintableOriginX \* CustPrintableOriginY \* CustPrintableSizeX \* CustPrintableSizeY CUSTOMSIZE 选项还必须包含 \* 命令项，该命令项指定了用于选择最大打印机大小的命令。 对于所有自定义纸张大小，将发送此命令，为可打印区域和光标源控件指定的公式将在实际纸张上打印的位置（无论大小如何）。

### <a name="sample-calculations"></a>示例计算

作为一个简单的示例，假设您的打印机支持的自定义纸张大小的边距与最大纸张大小的边距相同。 涉及的步骤包括：

确定最大纸张大小的 \* **PageDimensions**、 \* *_CursorOrigin_*、 \* *_PrintableOrigin_* 和 \* *_PrintableArea_* 条目的值。  (不要将这些项放在 GPD 文件中。 ) 

根据这些值，确定最大纸张大小的每个边距的宽度，如以下 pseudoexpressions 中所示：

LeftMarginWidth = \* *_PrintableOrigin_*

RightMarginWidth = \* *_PageDimensions_*- \* *_PrintableArea_*-LeftMarginWidthTopMarginWidth = \* *_PrintableOrigin_* BottomMarginWidth = \* *_PageDimensions_* \* *_PrintableArea_***TopMarginWidth** PageDimensions-PrintableArea-TopMarginWidth-

在这些 pseudoexpressions 中，a.x 和. y 表示每个项的 [对](pairs.md) 值的水平和垂直分量。 对于横向打印，请使用 \* *_PrintableArea_* 和 PrintableOrigin 的横向值 \* *_PrintableOrigin_*。

现在，创建 pseudoexpressions 来指定或计算非标准纸张大小的可打印区域。

\*CustPrintableOriginX：% d {LeftMarginWidth}

\*CustPrintableOriginY：% d {TopMarginWidth}

\*CustPrintableSizeX：% d {PhysPaperWidth-LeftMarginWidth-RightMarginWidth}

\*CustPrintableSizeY：% d {PhysPaperLength-TopMarginWidth-BottomMarginWidth}

请注意，使用 PhysPaperWidth 和 PhysPaperLength 这两个标准变量。 在运行时，这些变量包含应用程序请求的实际纸张大小的长度和宽度。

请注意，无论是送纸、进纸还是送入纸，这些 pseudoexpressions 都是有效的。

将步骤1中确定的实际值插入到这些表达式中，以创建 GPD 条目。 示例可能为：
```cpp
*CustPrintableOriginX:  %d{300}
*CustPrintableOriginY:  %d{300}
*CustPrintableSizeX:   %d{PhysPaperWidth-600}
*CustPrintableSizeY:  %d{PhysPaperLength-600}
```

创建用于计算游标源索引的 pseudoexpressions。 在下面的 pseudoexpressions 中， \* CursorOrigin 和 \* CursorOrigin 是针对最大纸张大小光标原点的 [对](pairs.md) 值的水平和垂直分量的占位符。

对于左送打印机：

\*CustCursorOriginX：% d { \* CursorOrigin} \* CustCursorOriginY：% d { \* CursorOrigin} 对于右送打印机：

\*CustCursorOriginX：% d { \* CursorOrigin + PhysPaperWidth- \* PageDimensions \* CustCursorOriginY：% d { \* CursorOrigin} 对于中心送纸打印机：

\*CustCursorOriginX：% d { \* CursorOrigin + (PhysPaperWidth-PageDimensions) /2} \* CustCursorOriginY：% d { \* CursorOrigin} 将在步骤1中确定的实际值插入到这些表达式中以创建 GPD 项。 对于中心送纸) ，可能 (的示例：
```cpp
*CustCursorOriginX:  %d{((PhysPaperWidth-14040)/2)+300}
*CustCursorOriginY:   %d{180}
```

为其余三个 GPD 条目指定值-- \* MinSize、 \* MaxSize 和 \* MaxPrintableWidth。 为 MaxPrintableWidth 指定的值 \* 实际上并不用于此方法，但分析器要求该项存在，因此它的值可以设置为1。

### <a name="a-real-example"></a>真实示例

下面的示例 GPD 文件段描述了可接受的、用于中心纸打印机的自定义纸张大小。 对于纵向模式，所有自定义纸张大小的所有边距均为300主单位 (1/4 英寸) 大小。 对于横向模式，上边距和下边距均为240主单元，而左右边距为200主单位。

```cpp
*Option: CUSTOMSIZE
{
  *rcNameID: =USER_DEFINED_SIZE_DISPLAY
  *MinSize: PAIR(4200,9000)
  *MaxSize: PAIR(14040, 21240)
  *MaxPrintableWidth: 14040
  *MinLeftMargin: 100
  *CenterPrintable?: FALSE
  *PageProtectMem: 1692
  *InsertBlock: =PaperConstraints
  *switch: Orientation
  {
    *case: PORTRAIT
    {
       *CustCursorOriginX:  %d{((PhysPaperWidth-14040)/2)+300}
       *CustCursorOriginY:   %d{180}
       *CustPrintableOriginX:  %d{300}
       *CustPrintableOriginY:  %d{300}
       *CustPrintableSizeX:   %d{PhysPaperWidth-600}
       *CustPrintableSizeY:  %d{PhysPaperLength-600}
       *Command: CmdSelect
       {
         *Order: DOC_SETUP.13
 *Cmd: "<1B>&l101a8c1e99F<1B>*p0x0Y<1B>*c0t8064x12528Y"
 }
    }
    *case: LANDSCAPE_CC90
    {
      *switch:  Option20
      {
      *% The 8100 rotates the landscape job 180 degrees if a stapler
      *% is attached, so the staple can be placed in the top left
      *% corner of the document. The printer always rotates the
      *% landscape job, even if stapling is not selected.
        *case: 3KStapler
        {
          *CustCursorOriginX:  %d{((PhysPaperWidth-14040)/2)+200}
          *CustCursorOriginY:   %d{PhysPaperLength}
          *CustPrintableOriginX:  %d{200}
          *CustPrintableOriginY:  %d{240}
          *CustPrintableSizeX:   %d{PhysPaperWidth-400}
          *CustPrintableSizeY:  %d{PhysPaperLength-480}
          *Command: CmdSelect
          {
            *Order: DOC_SETUP.13
            *Cmd: "<1B>&l101a8c1e63F<1B>*p0x0Y<1B>*c0t12456x8184Y"
          }
        }
        *case: MBM5S
        {
          *CustCursorOriginX:  %d{((PhysPaperWidth-14040)/2)+200}
          *CustCursorOriginY:   %d{PhysPaperLength}
          *CustPrintableOriginX:  %d{200}
          *CustPrintableOriginY:  %d{240}
          *CustPrintableSizeX:   %d{PhysPaperWidth-400}
          *CustPrintableSizeY:  %d{PhysPaperLength-480}
          *Command: CmdSelect
          {
            *Order: DOC_SETUP.13
            *Cmd: "<1B>&l101a8c1e63F<1B>*p0x0Y<1B>*c0t12456x8184Y"
          }
        }
        *default
        {
          *CustCursorOriginX:  %d{((PhysPaperWidth-14040)/2)+200}
          *CustCursorOriginY:   %d{21000}
          *CustPrintableOriginX:  %d{200}
          *CustPrintableOriginY:  %d{240}
          *CustPrintableSizeX:   %d{PhysPaperWidth-400}
          *CustPrintableSizeY:  %d{PhysPaperLength-480}
          *Command: CmdSelect
          {
            *Order: DOC_SETUP.13
 *Cmd: "<1B>&l101a8c1e63F<1B>*p0x0Y<1B>*c0t12456x8184Y"
 }
        }
      } *% switch Option20
    } *% case LANDSCAPE_CC90
  } *% switch Orientation
}
```

 

 




