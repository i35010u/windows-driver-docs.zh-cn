---
title: ChildLocationPaths 注册表子项
description: ChildLocationPaths 注册表子项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 465c7e9fcee44873469e98f162dab7279958d790
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787525"
---
# <a name="childlocationpaths-registry-subkey"></a>ChildLocationPaths 注册表子项


从 Windows 7 开始， **ChildLocationPaths** 注册表子项用于通过 [HardwareID](hardwareid-registry-subkey.md) 或 [CompatibleID](compatibleid-registry-subkey.md) 注册表子项识别的设备的可移动设备功能替代规范。 **ChildLocationPaths** 注册表子项指定只有设备的子设备节点的位置路径 (*devnodes*) 才能应用可移动设备功能覆盖。 有关可移动设备功能替代的详细信息，请参阅 [DeviceOverrides 注册表项](deviceoverrides-registry-key.md)。

**ChildLocationPaths** 注册表子项仅适用于通过父 **HardwareID** 或 **CompatibleID** 子项的名称指定的设备的子 devnodes。 因此，只有指定设备的子 devnodes 受可移动设备功能覆盖值的影响。 指定设备的父 devnode 不受可移动设备功能覆盖的影响，除非还指定了 [**LocationPaths**](locationpaths-registry-subkey.md) 注册表子项或为父 devnode 指定了 **ChildLocationPaths** 注册表子项。

下表定义了 **ChildLocationPaths** 注册表子项的格式和要求。

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
<th align="left">父子项</th>
<th align="left">子子项</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ChildLocationPaths</strong></p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p><a href="hardwareid-registry-subkey.md" data-raw-source="[HardwareID](hardwareid-registry-subkey.md)">HardwareID</a> 或 <a href="compatibleid-registry-subkey.md" data-raw-source="[CompatibleID](compatibleid-registry-subkey.md)">CompatibleID</a></p></td>
<td align="left"><p><a href="locationpath-registry-subkey.md" data-raw-source="[LocationPath](locationpath-registry-subkey.md)">LocationPath</a> 或 <a href="--registry-subkey.md" data-raw-source="[*](--registry-subkey.md)">*</a></p></td>
</tr>
</tbody>
</table>

 

**注意**  必须存在 [**LocationPaths**](locationpaths-registry-subkey.md) 或 **ChildLocationPaths** 注册表子项，才能指示可移动设备功能覆盖适用的父/子关系。

 

 

 





