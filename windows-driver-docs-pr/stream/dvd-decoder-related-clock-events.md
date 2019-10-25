---
title: 与 DVD 解码器相关的时钟事件
description: 与 DVD 解码器相关的时钟事件
ms.assetid: c3ed0ee4-95a3-4596-9f29-86397b0d8753
keywords:
- DVD 解码器微型驱动程序 WDK，主时钟
- 解码器微型驱动程序 WDK DVD，主时钟
- 主时钟 WDK DVD 解码器
- 时钟 WDK DVD 解码器
- 事件 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d88d80085b82f2a58f6a690bd86a41b6fd392326
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843217"
---
# <a name="dvd-decoder-related-clock-events"></a>与 DVD 解码器相关的时钟事件





支持 DVD 播放的主时钟的任何 DVD 解码器微型驱动程序流还必须支持以下两个时钟事件： [**KSEVENT\_时钟\_位置\_标记**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-clock-position-mark)和[**KSEVENT\_时钟\_间隔\_MARK**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-clock-interval-mark)。 这些事件在 DVD 播放期间需要同步时，向系统中的任何组件提供参考信息。 事件集的 GUID 是[**KSEVENTSETID\_时钟**](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-clock)。

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
<td><p>此事件提供已超过指定的流时间的通知。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification" data-raw-source="[&lt;strong&gt;StreamClassStreamNotification&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification)"><strong>StreamClassStreamNotification</strong></a>函数的<em>SignalStreamEvent</em>参数发出此事件的信号。 完成此调用后， <strong>KSEVENT_ENTRY</strong>结构可能不用于任何其他函数调用，包括对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassgetnextevent" data-raw-source="[&lt;strong&gt;StreamClassGetNextEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassgetnextevent)"><strong>StreamClassGetNextEvent</strong></a>函数的调用。</p></td>
</tr>
<tr class="even">
<td><p>KSEVENT_CLOCK_INTERVAL_MARK</p></td>
<td><p>此事件在达到指定的开始时间之后，在指定的时间间隔内提供定期通知。</p></td>
</tr>
</tbody>
</table>

 

 

 




