---
title: HardwareID 注册表子项
description: HardwareID 注册表子项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b879f9d0559555bfd957495df8fcf295f80116bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791770"
---
# <a name="hardwareid-registry-subkey"></a>HardwareID 注册表子项


从 Windows 7 开始， **HardwareID** 注册表子项为计算机上安装的设备指定可移动设备功能替代。 有关可移动设备功能替代的详细信息，请参阅 [DeviceOverrides 注册表项](deviceoverrides-registry-key.md)。

**HardwareID** 注册表子项的名称指定设备的 [硬件 ID](hardware-ids.md) ，并根据下述要求进行格式化。

下表定义了 **HardwareID** 注册表子项的格式和要求。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">注册表子项名称</th>
<th align="left">必需/可选</th>
<th align="left">格式要求</th>
<th align="left">父键</th>
<th align="left">子子项</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>有效的 <a href="hardware-ids.md" data-raw-source="[hardware ID](hardware-ids.md)">硬件 ID</a> 值</p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>必须包含硬件 ID 的总线前缀。</p>
<p>必须将硬件 ID 内的所有反斜杠 ( # A1 路径分隔符替换为数字 ( # ) 字符。</p></td>
<td align="left"><a href="deviceoverrides-registry-key.md" data-raw-source="[DeviceOverrides](deviceoverrides-registry-key.md)">DeviceOverrides</a></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

硬件 ID 值必须遵循此表中所述的格式要求。 每个 **HardwareID** 子项必须包含 **LocationPaths** 或 **ChildLocationPaths** 子项。 必要时，可以在 **HardwareID** 子项中指定这两个子项。

由于斜杠字符在注册表子项名称中不是有效字符，因此，在为 **HardwareID** 注册表子项名称指定总线前缀时，必须将其替换为数字字符。 例如，如果为设备节点指定了可移动设备功能覆盖 (*devnode*) ， [硬件 ID](hardware-ids.md) 为 usb \\ VID_1234&PID_ABCD&REV_0001，则必须创建名称为 usb VID_1234&PID_ABCD&REV_0001 的 **HardwareID** 注册表子项 \# 。

 

 





