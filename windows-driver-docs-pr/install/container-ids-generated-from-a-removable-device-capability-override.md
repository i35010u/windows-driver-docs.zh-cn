---
title: 从可移动设备功能生成的容器 Id 重写
description: 从可移动设备功能生成的容器 Id 重写
ms.assetid: 8b1bf9d4-1aea-4d82-b783-f6dc62b9f8f3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9eb30a571422049762cc202a97c45e75d1b01a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525088"
---
# <a name="container-ids-generated-from-a-removable-device-capability-override"></a>从可移动设备功能生成的容器 Id 重写


从 Windows 7 开始，新设备应提供特定于总线的唯一 ID (如中所述[从特定于总线的唯一 ID 生成的容器 Id](container-ids-generated-from-a-bus-specific-unique-id.md))。

或者，设备和总线驱动程序必须可移动设备功能正确设置 (如中所述[从可移动设备功能生成的容器 Id](container-ids-generated-from-the-removable-device-capability.md))。 有关可移动设备功能的详细信息，请参阅[可移动设备功能的概述](overview-of-the-removable-device-capability.md)。

Windows 7 和更高版本的 Windows 还支持一种机制来重写的报告的可移动设备功能。 此机制可用于错误地报告了可移动设备功能的旧设备。

尽管替代机制不会更改可移动设备功能的值，它会强制 PnP 管理器中，替代设置而不是可移动设备功能的值生成时要使用设备的容器 Id。

通过这种替代机制，可以通过基于注册表的方法生成一个容器 ID。 只要为最顶层 （父） 设备节点生成的容器 ID (*devnode*) 中所述的试探法通过在设备每个子级 devnode 的设备，继承相同的容器 ID[容器 Id从可移动设备功能生成](container-ids-generated-from-the-removable-device-capability.md)。

替代机制是基于注册表的查找表包含映射到特定设备的注册表项。 此重写表下都保持[DeviceOverrides 注册表项](deviceoverrides-registry-key.md)，并且由以下注册表项和子项组成。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">表级别</th>
<th align="left">注册表子项密钥/名称</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p><a href="deviceoverrides-registry-key.md" data-raw-source="[DeviceOverrides](deviceoverrides-registry-key.md)">DeviceOverrides</a></p></td>
<td align="left"><p>重写所有可移动设备功能的父项。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><a href="hardwareid-registry-subkey.md" data-raw-source="[HardwareID](hardwareid-registry-subkey.md)">HardwareID</a></p></td>
<td align="left"><p>指定<a href="hardware-ids.md" data-raw-source="[hardware ID](hardware-ids.md)">硬件 ID</a>可移动设备功能重写的设备的应用。</p>
<p>此子项的名称是实际的硬件 ID，与所有反斜杠 (&#39;&#39;) 字符替换为的数字 (&#39;#&#39;) 字符。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p><a href="compatibleid-registry-subkey.md" data-raw-source="[CompatibleID](compatibleid-registry-subkey.md)">CompatibleID</a></p></td>
<td align="left"><p>指定<a href="compatible-ids.md" data-raw-source="[compatible ID](compatible-ids.md)">兼容 ID</a>可移动设备功能重写的设备的应用。</p>
<p>此子项的名称是实际的硬件 ID，与所有反斜杠 (&#39;&#39;) 字符替换为的数字 (&#39;#&#39;) 字符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p><a href="locationpaths-registry-subkey.md" data-raw-source="[LocationPaths](locationpaths-registry-subkey.md)">LocationPaths</a></p></td>
<td align="left"><p>指定仅在设备的位置路径&#39;s 父设备节点 (<a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-devnode" data-raw-source="&lt;em&gt;devnode&lt;/em&gt;"><em>devnode</em></a>) 将具有可移动设备功能重写应用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><a href="childlocationpaths-registry-subkey.md" data-raw-source="[ChildLocationPaths](childlocationpaths-registry-subkey.md)">ChildLocationPaths</a></p></td>
<td align="left"><p>指定设备的位置路径&#39;s 子 devnodes 会应用该可移动设备功能重写。</p>
<div class="alert">
<strong>请注意</strong>指定的设备父 devnode 不受影响的可移动设备功能重写时，除非<a href="locationpaths-registry-subkey.md" data-raw-source="[LocationPaths](locationpaths-registry-subkey.md)">LocationPaths</a>还指定了注册表子项或<strong>ChildLocationPaths</strong>为父 devnode 指定注册表子项。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p><a href="locationpath-registry-subkey.md" data-raw-source="[LocationPath](locationpath-registry-subkey.md)">LocationPath</a></p></td>
<td align="left"><p>指定应用的可移动设备功能重写的 devnode 离散位置路径。</p>
<p>此子项的名称是设备的单个 devnode 实例的计算机中安装的实际位置路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p><a href="--registry-subkey.md" data-raw-source="[*](--registry-subkey.md)">*</a></p></td>
<td align="left"><p>指定可移动设备功能重写应用于所有 devnodes 指定设备。</p></td>
</tr>
</tbody>
</table>

 

内[LocationPath](locationpath-registry-subkey.md)并[ \* ](--registry-subkey.md)注册表子项、 DWORD 值 (**可移动**) 指定适用 devnodes 是否被视为可移动（1） 或不可移动 (0)。

### <a href="" id="example-1"></a> 示例 1

下面的示例演示是设备的重写的匹配 devnode [HardwareID](hardwareid-registry-subkey.md)通过指定的注册表子项的位置路径除了[LocationPaths](locationpaths-registry-subkey.md)注册表子项。

在此示例中，重写将禁用可移动设备功能，并应用于具有的所有 devnodes[硬件 ID](hardware-ids.md)的 USB\\VID_1234 & 在位置路径 PCIROOT(0) PID_5678\#PCI (102)\#USBROOT(0)\#USB(1)。

下面是此重写的注册表表格格式的示例。

```cpp
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceOverrides
    USB#VID_1234&PID_5678
        LocationPaths
            PCIROOT(0)#PCI(102)#USBROOT(0)#USB(1)
                Removable=0
```

在此示例中，`USB#VID_1234&PID_5678 `的名称[HardwareID](hardwareid-registry-subkey.md)注册表子项和`PCIROOT(0)#PCI(102)#USBROOT(0)#USB(1)`的名称[LocationPath](locationpath-registry-subkey.md)注册表子项。

此替代将更改的设备拓扑插即用 (PnP) 管理器的解释。 请注意，与 devnode[硬件 ID](hardware-ids.md) USB 值\\VID_1234 & PID_5678 被标记为不可移除在注册表中。 因为即插即用管理器将解释为不可从其父可移动 devnode，没有此 devnode 生成新的容器 ID。 相反，USB\\VID_1234 & PID_5678 （及其所有子级） 继承其父容器 ID (ContainerID {A})。

此重写的结果是单个设备分组，因为在树中的所有 devnodes 都具有相同的容器 id。 设备 USB\\VID_1234 & PID_5678 被解释为与计算机集成。

下图显示了生成设备拓扑和关联容器 ID 分配。

![说明的可移动设备功能的关系图覆盖标记为不可移动 devnode](images/containerid-4.png)

上面的示例演示经常遇到的 devnode 拓扑： 使用设备硬编码到错误地将其自身报告为可移动的特定的总线位置的便携式计算机。 不会以物理方式集成在一起的计算机，如网络摄像机或生物特征 （指纹） 传感器的设备报告为可移动，因为用户不能从计算机时以物理方式分隔。 可移动的重写允许独立硬件供应商 (IHV) 或原始设备制造商 (OEM) 更改的即插即用的管理器如何解释可移动设备功能，并从而会影响设备的容器 ID 分配。

### <a name="example-2"></a>示例 2

下面显示了可移动设备功能替代的所有 devnodes 匹配特定[硬件 ID](hardware-ids.md)值。

在此示例中，重写将启用可移动设备功能，并替代应用于具有 USB 的硬件 ID 值的 devnodes\\VID_062A & PID_0000。

下面是此重写的注册表表格格式的高级说明。

```cpp
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceOverrides
    USB#VID_062A&PID_00001
        LocationPaths
            *
                Removable=1
```

1 的名称[HardwareID](hardwareid-registry-subkey.md)注册表子项。

在此示例中，使用 devnode[硬件 ID](hardware-ids.md)的 USB\\VID_1234 & PID_5678 正确报告设备可移动功能。 PnP 管理器生成，并且其所有子 devnodes 容器 ID (ContainerID {B})。

但是，与子 devnode[硬件 ID](hardware-ids.md)的 USB\\VID_062A & PID_0000 匹配重写。 因此，即插即用 manager 会生成此 devnode 和其所有子 devnodes 的另一个包含的 ID (ContainerID {C})。

为之前，此重写更改的设备拓扑的即插即用管理器的解释。 物理设备分配这两个容器 Id，并通过 Windows 将它视为两个设备。 请注意，与 devnode[硬件 ID](hardware-ids.md)的 USB\\VID_062A & PID_0000 被解释为可移动中分组 devnodes 到设备。 这不会更改设备可移动功能 devnode 报告的值。

此外，\*指定了注册表子项来指示，此重写应应用于计算机上具有的所有 devnodes[硬件 ID](hardware-ids.md) USB 的\\VID_062A & PID_0000。

下图显示了生成设备拓扑和关联容器 ID 分配。

![说明的可移动设备功能的关系图覆盖标记为可移动 devnode](images/containerid-5.png)

 

 





