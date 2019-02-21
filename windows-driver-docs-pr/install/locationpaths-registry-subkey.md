---
title: LocationPaths 注册表子项
description: LocationPaths 注册表子项
ms.assetid: d34ba7f4-97d2-4e63-a820-436c0336c584
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62970aff742d93ad3f4410ace59a506726a84a8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524372"
---
# <a name="locationpaths-registry-subkey"></a>LocationPaths 注册表子项


从 Windows 7 开始**LocationPaths**注册表子项中的可移动设备功能重写的规范通过硬件 Id 标识的设备使用) 都有可移动设备功能应用的重写。 重写有关可移动设备功能的详细信息，请参阅[DeviceOverrides 注册表项](deviceoverrides-registry-key.md)。

**LocationPaths**注册表子项适用于仅通过名称指定的设备的父 devnode **HardwareID**或**CompatibleID**子项。 因此，仅指定设备父 devnode 受可移动设备功能重写值。 指定设备的子 devnodes 不受影响的可移动设备功能重写时，除非[ChildLocationPaths](childlocationpaths-registry-subkey.md)还指定了注册表子项。

下表定义的格式和要求**LocationPaths**注册表子项。

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
<th align="left">子级子项</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>LocationPaths</strong></p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p><a href="hardwareid-registry-subkey.md" data-raw-source="[HardwareID](hardwareid-registry-subkey.md)">HardwareID</a>或<a href="compatibleid-registry-subkey.md" data-raw-source="[CompatibleID](compatibleid-registry-subkey.md)">CompatibleID</a></p></td>
<td align="left"><p><a href="locationpath-registry-subkey.md" data-raw-source="[LocationPath](locationpath-registry-subkey.md)">LocationPath</a>或 <a href="--registry-subkey.md" data-raw-source="[*](--registry-subkey.md)">*</a></p></td>
</tr>
</tbody>
</table>

 

任一**LocationPaths**或[ChildLocationPaths](childlocationpaths-registry-subkey.md)注册表子项必须存在以指示适用的可移动设备功能重写父/子关系。

 

 





