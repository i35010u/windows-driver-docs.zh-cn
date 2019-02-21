---
title: 外部设备属性
description: 外部设备属性
ms.assetid: 633b24c7-a1da-4748-aaa2-864a01a3fd98
keywords:
- 外部设备属性 WDK 视频捕获
- PROPSETID_EXT_DEVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dc036620e340ed2fba5e4e234985cd925887c15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523404"
---
# <a name="external-device-properties"></a>外部设备属性


[PROPSETID\_EXT\_设备](https://msdn.microsoft.com/library/windows/hardware/ff567795)属性集包含与控件或外部设备，如摄像机或数字磁带卡片组的操作相关的属性。 下表介绍的属性属于 PROPSETID\_EXT\_设备属性集。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565153" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_ID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565153)"><strong>KSPROPERTY_EXTDEVICE_ID</strong></a></p></td>
<td><p>返回外部设备&#39;s 通用化系统范围 id。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565157" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_VERSION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565157)"><strong>KSPROPERTY_EXTDEVICE_VERSION</strong></a></p></td>
<td><p>返回外部设备的版本。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565155" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_POWER_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565155)"><strong>KSPROPERTY_EXTDEVICE_POWER_STATE</strong></a></p></td>
<td><p>控件外部设备，电源的状态如上等待状态，或关闭。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565154" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_PORT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565154)"><strong>KSPROPERTY_EXTDEVICE_PORT</strong></a></p></td>
<td><p>返回外部设备&#39;s 连接端口类型，例如 1394年或 USB。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565152" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565152)"><strong>KSPROPERTY_EXTDEVICE_CAPABILITIES</strong></a></p></td>
<td><p>返回是否可以记录设备，请等外部设备的功能都拥有视频功能和/或设备使用的文件。</p></td>
</tr>
</tbody>
</table>

 

 

 




