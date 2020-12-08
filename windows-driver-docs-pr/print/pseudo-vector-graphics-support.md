---
title: 伪矢量图形支持
description: 伪矢量图形支持
keywords:
- 矢量图形 WDK Unidrv，pseudovector 图形
- pseudovector 图形 WDK Unidrv
- nonvector 图形设备 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5863841e662a16c2e8aebdad84372cb76b9cf2bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807117"
---
# <a name="pseudo-vector-graphics-support"></a>伪矢量图形支持





不支持 true 向量图形的设备可以利用 Unidrv 为 pseudovector 图形提供的支持。 使用此功能时，Unidrv 会将纯黑色矩形和水平和垂直直线直接下载到 nonvector 图形设备，从而减少了在光栅图面上渲染这些图形的开销。 这还会减少输出数据的大小，从而提高不会有效处理光栅数据的设备的打印机吞吐量。

若要从此功能中受益，nonvector 图形设备的微型驱动程序仅需支持 CmdRectBlackFill 命令。 当打印机属性页的 "**高级**" 选项卡中的 "**打印优化**" 功能关闭时，将禁用此功能。

Pseudovector graphics 功能可截获对 [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt)、 [**DrvStrokePath**](/windows/win32/api/winddi/nf-winddi-drvstrokepath)和 [**DrvLineTo**](/windows/win32/api/winddi/nf-winddi-drvlineto)的调用，以确定是否要绘制实心黑色矩形或垂直或水平线条。 当 Unidrv 识别出要绘制为一个 (的有效矩形时，该图形将绘制为一个纯黑色的图形，并且不使用当前目标位) 的 ROP，而是将其存储在矩形数组中，而不是在图面上绘制。

Pseudovector graphics 功能最困难的方面是避免由必须在以前绘制的对象之上绘制的对象导致的 z 顺序问题。 顶部的对象可能需要清除或覆盖部分黑色矩形。 如果已将黑色矩形下载到设备，则在系统表面以后绘制的对象可能不会正确绘制。

此问题的解决方法是临时存储有效矩形，而不是立即在图面上绘制。 在图面上绘制新的对象时，Unidrv 会检查该对象，以查看该对象是否与任何黑色矩形重叠。 如果是这样，则在绘制新的对象之前，将首先在图面上绘制黑色矩形的重叠部分，从而保持正确的 z 顺序。 首先绘制矩形还会考虑到要绘制的新对象可能有一个与之关联的 ROP，包括与目标交互的对象。

此外，要绘制的新对象有可能包含复杂的剪辑，使得到的图不再是矩形。 当带区或页面呈现完成后，任何剩余的黑色矩形都可以直接下载到设备，而不会导致任何 z 顺序问题。 Unidrv 维护一个列表，其中每个带区最多256个矩形，尽可能连接 BitBlt 矩形。

### <a name="pseudovector-graphics-issues"></a>Pseudovector 图形问题

在某些情况下，pseudovector graphics 功能可能会改变 z 顺序，特别是在将文本直接下载到设备时，并且具有复杂剪辑的后续对象必须与该文本交互。

 

