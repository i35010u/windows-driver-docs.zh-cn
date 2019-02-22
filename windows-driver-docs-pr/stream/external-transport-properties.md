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
ms.openlocfilehash: eb48052c694e8e742f8d27133b450946e9e96b09
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542919"
---
# <a name="external-transport-properties"></a>外部传输属性


[PROPSETID\_EXT\_传输](https://msdn.microsoft.com/library/windows/hardware/ff567797)属性集包含从外部源，例如的信号进行传输和搜索到的类型的控制和传输数据相关的属性特定位置或时间的源媒体上的代码。 下表介绍的属性属于 PROPSETID\_EXT\_传输属性集。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565160" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565160)"><strong>KSPROPERTY_EXTXPORT_CAPABILITIES</strong></a></p></td>
<td><p>返回的信息的功能的外部数据传输，如是否在设备&#39;可以弹出 s 媒体，或该设备可以向后播放。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565161" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565161)"><strong>KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE</strong></a></p></td>
<td><p>如 525 行，60 赫兹 (NTSC) 标准定义 SD-DV 或 MPEG2 传输流控制传输中，输入的信号模式。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565165" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_OUTPUT_SIGNAL_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565165)"><strong>KSPROPERTY_EXTXPORT_OUTPUT_SIGNAL_MODE</strong></a></p></td>
<td><p>控制输出信号模式的传输方式，例如 625 线条 50 赫兹 (PAL) MPEG。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565162" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_LOAD_MEDIUM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565162)"><strong>KSPROPERTY_EXTXPORT_LOAD_MEDIUM</strong></a></p></td>
<td><p>控制负载中的外部设备，如打开任务栏中，关闭送纸器，或弹出。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565163" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_MEDIUM_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565163)"><strong>KSPROPERTY_EXTXPORT_MEDIUM_INFO</strong></a></p></td>
<td><p>返回外部设备有关的信息&#39;s 介质，例如是否盒式磁带或磁盘，以及是否启用了写保护。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565168" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565168)"><strong>KSPROPERTY_EXTXPORT_STATE</strong></a></p></td>
<td><p>控制外部设备&#39;s 传输模式和状态。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565169" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_STATE_NOTIFY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565169)"><strong>KSPROPERTY_EXTXPORT_STATE_NOTIFY</strong></a></p></td>
<td><p>控制外部设备的通知&#39;s 传输模式下更改或其状态的更改。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565170" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_TIMECODE_SEARCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565170)"><strong>KSPROPERTY_EXTXPORT_TIMECODE_SEARCH</strong></a></p></td>
<td><p>指定到搜索到，包括框架中，第二个、 分钟和小时的时间码。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565159" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_ATN_SEARCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565159)"><strong>KSPROPERTY_EXTXPORT_ATN_SEARCH</strong></a></p></td>
<td><p>指定要在磁带上搜索到的绝对跟踪号。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565166" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_RTC_SEARCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565166)"><strong>KSPROPERTY_EXTXPORT_RTC_SEARCH</strong></a></p></td>
<td><p>指定要在磁带上搜索到的相对时间计数器。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565214" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_RAW_AVC_CMD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565214)"><strong>KSPROPERTY_EXTXPORT_RAW_AVC_CMD</strong></a></p></td>
<td><p>控制要发送到外部设备的原始 AV/C 代码。</p></td>
</tr>
</tbody>
</table>

 

 

 




