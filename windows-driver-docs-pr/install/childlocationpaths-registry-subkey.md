---
title: ChildLocationPaths 注册表子项
description: ChildLocationPaths 注册表子项
ms.assetid: 9c485981-e9f8-420d-9a87-d298b55356c4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9b1df40309d1743642e0f27b87d0871e992b7a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526668"
---
# <a name="childlocationpaths-registry-subkey"></a>ChildLocationPaths 注册表子项


从 Windows 7 开始**ChildLocationPaths** HardwareID 通过标识设备的可移动设备功能重写的规范中使用注册表子项) 将具有可移动设备应用功能重写。 重写有关可移动设备功能的详细信息，请参阅[DeviceOverrides 注册表项](deviceoverrides-registry-key.md)。

**ChildLocationPaths**注册表子项适用于只能通过父项的名称指定的设备的子 devnodes **HardwareID**或**CompatibleID**子项。 因此，仅指定设备子 devnodes 受可移动设备功能重写值。 指定设备父 devnode 不受影响的可移动设备功能重写时，除非[ **LocationPaths** ](locationpaths-registry-subkey.md)还指定了注册表子项或**ChildLocationPaths**为父 devnode 指定注册表子项。

下表定义的格式和要求**ChildLocationPaths**注册表子项。

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
<td align="left"><p><strong>ChildLocationPaths</strong></p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p><a href="hardwareid-registry-subkey.md" data-raw-source="[HardwareID](hardwareid-registry-subkey.md)">HardwareID</a>或<a href="compatibleid-registry-subkey.md" data-raw-source="[CompatibleID](compatibleid-registry-subkey.md)">CompatibleID</a></p></td>
<td align="left"><p><a href="locationpath-registry-subkey.md" data-raw-source="[LocationPath](locationpath-registry-subkey.md)">LocationPath</a>或 <a href="--registry-subkey.md" data-raw-source="[*](--registry-subkey.md)">*</a></p></td>
</tr>
</tbody>
</table>

 

**请注意**  任一[ **LocationPaths** ](locationpaths-registry-subkey.md)或者**ChildLocationPaths**注册表子项必须存在以指示父/子可移动设备功能重写应用到的关系。

 

 

 





