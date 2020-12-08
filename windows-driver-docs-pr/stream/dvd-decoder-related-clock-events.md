---
title: 与 DVD 解码器相关的时钟事件
description: 与 DVD 解码器相关的时钟事件
keywords:
- DVD 解码器微型驱动程序 WDK，主时钟
- 解码器微型驱动程序 WDK DVD，主时钟
- 主时钟 WDK DVD 解码器
- 时钟 WDK DVD 解码器
- 事件 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf71874a37af7696f7e7a29043c84a4e398255f0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782083"
---
# <a name="dvd-decoder-related-clock-events"></a>与 DVD 解码器相关的时钟事件





支持 DVD 播放的主时钟的任何 DVD 解码器微型驱动程序流还必须支持以下两个时钟事件： [**KSEVENT \_ 时钟 \_ 位置 \_ 标记**](./ksevent-clock-position-mark.md) 和 [**KSEVENT \_ 时钟 \_ 间隔 \_ 标记**](./ksevent-clock-interval-mark.md)。 这些事件在 DVD 播放期间需要同步时，向系统中的任何组件提供参考信息。 事件集的 GUID 为 [**KSEVENTSETID \_ 时钟**](./kseventsetid-clock.md)。

DVD 解码器微型驱动程序应检查是否有未完成的时钟事件。 典型的实现可能会检查针对每个视频开始代码生成的中断或针对 VSYNC 生成的中断的所有时钟事件。 提供以下事件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSEVENT_CLOCK_POSITION_MARK</p></td>
<td><p>此事件提供已超过指定的流时间的通知。 使用<a href="/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification" data-raw-source="[&lt;strong&gt;StreamClassStreamNotification&lt;/strong&gt;](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification)"><strong>StreamClassStreamNotification</strong></a>函数的<em>SignalStreamEvent</em>参数发出此事件的信号。 完成此调用后，不能将 <strong>KSEVENT_ENTRY</strong> 结构用于任何其他函数调用，包括对 <a href="/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassgetnextevent" data-raw-source="[&lt;strong&gt;StreamClassGetNextEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassgetnextevent)"><strong>StreamClassGetNextEvent</strong></a> 函数的调用。</p></td>
</tr>
<tr class="even">
<td><p>KSEVENT_CLOCK_INTERVAL_MARK</p></td>
<td><p>此事件在达到指定的开始时间之后，在指定的时间间隔内提供定期通知。</p></td>
</tr>
</tbody>
</table>

 

