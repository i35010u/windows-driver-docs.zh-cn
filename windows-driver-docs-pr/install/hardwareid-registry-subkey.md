---
title: HardwareID 注册表子项
description: HardwareID 注册表子项
ms.assetid: c6c52aa1-68ee-4d64-be97-509203db6970
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b12f89fb71ef18c2cdeadd3e03caacc67d84f4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330910"
---
# <a name="hardwareid-registry-subkey"></a>HardwareID 注册表子项


从 Windows 7 开始**HardwareID**注册表子项指定可移动设备功能的替代计算机上安装的设备。 重写有关可移动设备功能的详细信息，请参阅[DeviceOverrides 注册表项](deviceoverrides-registry-key.md)。

名称**HardwareID**注册表子项指定[硬件 ID](hardware-ids.md)的设备，并设置的格式根据如下所述的要求。

下表定义的格式和要求**HardwareID**注册表子项。

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
<th align="left">父项</th>
<th align="left">子级子项</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>有效<a href="hardware-ids.md" data-raw-source="[hardware ID](hardware-ids.md)">硬件 ID</a>值</p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>必须包括硬件 ID 总线前缀。</p>
<p>所有正斜杠 （） 中的硬件 ID 必须替换为数字 （#） 字符的路径分隔符字符。</p></td>
<td align="left"><a href="deviceoverrides-registry-key.md" data-raw-source="[DeviceOverrides](deviceoverrides-registry-key.md)">DeviceOverrides</a></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

硬件 ID 值必须遵循此表中所述的格式要求。 每个**HardwareID**子项必须包含**LocationPaths**或**ChildLocationPaths**子项。 无法在中指定这两个子项**HardwareID**子项如有必要。

由于包含斜杠字符不是注册表子项名称中的有效字符，您必须将其替换为数字的字符时指定的总线前缀**HardwareID**注册表子项名称。 例如，如果可移动设备功能重写指定的设备节点 (*devnode*) 与[硬件 ID](hardware-ids.md)的 USB\\VID_1234 PID_ABCD & REV_0001，必须创建**HardwareID** USB 同名的注册表子项\#VID_1234 PID_ABCD & REV_0001。

 

 





