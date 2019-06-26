---
title: 伪矢量图形支持
description: 伪矢量图形支持
ms.assetid: 8eeba51b-00fa-4bf3-a78c-ac1d1adc9696
keywords:
- 矢量图形 WDK Unidrv，pseudovector 图形
- pseudovector 图形 WDK Unidrv
- nonvector 图形设备 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90582e540cba9e034bc1f818131871859c66c5b1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358462"
---
# <a name="pseudo-vector-graphics-support"></a>伪矢量图形支持





不支持 true 矢量图形的设备可以充分利用 Unidrv 提供 pseudovector 图形的支持。 当使用此功能时，Unidrv 下载 solid 黑色的矩形和水平和垂直线条直接到 nonvector 图形设备时，减少呈现这些数字光栅图面上的开销。 这还可以减少输出数据，这可以提高打印机的设备无法有效地处理光栅数据吞吐量的大小。

若要利用此功能，为 nonvector 图形设备微型驱动程序需要只是为了支持 CmdRectBlackFill 命令。 此功能处于禁用状态时**打印优化**中的功能**高级**打印机属性页的选项卡处于关闭状态。

Pseudovector 图形功能截获对调用[ **DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)， [ **DrvStrokePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)，和[ **DrvLineTo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto)，以确定是否 solid 黑色的矩形或垂直或水平线条是要在绘制。 如果 Unidrv 识别图绘制为一个有效的矩形 （一种为纯黑色、 具有任何复杂的剪辑，并且不使用使用当前的目标位 ROP），而不是图面上所绘制的矩形数组中存储。

Pseudovector 图形功能的最困难的方面避免导致必须先前绘制对象之上绘制的对象的 z 顺序问题。 在最前面的对象可能需要清除或覆盖一个黑色的矩形的一部分。 当黑色的矩形已经下载到设备，更高版本上绘制对象系统绘制图面可能不正确。

此问题的解决方案是一个有效的矩形，而不是立即表面上绘制临时存储。 当新对象是图面上绘制时，Unidrv 检查它以查看该对象是否与任何黑色的矩形重叠。 如果是这样，黑色的矩形的重叠的部分绘制图面上第一次，从而保持正确 z-顺序绘制新对象之前。 绘制矩形首先还会考虑要绘制的新对象可能具有与之关联，其中包括一个与目标交互 ROP 情况。

此外，很可能要绘制的新对象，包含复杂的剪辑，以便生成图不再是一个矩形。 带外或页面呈现完成后，任何剩余的黑色矩形可以直接下载到设备而不会导致任何 z 顺序问题。 Unidrv 维护每个带区，最多 256 个矩形的列表串联 BitBlt 矩形，在可能的情况。

### <a name="pseudovector-graphics-issues"></a>Pseudovector 图形问题

Pseudovector 图形功能可能会更改 z 顺序在某些情况下，尤其是当与设备直接下载文本并且具有复杂的剪辑的后续对象必须与该文本进行交互。

 

 




