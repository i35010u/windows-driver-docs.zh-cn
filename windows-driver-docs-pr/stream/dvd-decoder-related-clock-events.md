---
title: 与 DVD 解码器相关的时钟事件
description: 与 DVD 解码器相关的时钟事件
ms.assetid: c3ed0ee4-95a3-4596-9f29-86397b0d8753
keywords:
- DVD 解码器微型驱动程序 WDK，主时钟
- 解码器微型驱动程序 WDK DVD，主时钟
- 主时钟 WDK DVD 解码器
- 时钟的 WDK DVD 解码器
- 事件的 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c842733a2c820ae76c10e3bb35e8f7721c008c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358426"
---
# <a name="dvd-decoder-related-clock-events"></a>与 DVD 解码器相关的时钟事件





任何支持主时钟的 DVD 播放的 DVD 解码器微型驱动程序流还必须支持以下两个时钟事件：[**KSEVENT\_时钟\_位置\_标记**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-clock-position-mark)并[ **KSEVENT\_时钟\_间隔\_标记**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-clock-interval-mark). 在需要同步播放 DVD 时的任何时间时，这些事件在系统中提供任何组件的参考的信息。 用于事件集的 guid [ **KSEVENTSETID\_时钟**](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-clock)。

DVD 解码器微型驱动程序应检查未完成的时钟事件。 典型的实现可能会检查所有时钟事件或中断生成 VSYNC 上为每个视频的起始代码，生成的中断。 提供了以下事件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Event</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSEVENT_CLOCK_POSITION_MARK</p></td>
<td><p>此事件提供了超过了指定的流时的通知。 使用终止此事件<em>SignalStreamEvent</em>参数<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassstreamnotification" data-raw-source="[&lt;strong&gt;StreamClassStreamNotification&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassstreamnotification)"> <strong>StreamClassStreamNotification</strong> </a>函数。 进行此调用后， <strong>KSEVENT_ENTRY</strong>结构可能不用于任何进一步的函数调用，其中包括对调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassgetnextevent" data-raw-source="[&lt;strong&gt;StreamClassGetNextEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassgetnextevent)"> <strong>StreamClassGetNextEvent</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td><p>KSEVENT_CLOCK_INTERVAL_MARK</p></td>
<td><p>在达到指定的开始时间后，此事件提供了在指定的时间间隔定期通知。</p></td>
</tr>
</tbody>
</table>

 

 

 




