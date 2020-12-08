---
title: DeviceOverrides 注册表项
description: DeviceOverrides 注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7837d7ca391b16e4bbd5d370962442217ced01fb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827685"
---
# <a name="deviceoverrides-registry-key"></a>DeviceOverrides 注册表项


从 Windows 7 开始， **DeviceOverrides** 注册表项指定系统中存在一个或多个可移动设备功能重写。 有关可移动设备功能的详细信息，请参阅 [可移动设备功能的概述](overview-of-the-removable-device-capability.md)。

即插即用 (PnP) 管理器使用 ([容器 id](container-ids.md) 的新 *ID) 将* 源自于的一个或多个设备节点组合到计算机上安装的特定物理设备的每个实例。 对于旧设备，PnP 管理器通过可移动设备功能生成容器 Id。 有关 PnP 管理器如何生成容器 Id 的详细信息，请参阅 [如何生成容器 id](how-container-ids-are-generated.md)。

可移动设备功能替代允许独立硬件供应商 (IHV) 或原始设备制造商 (OEM) 更改 devnode 或 devnodes 的可移动设备功能的解释值。

通过 **DeviceOverrides** 注册表项的可移动设备功能重写对于可能无法正确报告可移动设备功能的旧设备或第三方硬件组件非常有用。 这会导致 PnP 管理器错误地生成用于对从物理设备枚举的 devnodes 进行分组的容器 ID。

这些替代实际上不会更改 devnode 报告的可移动设备功能的全局状态。 相反，这些替代会导致 PnP 管理器忽略所报告的设备功能，并在为与替代的 devnodes 生成 [容器 ID](container-ids.md) 时使用基于注册表的设置。 DeviceOverrides 注册表子项下的其他子项更详细地介绍了要重写哪些 devnodes。

下表定义了 **DeviceOverrides** 注册表项的格式和要求。

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
<th align="left">注册表项名称</th>
<th align="left">必需/可选</th>
<th align="left">格式要求</th>
<th align="left">父键</th>
<th align="left">子子项</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>DeviceOverrides</strong></p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p><a href="hardwareid-registry-subkey.md" data-raw-source="[HardwareID](hardwareid-registry-subkey.md)">HardwareID</a> 或 <a href="compatibleid-registry-subkey.md" data-raw-source="[CompatibleID](compatibleid-registry-subkey.md)">CompatibleID</a></p></td>
</tr>
</tbody>
</table>

 

每个可移动设备功能重写均通过 **HardwareID** 或 **ContainerID** 注册表子项来指定。

**DeviceOverrides** 注册表项在 [HKLM \\ 系统 \\ CurrentControlSet \\ 控制注册表树](hklm-system-currentcontrolset-control-registry-tree.md)下创建和维护。 在此注册表项中，创建或维护一个或多个可移动设备功能重写。

可移动设备功能替代特定于通过 [HardwareID](hardwareid-registry-subkey.md) 或 [CompatibleID](compatibleid-registry-subkey.md) 注册表子项指定的单独设备。 其他子项定义为指定设备枚举的 devnodes 的路径。 通常，应使用最具体的设备硬件 ID 来识别设备，而不是使用不太具体的硬件或兼容 ID。 这可确保可移动设备功能替代不适用于与目标设备共享相同硬件或兼容 ID 的任何意外设备。

下图显示了 **DeviceOverrides** 注册表项及其相关子项的拓扑。

![说明 deviceoverrides 注册表项拓扑的示意图](images/containerid-3.png)

必须为添加到系统中的第一个可移动设备功能重写创建 **DeviceOverrides** 注册表项。 默认情况下，在干净的操作系统安装上可能不存在此设置。

**注意**  可移动设备功能注册表替代的存在不会更改 devnode 上可移动设备功能的全局状态。

 

 

 





