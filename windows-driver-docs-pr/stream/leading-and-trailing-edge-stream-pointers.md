---
title: 前导和尾随边缘流指针
description: 前导和尾随边缘流指针
ms.assetid: 73ab974f-8034-421f-980a-2393d84ec54c
keywords:
- 流指针 WDK AVStream 前导和尾随边缘
- 前导边缘流指针 WDK AVStream
- 尾随边缘流指针 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cba66bb34a726076a97d47d52022cd0427f50ff7
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348842"
---
# <a name="leading-and-trailing-edge-stream-pointers"></a>前导和尾随边缘流指针





默认情况下，包含每个 AVStream 队列*前沿*流指针。 前沿指向新帧到达放入队列。 具体而言，前导边缘最初指向第一个帧到达放入队列并不会移动直到微型驱动程序将其移动。 AVStream 创建前导边缘，然后针对而存在的队列的生存期。 微型驱动程序可以操作使用由 Microsoft 提供的函数的前沿。

当新帧到达队列中时，AVStream 设置前沿以指向此帧中，前提是前导边缘不已指向一个帧。

若要获取指向前导边缘流指针的指针，微型驱动程序调用[ **KsPinGetLeadingEdgeStreamPointer**](https://msdn.microsoft.com/library/windows/hardware/ff563513)。

微型驱动程序负责提升中所有前导边缘，但下表中汇总的两种情况。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>情形</th>
<th>AVStream 的行为</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>先前为空队列中到达一个帧。</p></td>
<td><p>AVStream 设置为指向此帧的前沿。</p></td>
</tr>
<tr class="even">
<td><p>前沿指向一个帧。 IRP 对应于此帧将被取消。</p></td>
<td><p>AVStream 前移前沿。 前沿现在指向较新帧。</p></td>
</tr>
</tbody>
</table>

 

请参阅[简介 Stream 指针](introduction-to-stream-pointers.md)有关改进流指针的详细信息。

### <a name="specifying-a-trailing-edge-stream-pointer"></a>指定的尾随边 Stream 指针

微型驱动程序可以指定一个队列有尾随边缘流指针。 尾随边缘通常表示微型驱动程序感兴趣的最早的帧。 若要指定尾随边缘，设置 KSPIN\_标志\_DISTINCT\_尾随\_中的边缘标志**标志**的相关成员[ **KSPIN\_描述符\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)结构。 然后调用[ **KsPinGetTrailingEdgeStreamPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff563518)以获取尾随边缘流指针的指针。

当尾随边缘的发展时，完成到它以前指向降到零的框架和框架的引用计数。 如果框架的最后一个包含在其 IRP，接收器 pin 完成时向调用方; IRP源 pin 将 IRP 发送到连接到的 pin。

### <a name="maintaining-a-frame-window"></a>维护框架窗口

由于规则中所述的框架引用计数[简介 Stream 指针](introduction-to-stream-pointers.md)，直到它被取消，前导和尾随边缘之间的帧将保留在队列中<em>，即使未被引用框架流指针</em>。 在这种情况下，微型驱动程序可以使用前导和尾随边缘指针来维护工作窗口的多个连续帧。 处理或填充，例如，可能正在等待在窗口中的帧。

在下图中，最早的帧，是在底部。 新帧到达顶部。 每个帧中的数字是该范围的引用计数。 当流指针前进，它们在此图中向上移动。

![说明 avstream 流指针引用 pin 队列的关系图](images/cnstream4.png)

最左侧的队列演示微型驱动程序如何使用尾随边缘来创建一组有效的帧。 前导和尾随边缘之间的每个框架都有引用计数为一个没有流指针引用这些框架的情况。

中间队列是一种[克隆 Stream 指针](cloning-stream-pointers.md)。 驱动程序已反复克隆，然后高级前沿，pin 过程步骤中所述[AVStream DMA 服务](avstream-dma-services.md)。

最右侧的队列显示微型驱动程序如何通过使用流指针克隆来维护背后尾随边缘的帧的引用计数。

 

 




