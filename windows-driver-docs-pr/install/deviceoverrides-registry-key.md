---
title: DeviceOverrides 注册表项
description: DeviceOverrides 注册表项
ms.assetid: 18f95848-71fe-4884-bcbe-d3cae90fc262
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d2f2a5abc278d3679ecb57bd1b8d084dc2f992e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354636"
---
# <a name="deviceoverrides-registry-key"></a>DeviceOverrides 注册表项


从 Windows 7 开始**DeviceOverrides**注册表项指定在系统中存在一个或多个可移动设备功能重写。 有关可移动设备功能的详细信息，请参阅[可移动设备功能的概述](overview-of-the-removable-device-capability.md)。

插即用 (PnP) 管理器使用源自和属于特定的物理设备在计算机中安装的每个实例的新 ID （容器 Id）。 对于旧设备的即插即用的管理器会生成通过可移动设备功能的容器 Id。 PnP 管理器如何生成容器 Id 的详细信息，请参阅[生成如何容器 Id](how-container-ids-are-generated.md)。

通过重写可移动设备功能，独立硬件供应商 (IHV) 或原始设备制造商 (OEM) 更改 devnode 或 devnodes 组上的可移动设备功能的解释型值。

可移动设备功能通过重写**DeviceOverrides**注册表项可用于旧设备或可能无法正确报告了可移动设备功能的第三方硬件组件。 这将导致错误地生成容器 ID 用于分组 devnodes 枚举从物理设备的即插即用管理器。

这些重写不实际更改报告的 devnode 可移动设备功能的全局的状态。 相反，这些重写导致 PnP 管理器忽略报告的设备功能，并生成时使用的基于注册表的设置[容器 ID](container-ids.md) devnodes 匹配重写的。 附加子项 DeviceOverrides 注册表子项下的提供有关哪些 devnodes 重写的更多详细信息。

下表定义了**DeviceOverrides**注册表项的格式和要求。

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
<th align="left">父项</th>
<th align="left">子级子项</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>DeviceOverrides</strong></p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p><a href="hardwareid-registry-subkey.md" data-raw-source="[HardwareID](hardwareid-registry-subkey.md)">HardwareID</a>或<a href="compatibleid-registry-subkey.md" data-raw-source="[CompatibleID](compatibleid-registry-subkey.md)">CompatibleID</a></p></td>
</tr>
</tbody>
</table>

 

通过指定每个可移动设备功能重写**HardwareID**或**ContainerID**注册表子项。

**DeviceOverrides**注册表项是下创建和维护[HKLM\\系统\\CurrentControlSet\\控件注册表树](hklm-system-currentcontrolset-control-registry-tree.md)。 在此注册表项，一个或多个可移动设备功能重写创建或维护。

可移动设备功能替代不特定于单个设备通过指定[HardwareID](hardwareid-registry-subkey.md)或[CompatibleID](compatibleid-registry-subkey.md)注册表子项。 附加子项定义 devnodes 枚举用于指定设备的路径。 通常情况下，应使用 ID 来标识设备，而不是更具体的硬件或兼容的最特定设备硬件 id。 这可确保可移动设备功能重写，不应用于共享相同的硬件或兼容 ID 作为目标设备的任何意外的设备。

下图显示了的拓扑**DeviceOverrides**注册表项及其相关的子项。

![说明 deviceoverrides 注册表密钥拓扑关系图](images/containerid-3.png)

**DeviceOverrides**必须为添加到系统的第一个可移动设备功能重写创建注册表项。 它可能不存在干净操作系统安装在默认情况下。

**请注意**  可移动设备功能注册表替代是否存在不会更改 devnode 上的可移动设备功能的全局状态。

 

 

 





