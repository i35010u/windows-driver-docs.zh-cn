---
title: CompatibleID 注册表子项
description: CompatibleID 注册表子项
ms.assetid: 0111b013-d559-47bb-9cc8-d3930661a0a3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40a51cc5acaac5682ed2ba4f75b247fc23678fe0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544391"
---
# <a name="compatibleid-registry-subkey"></a>CompatibleID 注册表子项


从 Windows 7 开始**CompatibleID**注册表子项指定可移动设备功能的替代计算机上安装的设备。 重写有关可移动设备功能的详细信息，请参阅[DeviceOverrides 注册表项](deviceoverrides-registry-key.md)。

名称**CompatibleID**注册表子项指定[兼容 ID](compatible-ids.md)的设备，并设置的格式根据如下所述的要求。

下表定义的格式和要求**CompatibleID**注册表子项。

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
<td align="left"><p>有效<a href="compatible-ids.md" data-raw-source="[compatible ID](compatible-ids.md)">兼容 ID</a>值</p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>必须包括兼容 ID&#39;s 总线前缀。</p>
<p>兼容 ID 中的所有反斜杠 （） 路径分隔符字符必须替换为数字 （#） 字符。</p></td>
<td align="left"><a href="deviceoverrides-registry-key.md" data-raw-source="[DeviceOverrides](deviceoverrides-registry-key.md)">DeviceOverrides</a></td>
<td align="left"><p><a href="locationpaths-registry-subkey.md" data-raw-source="[LocationPaths](locationpaths-registry-subkey.md)">LocationPaths</a>和/或<a href="childlocationpaths-registry-subkey.md" data-raw-source="[ChildLocationPaths](childlocationpaths-registry-subkey.md)">ChildLocationPaths</a></p></td>
</tr>
</tbody>
</table>

 

兼容 ID 值必须遵循此表中所述的格式要求。 每个**CompatibleID**子项必须包含**LocationPaths**或**ChildLocationPaths**子项。 无法在中指定这两个子项**CompatbleID**子项如有必要。

由于包含斜杠字符不是注册表子项名称中的有效字符，您必须将其替换为数字的字符时指定的总线前缀**CompatibleID**注册表子项名称。 例如，如果可移动设备功能重写指定的设备节点 (*devnode*) 与[硬件 ID](hardware-ids.md) PCI 的\\VEN_ABCD DEV_1234 & SUBSYS_000，必须创建**CompatibleID**一个名为 PCI 的注册表子项\#VEN_ABCD DEV_1234 & SUBSYS_000。

 

 





