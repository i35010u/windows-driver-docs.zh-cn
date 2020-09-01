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
ms.openlocfilehash: 1283f26e348f88eb9bbf69ce276ce7fc760ccd91
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188209"
---
# <a name="external-transport-properties"></a>外部传输属性


[PROPSETID \_ 扩展 \_ 传输](./propsetid-ext-transport.md)属性集包含与外部源中的数据的控制和传输相关的属性，例如传输的信号类型和搜索到特定位置或源媒体上的时间码。 下表描述了作为 PROPSETID \_ 扩展传输属性集的一部分的属性 \_ 。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-capabilities" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_CAPABILITIES&lt;/strong&gt;](./ksproperty-extxport-capabilities.md)"><strong>KSPROPERTY_EXTXPORT_CAPABILITIES</strong></a></p></td>
<td><p>返回有关外部数据传输功能的信息，例如是否可以弹出设备的媒体，或者设备能否向后播放。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-input-signal-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE&lt;/strong&gt;](./ksproperty-extxport-input-signal-mode.md)"><strong>KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE</strong></a></p></td>
<td><p>控制传输的输入信号模式，如525行、60赫兹 (NTSC) 标准定义 SD-DV 或 MPEG2 传输流。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-output-signal-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_OUTPUT_SIGNAL_MODE&lt;/strong&gt;](./ksproperty-extxport-output-signal-mode.md)"><strong>KSPROPERTY_EXTXPORT_OUTPUT_SIGNAL_MODE</strong></a></p></td>
<td><p>控制传输的输出信号模式，如625线路、50赫兹 (PAL) MPEG。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-load-medium" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_LOAD_MEDIUM&lt;/strong&gt;](./ksproperty-extxport-load-medium.md)"><strong>KSPROPERTY_EXTXPORT_LOAD_MEDIUM</strong></a></p></td>
<td><p>控制外部设备的负载介质，如 "打开"、"关闭" 或 "弹出"。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-medium-info" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_MEDIUM_INFO&lt;/strong&gt;](./ksproperty-extxport-medium-info.md)"><strong>KSPROPERTY_EXTXPORT_MEDIUM_INFO</strong></a></p></td>
<td><p>返回有关外部设备介质的信息，例如它是卡带磁带还是光盘，以及是否启用了写入保护。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-state" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_STATE&lt;/strong&gt;](./ksproperty-extxport-state.md)"><strong>KSPROPERTY_EXTXPORT_STATE</strong></a></p></td>
<td><p>控制外部设备的传输模式和状态。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-state-notify" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_STATE_NOTIFY&lt;/strong&gt;](./ksproperty-extxport-state-notify.md)"><strong>KSPROPERTY_EXTXPORT_STATE_NOTIFY</strong></a></p></td>
<td><p>控制外部设备的传输模式更改或其状态更改的通知。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-timecode-search" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_TIMECODE_SEARCH&lt;/strong&gt;](./ksproperty-extxport-timecode-search.md)"><strong>KSPROPERTY_EXTXPORT_TIMECODE_SEARCH</strong></a></p></td>
<td><p>指定要搜索的时间码，包括帧、秒、分钟和小时。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-atn-search" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_ATN_SEARCH&lt;/strong&gt;](./ksproperty-extxport-atn-search.md)"><strong>KSPROPERTY_EXTXPORT_ATN_SEARCH</strong></a></p></td>
<td><p>指定要在磁带上搜索的绝对磁道号。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-rtc-search" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_RTC_SEARCH&lt;/strong&gt;](./ksproperty-extxport-rtc-search.md)"><strong>KSPROPERTY_EXTXPORT_RTC_SEARCH</strong></a></p></td>
<td><p>指定要在磁带上搜索的相对时间计数器。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-raw-avc-cmd" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_RAW_AVC_CMD&lt;/strong&gt;](./ksproperty-raw-avc-cmd.md)"><strong>KSPROPERTY_EXTXPORT_RAW_AVC_CMD</strong></a></p></td>
<td><p>控制要发送到外部设备的原始 AV/C 代码。</p></td>
</tr>
</tbody>
</table>

 

 

