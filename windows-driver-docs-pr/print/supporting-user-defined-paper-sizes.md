---
title: 支持用户定义的纸张大小
description: 支持用户定义的纸张大小
ms.assetid: f9c0b759-687e-4d92-80ce-330e30cbc41c
keywords:
- 用户定义的纸张大小 WDK Unidrv
- 自定义的纸张大小 WDK Unidrv
- 最大纸张大小 WDK Unidrv
- 边距 WDK 纸张大小
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dfbd1d19ac42c46391f0a36aadb5a2bd93fd0ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554231"
---
# <a name="supporting-user-defined-paper-sizes"></a>支持用户定义的纸张大小





用户定义的纸张大小可能是特定于一台打印服务器，通常为特定的应用程序自定义。 因此它们通常称为自定义的纸张大小。 系统管理员使用打印文件夹来定义自定义的纸张大小。 如果打印机可以处理自定义的纸张大小，供应商必须使用打印机的 GPD 文件以指定大小的可接受范围。

用于描述自定义纸张的可接受的大小范围提供了两种方法：

-   可以显式指定大小范围。

-   您可以指定相对于打印机的最大的纸张大小的大小范围。

### <a name="specifying-paper-size-ranges-explicitly"></a>显式指定纸张大小范围

若要使用此方法，GPD 文件的 PaperSize 功能都必须包括\*选项使用 CUSTOMSIZE 自变量的条目。 此条目必须包含以下选项属性：

\*MinSize \*MaxSize \*MaxPrintableWidth \*MinLeftMargin \*TopMargin \*BottomMargin \*CenterPrintable？
\*CursorOrigin\*命令可用于这些 GPD 条目创建自定义的纸张大小说明仅针对打印机具有下列特征：

-   打印机支持命令 （通常通过移动光标原点） 显式选择自定义的纸张大小。

-   游标源保持固定，相对于纸时，适用于所有自定义的纸张大小的左上角。 （这通常不是为横向模式下打印或中心馈送或右侧 hand 送入的打印机，则返回 true。）

-   顶部和底部边距是独立的纸张大小。

-   纸张宽度是否为指定的值之和小于\* **MinLeftMargin**并\* **MaxPrintableWidth**，没有任何右边距。 也就是说，打印机可以打印到纸张的右边缘。

命令参数 (在指定\***命令**条目) 如果，则可以在打印时计算[标准变量表达式](standard-variable-expressions.md)使用，通常包括 PhysPaperLength 和PhysPaperWidth 变量。 这些变量表示打印作业，由应用程序指定所请求的实际的纸张大小。

### <a name="specifying-paper-size-ranges-relative-to-the-printers-largest-paper-size"></a>指定纸张大小范围相对于打印机的最大的纸张大小

对于不支持显式指定自定义的纸张大小范围所需的特征的打印机，另一种方法提供，它指定相对于打印机的最大的纸张大小的纸张大小。

若要使用此方法，GPD 文件的 PaperSize 功能都必须包括\*选项使用 CUSTOMSIZE 自变量的条目。 此条目必须包含以下选项属性：

\*MinSize \*MaxSize \*MaxPrintableWidth \*CustCursorOriginX \*CustCursorOriginX \*CustPrintableOriginX \*CustPrintableOriginY \*CustPrintableSizeX \*CustPrintableSizeY\*命令时指定的大小范围相对于打印机的最大的纸张大小，使用下列对齐规则：

-   对于左侧源打印机，必须对齐所有纸张大小上的边距和左边距。

-   右送纸打印机必须对齐所有纸张大小上的边距和右边距。

-   对于中心源打印机，必须对齐的上边距和所有纸张大小的顶部中心点。

包括以下步骤：

1.  确定打印机的最大的纸张大小的以下信息：
    -   选择最大的纸张大小所需的命令。
    -   将使用的最大的纸张大小的值\*PageDimensions， \*CursorOrigin， \*PrintableOrigin，和\*PrintableArea GPD 条目，如同将包括在 GPD 文件中。 但是，将不实际置于这些项在文件中。

2.  创建指定或计算以下信息为每个自定义的纸张大小，相对于打印机的最大的纸张大小的公式。
    -   源和每个纸张的可打印区域的大小。
    -   每个纸张的的游标原点。

步骤 2 的公式必须是[CUSTOMSIZE 参数表达式](option-attributes-for-the-papersize-feature.md#ddk-customsize-parameter-expressions-gg)，这被指定为以下 GPD 条目的值：

\*CustCursorOriginX \*CustCursorOriginX \*CustPrintableOriginX \*CustPrintableOriginY \*CustPrintableSizeX \*CustPrintableSizeY CUSTOMSIZE 选项还必须包括\*指定选择的最大的打印机大小的命令的命令项。 此命令将发送的所有自定义纸张大小和指定的可打印区域和游标源控件的公式，其中打印机上打印实际纸张，无论其大小。

### <a name="sample-calculations"></a>示例计算

举一个简单的例子，假设您的打印机支持为最大纸张大小的边距的边距大小相同的自定义的纸张大小。 所涉及的步骤如下：

确定最大的纸张大小的值\* **PageDimensions**， \* **CursorOrigin**， \* **PrintableOrigin**，和\* **PrintableArea**条目。 （不要将这些条目 GPD 文件中。）

确定每个根据这些值的最大纸张大小的边距的宽度，如以下 pseudoexpressions 中所示：

LeftMarginWidth=\***PrintableOrigin**.x

RightMarginWidth =\***PageDimensions**.x-\***PrintableArea**.x LeftMarginWidthTopMarginWidth =\***PrintableOrigin**.y BottomMarginWidth =\***PageDimensions**.y-\***PrintableArea**.y-**TopMarginWidth**

在这些 pseudoexpressions.x 和.y 表示每个条目的水平和垂直组件[对](pairs.md)值。 对于横向打印，使用环境值\* **PrintableArea**并\* **PrintableOrigin**。

现在创建 pseudoexpressions 的指定或计算的非标准纸张大小的可打印区域。

\*CustPrintableOriginX: %d{LeftMarginWidth}

\*CustPrintableOriginY: %d {TopMarginWidth}

\*CustPrintableSizeX: %d{PhysPaperWidth-LeftMarginWidth-RightMarginWidth}

\*CustPrintableSizeY: %d {PhysPaperLength TopMarginWidth BottomMarginWidth}

请注意，使用 PhysPaperWidth 和 PhysPaperLength 两个标准变量。 在运行时，这些变量包含的长度和应用程序已请求的实际的纸张大小的宽度。

请注意，这些 pseudoexpressions 有效纸张是左填充、 右送纸或中心馈送。

插入到两个表达式来创建 GPD 条目在步骤 1 中确定的实际值。 例如，可能是：
```cpp
*CustPrintableOriginX:  %d{300}
*CustPrintableOriginY:  %d{300}
*CustPrintableSizeX:   %d{PhysPaperWidth-600}
*CustPrintableSizeY:  %d{PhysPaperLength-600}
```

创建 pseudoexpressions 计算游标源索引。 在以下 pseudoexpressions， \*CursorOrigin.x 并\*CursorOrigin.y 是占位符的水平和垂直组件[对](pairs.md)最大纸张大小的游标来源的值。

对于左侧送入打印机：

\*CustCursorOriginX: %d {\*CursorOrigin.x} \*CustCursorOriginY: %d {\*CursorOrigin.y} 右送入打印机：

\*CustCursorOriginX: %d {\*CursorOrigin.x+PhysPaperWidth-\*PageDimensions.x} \*CustCursorOriginY: %d {\*CursorOrigin.y} center 送入打印机：

\*CustCursorOriginX: %d {\*CursorOrigin.x+(PhysPaperWidth-PageDimensions.x)/2} \*CustCursorOriginY: %d {\*CursorOrigin.y} 插入到两个表达式来创建 GPD 条目在步骤 1 中确定的实际值. 示例可能是 （对于 center 送入的纸张）：
```cpp
*CustCursorOriginX:  %d{((PhysPaperWidth-14040)/2)+300}
*CustCursorOriginY:   %d{180}
```

指定剩余的三个 GPD 项-值\*MinSize， \*MaxSize 和\*MaxPrintableWidth。 为指定的值\*MaxPrintableWidth 实际上不使用此方法，但分析程序需要的项存在，因此其值可以设置为 1。

### <a name="a-real-example"></a>真实示例

以下示例 GPD 文件段落介绍 center 送入打印机的可接受的自定义的纸张大小。 对于纵向模式下，所有自定义纸张大小的所有边距都是 300 主单位 （1/4 英寸） 的大小。 为横向模式下，顶部和底部边距是 240 主单元时左侧和右边距是 200 个单位的 master。

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

 

 




