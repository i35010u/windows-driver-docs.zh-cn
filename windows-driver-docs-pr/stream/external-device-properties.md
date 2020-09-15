---
title: 外部设备属性
description: 外部设备属性
ms.assetid: 633b24c7-a1da-4748-aaa2-864a01a3fd98
keywords:
- 外部设备属性 WDK 视频捕获
- PROPSETID_EXT_DEVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a750dd6e740128846e65afb737082893c97e402
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107126"
---
# <a name="external-device-properties"></a>外部设备属性


[PROPSETID \_ EXT \_ 设备](./propsetid-ext-device.md)属性集包含与外部设备（如摄像机或数字磁带卡座）的控件或操作相关的属性。 下表描述了属于 PROPSETID \_ EXT \_ 设备属性集的属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_EXT_DEVICE KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-extdevice-id" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_ID&lt;/strong&gt;](./ksproperty-extdevice-id.md)"><strong>KSPROPERTY_EXTDEVICE_ID</strong></a></p></td>
<td><p>返回外部设备通用化系统范围内的 ID。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-extdevice-version" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_VERSION&lt;/strong&gt;](./ksproperty-extdevice-version.md)"><strong>KSPROPERTY_EXTDEVICE_VERSION</strong></a></p></td>
<td><p>返回外部设备的版本。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-extdevice-power-state" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_POWER_STATE&lt;/strong&gt;](./ksproperty-extdevice-power-state.md)"><strong>KSPROPERTY_EXTDEVICE_POWER_STATE</strong></a></p></td>
<td><p>控制外部设备的电源状态，如 "打开"、"备用" 或 "关闭"。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-extdevice-port" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_PORT&lt;/strong&gt;](./ksproperty-extdevice-port.md)"><strong>KSPROPERTY_EXTDEVICE_PORT</strong></a></p></td>
<td><p>返回外部设备的连接端口类型，如1394或 USB。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-extdevice-capabilities" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_CAPABILITIES&lt;/strong&gt;](./ksproperty-extdevice-capabilities.md)"><strong>KSPROPERTY_EXTDEVICE_CAPABILITIES</strong></a></p></td>
<td><p>返回外部设备的功能，例如设备是否可以记录、拥有视频功能和/或设备是否使用文件。</p></td>
</tr>
</tbody>
</table>

 

