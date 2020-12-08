---
title: 前导和尾随边缘流指针
description: 前导和尾随边缘流指针
keywords:
- 流指针 WDK AVStream、前导和尾随边缘
- 领先的边缘流指针 WDK AVStream
- 尾部边缘流指针 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48d3ec0c062443654f62f90ad1e295888a321438
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799291"
---
# <a name="leading-and-trailing-edge-stream-pointers"></a>前导和尾随边缘流指针





默认情况下，每个 AVStream 队列都包含一个 *前导边缘* 流指针。 当到达队列时，前导边缘指向新帧。 具体而言，前导边缘最初指向第一个帧进入队列，并不移动，直到微型驱动程序移动它。 AVStream 创建前导边缘，该边缘在队列的生存期内存在。 微型驱动程序可以使用 Microsoft 提供的功能来操纵领先的边缘。

当新帧到达队列时，AVStream 会将前导边缘设置为指向此帧，前提是前导边缘尚未指向帧。

若要获取指向前导边缘流指针的指针，微型驱动程序将调用 [**KsPinGetLeadingEdgeStreamPointer**](/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)。

在下表中汇总的两种情况下，微型驱动程序负责推动领先的边缘。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>场景</th>
<th>AVStream 的行为</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>帧到达之前的空队列。</p></td>
<td><p>AVStream 将前导边缘设置为指向此帧。</p></td>
</tr>
<tr class="even">
<td><p>前导边缘指向帧。 与此帧对应的 IRP 已取消。</p></td>
<td><p>AVStream 使领先边缘前进。 前导边缘现在指向较新的帧。</p></td>
</tr>
</tbody>
</table>

 

有关向前传递流指针的详细信息，请参阅 [流指针简介](introduction-to-stream-pointers.md) 。

### <a name="specifying-a-trailing-edge-stream-pointer"></a>指定尾随边缘流指针

微型驱动程序可以指定队列具有尾随边缘流指针。 尾随边缘通常指示微型驱动程序的最早的帧。 若要指定尾随边缘，请 \_ \_ \_ \_ 在相关 [**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构的 **Flags** 成员中设置 KSPIN 标志 DISTINCT 尾边缘标志。 然后，调用 [**KsPinGetTrailingEdgeStreamPointer**](/windows-hardware/drivers/ddi/ks/nf-ks-kspingettrailingedgestreampointer) 以获取指向尾部边缘流指针的指针。

当尾随边缘前进时，它以前指向的帧上的引用计数将降到零，并且帧完成。 如果帧是其 IRP 内包含的最后一个，则接收器 pin 会向调用方完成 IRP;源 pin 将 IRP 发送到它所连接到的 pin。

### <a name="maintaining-a-frame-window"></a>维护框架窗口

由于 [流指针简介](introduction-to-stream-pointers.md)中所述的帧引用计数规则，在取消之前，前导边缘和尾随边缘之间的帧将保留在队列中<em>，即使该帧未被流指针引用</em>也是如此。 因此，微型驱动程序可以使用前导和尾随边缘指针来维护多个连续帧的工作窗口。 例如，窗口中的帧可能等待处理或填充。

在下图中，最旧的帧位于底部。 新帧到达顶部。 每个帧中的数字是该帧的引用计数。 当流指针前进时，它们将在此关系图中上移。

![说明引用 pin 队列的 avstream 流指针的关系图](images/cnstream4.png)

最左侧的队列显示微型驱动程序如何使用尾部边缘来创建工作帧集。 尽管没有流指针引用这些帧，但前导边缘和尾随边缘之间的每个帧都有一个引用计数。

中间队列是 [克隆流指针](cloning-stream-pointers.md)的示例。 该驱动程序重复克隆，然后将其前进到最先进，如 [AVSTREAM DMA Services](avstream-dma-services.md)中的固定进程步骤中所述。

最右边的队列显示微型驱动程序如何使用流指针克隆来维护尾部边缘后面的帧的引用计数。

 

