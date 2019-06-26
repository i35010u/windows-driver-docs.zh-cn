---
title: 外部传输属性
description: 外部传输属性
ms.assetid: e57e6c13-dfa3-4bec-9136-0e2bb2ffdd56
keywords:
- 外部传输属性 WDK 视频捕获
- 传输属性 WDK 视频捕获
- PROPSETID_EXT_TRANSPORT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11321e9e89c46cf09eeb3cf24619d45f01eaf3f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384102"
---
# <a name="external-transport-properties"></a>外部传输属性


[PROPSETID\_EXT\_传输](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-ext-transport)属性集包含从外部源，例如的信号进行传输和搜索到的类型的控制和传输数据相关的属性特定位置或时间的源媒体上的代码。 下表介绍的属性属于 PROPSETID\_EXT\_传输属性集。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_EXT_TRANSPORT KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-capabilities" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-capabilities)"><strong>KSPROPERTY_EXTXPORT_CAPABILITIES</strong></a></p></td>
<td><p>返回信息的功能的外部数据传输，如是否可以弹出设备的介质，或该设备可以向后播放。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-input-signal-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-input-signal-mode)"><strong>KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE</strong></a></p></td>
<td><p>如 525 行，60 赫兹 (NTSC) 标准定义 SD-DV 或 MPEG2 传输流控制传输中，输入的信号模式。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-output-signal-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_OUTPUT_SIGNAL_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-output-signal-mode)"><strong>KSPROPERTY_EXTXPORT_OUTPUT_SIGNAL_MODE</strong></a></p></td>
<td><p>控制输出信号模式的传输方式，例如 625 线条 50 赫兹 (PAL) MPEG。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-load-medium" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_LOAD_MEDIUM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-load-medium)"><strong>KSPROPERTY_EXTXPORT_LOAD_MEDIUM</strong></a></p></td>
<td><p>控制负载中的外部设备，如打开任务栏中，关闭送纸器，或弹出。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-medium-info" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_MEDIUM_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-medium-info)"><strong>KSPROPERTY_EXTXPORT_MEDIUM_INFO</strong></a></p></td>
<td><p>返回有关外部设备的介质，例如是否盒式磁带或磁盘，以及是否启用了写保护的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-state" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-state)"><strong>KSPROPERTY_EXTXPORT_STATE</strong></a></p></td>
<td><p>控制外部设备的传输模式和状态。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-state-notify" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_STATE_NOTIFY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-state-notify)"><strong>KSPROPERTY_EXTXPORT_STATE_NOTIFY</strong></a></p></td>
<td><p>控制的外部设备的传输模式下更改或其状态更改的通知。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-timecode-search" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_TIMECODE_SEARCH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-timecode-search)"><strong>KSPROPERTY_EXTXPORT_TIMECODE_SEARCH</strong></a></p></td>
<td><p>指定到搜索到，包括框架中，第二个、 分钟和小时的时间码。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-atn-search" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_ATN_SEARCH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-atn-search)"><strong>KSPROPERTY_EXTXPORT_ATN_SEARCH</strong></a></p></td>
<td><p>指定要在磁带上搜索到的绝对跟踪号。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-rtc-search" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_RTC_SEARCH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-rtc-search)"><strong>KSPROPERTY_EXTXPORT_RTC_SEARCH</strong></a></p></td>
<td><p>指定要在磁带上搜索到的相对时间计数器。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-raw-avc-cmd" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_RAW_AVC_CMD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-raw-avc-cmd)"><strong>KSPROPERTY_EXTXPORT_RAW_AVC_CMD</strong></a></p></td>
<td><p>控制要发送到外部设备的原始 AV/C 代码。</p></td>
</tr>
</tbody>
</table>

 

 

 




