---
title: 调谐器属性
description: 调谐器属性
ms.assetid: 43a0c018-fb0e-4a45-9c9a-5896f1e728ac
keywords:
- 调谐器属性 WDK 视频捕获
- PROPSETID_TUNER
- 收音机调谐器属性 WDK 视频捕获
- 电视调谐器属性 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a5e2409965f9c4936191431d6c935e37343ecc6
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106316"
---
# <a name="tuner-properties"></a>调谐器属性


[PROPSETID \_ 调谐器](./propsetid-tuner.md)属性集包含与收音机和电视调谐器相关的属性。 下表描述了属于 PROPSETID \_ 调谐器属性集的属性。 第二个表描述了为在 Windows Vista 和更高版本上运行的 AVStream 微型驱动程序实现的属性。

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
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-tuner-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_CAPS&lt;/strong&gt;](./ksproperty-tuner-caps.md)"><strong>KSPROPERTY_TUNER_CAPS</strong></a></p></td>
<td><p>返回有关调谐器硬件功能的信息，包括支持的优化模式，如电视和收音机调谐。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-tuner-frequency" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_FREQUENCY&lt;/strong&gt;](./ksproperty-tuner-frequency.md)"><strong>KSPROPERTY_TUNER_FREQUENCY</strong></a></p></td>
<td><p>控制当前电视频道或射频。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-tuner-input" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_INPUT&lt;/strong&gt;](./ksproperty-tuner-input.md)"><strong>KSPROPERTY_TUNER_INPUT</strong></a></p></td>
<td><p>控制调谐器设备的输入，例如同轴电缆或天线调谐器输入。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-tuner-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE&lt;/strong&gt;](./ksproperty-tuner-mode.md)"><strong>KSPROPERTY_TUNER_MODE</strong></a></p></td>
<td><p>控制优化设备模式，例如模拟电视、数字电视、广播或 DSS。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-tuner-mode-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE_CAPS&lt;/strong&gt;](./ksproperty-tuner-mode-caps.md)"><strong>KSPROPERTY_TUNER_MODE_CAPS</strong></a></p></td>
<td><p>返回各个优化模式的功能。 返回的模拟电视调谐器功能可能不同于返回的无线电调谐功能。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-tuner-standard" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD&lt;/strong&gt;](./ksproperty-tuner-standard.md)"><strong>KSPROPERTY_TUNER_STANDARD</strong></a></p></td>
<td><p>返回模拟调谐器的标准，例如 NTSC、PAL 或 SECAM。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-tuner-status" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STATUS&lt;/strong&gt;](./ksproperty-tuner-status.md)"><strong>KSPROPERTY_TUNER_STATUS</strong></a></p></td>
<td><p>返回调谐器进程的当前状态，包括当前频率、PLL 偏移量和信号强度。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-tuner-if-medium" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_IF_MEDIUM&lt;/strong&gt;](./ksproperty-tuner-if-medium.md)"><strong>KSPROPERTY_TUNER_IF_MEDIUM</strong></a></p></td>
<td><p>对于支持数字电视的调谐器设备，返回中间频率引脚的 pin 媒体。</p></td>
</tr>
</tbody>
</table>

 

下表描述了 \_ 适用于 Windows Vista 的 PROPSETID 调谐器属性。

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
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-tuner-scan-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_CAPS&lt;/strong&gt;](./ksproperty-tuner-scan-caps.md)"><strong>KSPROPERTY_TUNER_SCAN_CAPS</strong></a></p></td>
<td><p>返回支持的广播网络类型，以及优化设备是否可支持有关扫描结果的信号扫描和通知。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-tuner-scan-status" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_STATUS&lt;/strong&gt;](./ksproperty-tuner-scan-status.md)"><strong>KSPROPERTY_TUNER_SCAN_STATUS</strong></a></p></td>
<td><p>返回信号扫描的状态。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-tuner-standard-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD_MODE&lt;/strong&gt;](./ksproperty-tuner-standard-mode.md)"><strong>KSPROPERTY_TUNER_STANDARD_MODE</strong></a></p></td>
<td><p>控制调谐器是否可以根据信号自动检测调谐器的标准。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-tuner-networktype-scan-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_NETWORKTYPE_SCAN_CAPS&lt;/strong&gt;](./ksproperty-tuner-networktype-scan-caps.md)"><strong>KSPROPERTY_TUNER_NETWORKTYPE_SCAN_CAPS</strong></a></p></td>
<td><p>返回优化设备支持的特定广播网络类型的扫描功能。</p></td>
</tr>
</tbody>
</table>

 

