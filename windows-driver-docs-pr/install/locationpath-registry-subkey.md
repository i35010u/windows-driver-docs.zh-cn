---
title: LocationPath 注册表子项
description: LocationPath 注册表子项
ms.assetid: 3b6f3501-5969-453c-a04b-5559761c3222
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f76da6c69a25caf6c202ac76cbc0a0a55d71973
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356939"
---
# <a name="locationpath-registry-subkey"></a>LocationPath 注册表子项


从 Windows 7 开始**LocationPath**注册表子项指定用于通过标识的单个设备的可移动设备功能重写的位置路径[HardwareID](hardwareid-registry-subkey.md)或[CompatibleID](compatibleid-registry-subkey.md)注册表子项。 重写有关可移动设备功能的详细信息，请参阅[DeviceOverrides 注册表项](deviceoverrides-registry-key.md)。

**LocationPath**注册表子项将可移动设备功能值应用于仅设备节点 (*devnode*) 位于指定的位置路径。 这使可移动设备功能重写应用于系统中安装的设备的单个实例。 其他设备具有相同**HardwareID**或**CompatibleID**在其他位置路径不受此类可移动设备功能的重写。

按照约定，该位置路径字符串采用格式*ServiceName(BusSpecificLocation)*。 例如，PCI 设备使用 PCI (*XXYY*)，其中*XX*是设备号并*YY*是函数数。 该字符串是适用于相对于其总线的设备。 插即用 (PnP) 管理人员召集 devnode 树的每个节点的位置路径。 在树中每个 devnode 将连接到其父 devnode 提供的位置路径字符串的末尾其服务名称字符串。 因此，可以通过在位置路径唯一标识在树中的任何 devnode 位置。

下表定义的格式和要求**LocationPath**注册表子项。

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
<td align="left"><p>有效"<em>LocationPath</em>"值</p></td>
<td align="left"><p>可选 (* 或有效的位置路径必须存在以指示可移动设备功能的作用域重写)</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p><a href="locationpaths-registry-subkey.md" data-raw-source="[LocationPaths](locationpaths-registry-subkey.md)">LocationPaths</a>或<a href="childlocationpaths-registry-subkey.md" data-raw-source="[ChildLocationPaths](childlocationpaths-registry-subkey.md)">ChildLocationPaths</a></p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>

 

任一**LocationPath**或[ \* ](--registry-subkey.md)注册表子项必须存在以指示可移动设备功能的作用域重写。

**LocationPath**子项必须包含**可移动**DWORD 值，该值指定设备是否可移动。 下表定义的有效**可移动**值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">可移动的值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>Devnode 应被认为是不可移除</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>应为可移动视为 devnode</p></td>
</tr>
</tbody>
</table>

 

给定 devnode 的位置路径字符串可以显示通过设备管理器中完成以下步骤：

1.  打开设备管理器，找到注册表替代是要应用 devnode。 若要执行此操作，您可能需要将视图更改为**依连接排序设备**。

2.  右键单击 devnode，单击**属性**，然后单击**详细信息**选项卡。

3.  在中**属性**下拉列表中，找到**LocationPaths**属性。 此属性包含此 devnode 的位置路径字符串，是应遵循的值**LocationPath**注册表子项。

**请注意**  可能 devnode 不具有**LocationPaths**值。 这是因为此 devnode 或其父项之一的驱动程序不实现[GUID_PNP_LOCATION_INTERFACE](https://msdn.microsoft.com/library/windows/hardware/ff546564)接口。 在这种情况下，必须检查为父 devnode **LocationPaths**属性。

 

**LocationPaths**旨在使用重写了硬编码到固定的总线位置的设备的可移动设备功能的注册表子项。 这通常发生在便携式计算机，并包括以下设备：

-   无线网络适配器

-   Bluetooth 适配器

-   键盘或指针设备

在用户不能更改的固定位置的不同内部总线上存在这些设备。 **LocationPaths**替代允许您指定仅在给定的总线位置设备受影响的可移动设备功能重写。 这可以防止在重写会影响在其他可能会共享相同的总线位置的设备[HardwareID](hardwareid-registry-subkey.md)或[CompatibleID](compatibleid-registry-subkey.md)子项替代目标的值。 当仅指定设备时，这是常见**CompatibleID**子项值以匹配的收件箱驱动程序。

当你使用[ChildLocationPaths](childlocationpaths-registry-subkey.md)注册表子项来重写子 devnodes 的可移动设备功能通常很有用目标子 devnodes 仅在特定位置，而不管它们是何种设备。

例如，便携式计算机可能有内部和外部端口与内部 USB 集线器。 如果此 USB 集线器误报为外部其内部端口，在内部是硬编码到这些端口的任何设备是未正确识别为可移动。 同样，如果所有端口都误报为内部，如同它是便携式计算机 nondetachable 一部分处理任何外部连接的设备。

若要了解连接到的外部 USB 端口的设备的位置路径值，可以插入到端口的任何设备，并观察其位置路径属性。 插入到同一个端口的任何其他 USB 设备应收到相同的位置路径值，因为父总线以及如何在内部标识某个端口，永远不会更改。

 

 





