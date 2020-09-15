---
title: 从可移动设备功能覆盖生成的容器 Id
description: 通过可移动设备功能重写生成的容器 ID
ms.assetid: 8b1bf9d4-1aea-4d82-b783-f6dc62b9f8f3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fc94fc0756ca7ce542615a7a37010bc2c42b8c5
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104928"
---
# <a name="container-ids-generated-from-a-removable-device-capability-override"></a>通过可移动设备功能重写生成的容器 ID


从 Windows 7 开始，新设备应提供特定于总线的唯一 ID (如 [从特定于总线的唯一 Id 生成的容器 id](container-ids-generated-from-a-bus-specific-unique-id.md)) 所述。

或者，设备和总线驱动程序必须正确设置可移动设备功能， (如 [从可移动设备功能) 生成的容器 id](container-ids-generated-from-the-removable-device-capability.md) 中所述。 有关可移动设备功能的详细信息，请参阅 [可移动设备功能的概述](overview-of-the-removable-device-capability.md)。

Windows 7 及更高版本的 Windows 还支持替代所报告的可移动设备功能的机制。 此机制适用于报告可移动设备功能错误的旧式设备。

尽管替代机制不会更改可移动设备功能的值，但它会强制 PnP 管理器使用替代设置，而不是在为设备生成容器 Id 时使用可移动设备功能的值。

通过此重写机制，可以通过基于注册表的方法生成容器 ID。 一旦为 (父) 设备节点的最顶层父设备 *)  (节点* 生成容器 id，则设备的每个子 devnode 都将使用相同的容器 id，该 id 通过 [从可移动设备功能生成的容器 id](container-ids-generated-from-the-removable-device-capability.md)中所述的试探法来继承。

替代机制是基于注册表的查找表，它包含映射到特定设备的注册表项。 此替代表将保留在 [DeviceOverrides 注册表项](deviceoverrides-registry-key.md)下，并由以下注册表项和子项组成。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">表级别</th>
<th align="left">注册表项/子项名称</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p><a href="deviceoverrides-registry-key.md" data-raw-source="[DeviceOverrides](deviceoverrides-registry-key.md)">DeviceOverrides</a></p></td>
<td align="left"><p>所有可移动设备功能重写的父键。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><a href="hardwareid-registry-subkey.md" data-raw-source="[HardwareID](hardwareid-registry-subkey.md)">HardwareID</a></p></td>
<td align="left"><p>指定可移动设备功能覆盖适用于的设备的 <a href="hardware-ids.md" data-raw-source="[hardware ID](hardware-ids.md)">硬件 ID</a> 。</p>
<p>此子项的名称是实际的硬件 ID，其中所有反斜杠 ( "" ) 字符由 number ( "#" ) 字符所替换。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p><a href="compatibleid-registry-subkey.md" data-raw-source="[CompatibleID](compatibleid-registry-subkey.md)">CompatibleID</a></p></td>
<td align="left"><p>指定可移动设备功能覆盖适用于的设备的 <a href="compatible-ids.md" data-raw-source="[compatible ID](compatible-ids.md)">兼容 ID</a> 。</p>
<p>此子项的名称是实际的硬件 ID，其中所有反斜杠 ( "" ) 字符由 number ( "#" ) 字符所替换。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p><a href="locationpaths-registry-subkey.md" data-raw-source="[LocationPaths](locationpaths-registry-subkey.md)">LocationPaths</a></p></td>
<td align="left"><p>指定只有设备父设备节点的位置路径 (<a href="/windows-hardware/drivers/#wdkgloss-devnode" data-raw-source="&lt;em&gt;devnode&lt;/em&gt;"><em>devnode</em></a>) 才能应用可移动设备功能覆盖。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><a href="childlocationpaths-registry-subkey.md" data-raw-source="[ChildLocationPaths](childlocationpaths-registry-subkey.md)">ChildLocationPaths</a></p></td>
<td align="left"><p>指定设备的子 devnodes 的位置路径将应用可移动设备功能覆盖。</p>
<div class="alert">
<strong>注意</strong>  指定设备的父 devnode 不受可移动设备功能覆盖的影响，除非还指定了 <a href="locationpaths-registry-subkey.md" data-raw-source="[LocationPaths](locationpaths-registry-subkey.md)">LocationPaths</a> 注册表子项或为父 devnode 指定了 <strong>ChildLocationPaths</strong> 注册表子项。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p><a href="locationpath-registry-subkey.md" data-raw-source="[LocationPath](locationpath-registry-subkey.md)">LocationPath</a></p></td>
<td align="left"><p>指定可移动设备功能覆盖适用于 devnode 的离散位置路径。</p>
<p>此子项的名称是计算机上安装的单个 devnode 实例的实际位置路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p><a href="--registry-subkey.md" data-raw-source="[*](--registry-subkey.md)">*</a></p></td>
<td align="left"><p>指定可移动设备功能覆盖适用于指定设备的所有 devnodes。</p></td>
</tr>
</tbody>
</table>

 

在 [LocationPath](locationpath-registry-subkey.md) 和 [\*](--registry-subkey.md) registry 子项中，DWORD 值 (**可移动**) 指定是否将适用的 devnodes 视为可移动 (1) 或非可移动 (0) 。

### <a name="example-1"></a><a href="" id="example-1"></a> 示例1

下面显示了与 [HardwareID](hardwareid-registry-subkey.md) 注册表子项匹配的 devnode 的设备替代，以及通过 [LocationPaths](locationpaths-registry-subkey.md) 注册表子项指定的位置路径。

在此示例中，重写将禁用可移动设备功能，并将其应用于&位置路径为 USB VID_1234 的 [硬件 ID](hardware-ids.md) 为 USB 的所有 devnodes \\ PID_5678 (0) \# PCI (102) \# USBROOT (0) \# USB (1) 。

下面是此替代的注册表表格式的示例。

```cpp
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceOverrides
    USB#VID_1234&PID_5678
        LocationPaths
            PCIROOT(0)#PCI(102)#USBROOT(0)#USB(1)
                Removable=0
```

在此示例中， `USB#VID_1234&PID_5678 ` 是 [HardwareID](hardwareid-registry-subkey.md) 注册表子项的名称， `PCIROOT(0)#PCI(102)#USBROOT(0)#USB(1)` 是 [LocationPath](locationpath-registry-subkey.md) 注册表子项的名称。

此重写将更改设备拓扑的即插即用 (PnP) 管理器的解释。 请注意，devnode 的 [硬件 ID](hardware-ids.md) 值为 USB \\ VID_1234&PID_5678 的在注册表中被标记为不可移动。 不会为此 devnode 生成新的容器 ID，因为 PnP 管理器会将 devnode 解释为无法从其父项移动。 相反，USB \\ VID_1234&PID_5678 (及其所有子项) 继承其父级 (ContainerID {A} ) 的容器 ID。

此重写的结果是单个设备分组，因为树中的所有 devnodes 具有相同的容器 ID。 设备 USB \\ VID_1234&PID_5678 被解释为与计算机集成。

下图显示了生成的设备拓扑和关联的容器 ID 分配。

![说明将 devnode 标记为不可删除的可移动设备功能替代的关系图](images/containerid-4.png)

前面的示例显示了经常遇到的 devnode 拓扑：设备硬编码到特定总线位置的便携式计算机，这些设备不正确地报告为可移动。 与计算机进行物理集成的设备（如网络摄像机或生物识别 (指纹) 传感器）不应报告为可移动设备，因为用户不能从物理上将它们与计算机进行区分。 可移动替代允许独立硬件供应商 (IHV) 或原始设备制造商 (OEM) 更改 PnP 管理器解释可移动设备功能的方式，从而影响设备的容器 ID 分配。

### <a name="example-2"></a>示例 2

下面显示了所有与特定 [硬件 ID](hardware-ids.md) 值匹配的 devnodes 的可移动设备功能重写。

在此示例中，重写将启用可移动设备功能，并将替代应用于硬件 ID 值为 USB \\ VID_062A&PID_0000 的 devnodes。

下面是此替代的注册表表格式的高级说明。

```cpp
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceOverrides
    USB#VID_062A&PID_00001
        LocationPaths
            *
                Removable=1
```

1 [HardwareID](hardwareid-registry-subkey.md) 注册表子项的名称。

在此示例中，devnode [硬件 ID](hardware-ids.md) 为 USB \\ VID_1234&PID_5678 报告设备可移动功能正确。 PnP 管理器会为其及其所有子 devnodes 生成一个容器 ID (ContainerID {B} ) 。

但是，具有 USB VID_062A&PID_0000 [硬件 ID](hardware-ids.md) 的子 devnode \\ 与替代。 因此，PnP 管理器会为此 devnode 及其所有子 devnodes 生成另一个包含的 ID (ContainerID {C} ) 。

与之前一样，此替代更改 PnP 管理器对设备拓扑的解释。 为物理设备分配了两个容器 Id，Windows 将其视为两个设备。 请注意，devnode 的 [硬件 ID](hardware-ids.md) 为 USB \\ VID_062A&PID_0000 的在将 devnodes 分组到设备中时被解释为可移动。 这不会更改 devnode 为设备可移动功能报告的值。

此外， \* 指定了注册表子项以指示应将此替代应用于计算机上的所有 devnodes，该计算机上的 [硬件 ID](hardware-ids.md) 为 USB \\ VID_062A&PID_0000。

下图显示了生成的设备拓扑和关联的容器 ID 分配。

![说明将 devnode 标记为可移动的可移动设备功能替代的关系图](images/containerid-5.png)

 

