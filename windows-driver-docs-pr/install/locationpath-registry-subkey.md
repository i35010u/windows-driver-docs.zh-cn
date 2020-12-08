---
title: LocationPath 注册表子项
description: LocationPath 注册表子项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13b52f255e18bc90d2f41b96b8503ebc729e4844
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808695"
---
# <a name="locationpath-registry-subkey"></a>LocationPath 注册表子项


从 Windows 7 开始， **LocationPath** 注册表子项为通过 [HardwareID](hardwareid-registry-subkey.md) 或 [CompatibleID](compatibleid-registry-subkey.md) 注册表子项识别的单个设备指定可移动设备功能覆盖的位置路径。 有关可移动设备功能替代的详细信息，请参阅 [DeviceOverrides 注册表项](deviceoverrides-registry-key.md)。

**LocationPath** 注册表子项仅将可移动设备功能值应用于指定位置路径 (*devnode*) 的设备节点。 这使可移动设备功能重写应用到系统中安装的单个设备实例。 其他位置路径上具有相同 **HardwareID** 或 **CompatibleID** 的其他设备不受此类可移动设备功能重写的影响。

按照约定，location 路径字符串采用的格式为 *ServiceName (BusSpecificLocation)*。 例如，PCI 设备使用 PCI (*XXYY*) ，其中 *XX* 是设备号， *YY* 是函数号。 该字符串相对于其总线而言是唯一的。 即插即用 (PnP) manager 在 devnode 树中汇编每个节点的位置路径。 树中的每个 devnode 将其服务名称字符串连接到其父 devnode 提供的位置路径字符串的末尾。 因此，可以通过位置路径唯一地标识树中的任何 devnode 的位置。

下表定义了 **LocationPath** 注册表子项的格式和要求。

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
<td align="left"><p>有效的 "<em>LocationPath</em>" 值</p></td>
<td align="left"><p>可选 ( * 或者必须存在有效的位置路径才能指示可移动设备功能覆盖的作用域) </p></td>
<td align="left"><p>无</p></td>
<td align="left"><p><a href="locationpaths-registry-subkey.md" data-raw-source="[LocationPaths](locationpaths-registry-subkey.md)">LocationPaths</a> 或 <a href="childlocationpaths-registry-subkey.md" data-raw-source="[ChildLocationPaths](childlocationpaths-registry-subkey.md)">ChildLocationPaths</a></p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>

 

必须存在 **LocationPath** 或 [\*](--registry-subkey.md) 注册表子项，才能指示可移动设备功能重写的作用域。

**LocationPath** 子项必须包含 **可移动** DWORD 值，该值指定设备是否可移动。 下表定义了有效的 **可移动** 值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">可移动值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>Devnode 应视为不可删除</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>Devnode 应视为可移动</p></td>
</tr>
</tbody>
</table>

 

可以通过以下步骤设备管理器显示给定 devnode 的位置路径字符串：

1.  打开设备管理器并找到要应用注册表替代的 devnode。 为此，可能需要将视图更改为 " **按连接的设备**"。

2.  右键单击 devnode，再单击 " **属性** "，然后单击 " **详细信息** " 选项卡。

3.  在 **属性** 下拉列表中，找到 **LocationPaths** 属性。 此属性包含此 devnode 的位置路径字符串，是应用于 **LocationPath** 注册表子项的值。

**注意**  Devnode 可能没有 **LocationPaths** 值。 这是因为此 devnode 的驱动程序或其父项的驱动程序未实现 [GUID_PNP_LOCATION_INTERFACE](https://msdn.microsoft.com/library/windows/hardware/ff546564) 接口。 在这种情况下，必须检查父 devnode 是否有 **LocationPaths** 属性。

 

**LocationPaths** 注册表子项旨在用于替代硬编码为固定总线位置的设备的可移动设备功能。 这通常发生在便携式计算机中，包括以下设备：

-   无线网络适配器

-   蓝牙适配器

-   键盘或指针设备

这些设备存在于用户无法更改的固定位置的不同内部总线上。 **LocationPaths** 替代使你能够指定只有给定总线位置的设备受可移动设备功能重写的影响。 这可防止重写影响其他总线位置上的设备，该总线位置可能与替代目标共享相同的 [HardwareID](hardwareid-registry-subkey.md) 或 [CompatibleID](compatibleid-registry-subkey.md) 子项值。 当设备仅指定 **CompatibleID** 子项值来匹配收件箱驱动程序时，这种情况很常见。

当你使用 [ChildLocationPaths](childlocationpaths-registry-subkey.md) 注册表子项替代子 devnodes 的可移动设备功能时，无论它们属于哪种设备，通常都仅针对特定位置的子 devnodes。

例如，便携式计算机可能具有内部和外部端口的内部 USB 集线器。 如果此 USB 集线器 misreporting 其内部端口为外部端口，则在内部硬编码到这些端口的任何设备均被错误地识别为可移动。 同样，如果所有端口都 misreported 为内部端口，则会将任何外部连接的设备视为便携式计算机的 nondetachable 部分。

若要发现连接到外部 USB 端口的设备的位置路径值，可以将任何设备插入端口并观察其位置路径属性。 插入同一端口的任何其他 USB 设备应该接收相同的位置路径值，因为父总线和它在内部如何识别端口从不会发生更改。

 

 





