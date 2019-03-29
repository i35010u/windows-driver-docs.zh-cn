---
title: 调谐器属性
description: 调谐器属性
ms.assetid: 43a0c018-fb0e-4a45-9c9a-5896f1e728ac
keywords:
- 调谐器属性 WDK 视频捕获
- PROPSETID_TUNER
- 广播调谐器属性 WDK 视频捕获
- 电视调谐器属性 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ee3e1290f0a7bfd5ea775e47e55fd2d61c46f29
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350322"
---
# <a name="tuner-properties"></a>调谐器属性


[PROPSETID\_调谐器](https://msdn.microsoft.com/library/windows/hardware/ff567800)属性集包含与收音机和电视调谐器相关的属性。 下表描述了属于 PROPSETID 属性\_调谐器属性集。 第二个表描述了为运行 Windows Vista 及更高版本 AVStream 微型驱动程序实现的属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_TUNER KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565825" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565825)"><strong>KSPROPERTY_TUNER_CAPS</strong></a></p></td>
<td><p>返回的调谐器硬件，包括优化模式的支持，如电视和广播优化功能的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565833" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_FREQUENCY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565833)"><strong>KSPROPERTY_TUNER_FREQUENCY</strong></a></p></td>
<td><p>控制当前电视频道或射频。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565851" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_INPUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565851)"><strong>KSPROPERTY_TUNER_INPUT</strong></a></p></td>
<td><p>控制到调谐器设备，如同轴电缆或天线调谐器输入的输入。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565862" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565862)"><strong>KSPROPERTY_TUNER_MODE</strong></a></p></td>
<td><p>控制优化设备模式，如模拟电视、 数字电视、 广播或 DSS。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565865" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565865)"><strong>KSPROPERTY_TUNER_MODE_CAPS</strong></a></p></td>
<td><p>返回每个单独的优化模式的功能。 返回的模拟电视调谐器功能可以不同于优化功能，返回单选。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565907" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565907)"><strong>KSPROPERTY_TUNER_STANDARD</strong></a></p></td>
<td><p>返回模拟调谐器的标准，如 NTSC、 PAL 或 SECAM。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565921" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565921)"><strong>KSPROPERTY_TUNER_STATUS</strong></a></p></td>
<td><p>返回一个调谐器的过程，包括当前的频率、 PLL 偏移量和信号强度的当前状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565842" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_IF_MEDIUM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565842)"><strong>KSPROPERTY_TUNER_IF_MEDIUM</strong></a></p></td>
<td><p>返回支持数字电视调谐器设备的中间频率 pin 的 pin 介质。</p></td>
</tr>
</tbody>
</table>

 

下表描述了 PROPSETID\_调谐器属性适用于 Windows Vista 新增的。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_TUNER KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565887" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565887)"><strong>KSPROPERTY_TUNER_SCAN_CAPS</strong></a></p></td>
<td><p>返回支持广播的网络类型和优化设备是否可以支持信号扫描和有关扫描结果的通知。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565893" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565893)"><strong>KSPROPERTY_TUNER_SCAN_STATUS</strong></a></p></td>
<td><p>返回信号扫描的状态。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565909" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565909)"><strong>KSPROPERTY_TUNER_STANDARD_MODE</strong></a></p></td>
<td><p>控制是否将电视调谐器可以自动检测信号的调谐器的标准。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565881" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_NETWORKTYPE_SCAN_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565881)"><strong>KSPROPERTY_TUNER_NETWORKTYPE_SCAN_CAPS</strong></a></p></td>
<td><p>返回优化设备支持的特定广播的网络类型的扫描功能。</p></td>
</tr>
</tbody>
</table>

 

 

 




