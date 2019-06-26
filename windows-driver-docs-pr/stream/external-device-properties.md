---
title: 外部设备属性
description: 外部设备属性
ms.assetid: 633b24c7-a1da-4748-aaa2-864a01a3fd98
keywords:
- 外部设备属性 WDK 视频捕获
- PROPSETID_EXT_DEVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17cffc125259090ff9f9d9848c082a04b08c09ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384088"
---
# <a name="external-device-properties"></a>外部设备属性


[PROPSETID\_EXT\_设备](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-ext-device)属性集包含与控件或外部设备，如摄像机或数字磁带卡片组的操作相关的属性。 下表介绍的属性属于 PROPSETID\_EXT\_设备属性集。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-id" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_ID&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-id)"><strong>KSPROPERTY_EXTDEVICE_ID</strong></a></p></td>
<td><p>返回外部设备的通用系统范围 id。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-version" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_VERSION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-version)"><strong>KSPROPERTY_EXTDEVICE_VERSION</strong></a></p></td>
<td><p>返回外部设备的版本。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-power-state" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_POWER_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-power-state)"><strong>KSPROPERTY_EXTDEVICE_POWER_STATE</strong></a></p></td>
<td><p>控件外部设备，电源的状态如上等待状态，或关闭。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-port" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_PORT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-port)"><strong>KSPROPERTY_EXTDEVICE_PORT</strong></a></p></td>
<td><p>返回外部设备的连接端口类型，例如 1394年或 USB。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-capabilities" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-capabilities)"><strong>KSPROPERTY_EXTDEVICE_CAPABILITIES</strong></a></p></td>
<td><p>返回是否可以记录设备，请等外部设备的功能都拥有视频功能和/或设备使用的文件。</p></td>
</tr>
</tbody>
</table>

 

 

 




