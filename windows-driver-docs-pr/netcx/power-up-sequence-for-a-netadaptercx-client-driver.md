---
title: NetAdapterCx 客户端驱动程序的启动顺序
description: NetAdapterCx 客户端驱动程序的启动顺序
ms.assetid: 86694F6B-9AE4-4FDB-A4BB-9B7ACBC0B1DA
keywords:
- 强化 NetAdapterCx 客户端驱动程序、 NetAdapterCx 客户端驱动程序的增益道具序列、 NetCx 客户端驱动程序的启动顺序的序列
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: eb565c3a05ac16fff0eb3ca6ddfd30138ef3271f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577471"
---
# <a name="power-up-sequence-for-a-netadaptercx-client-driver"></a>NetAdapterCx 客户端驱动程序的启动顺序

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

下图显示了在其中 NetAdapterCx 调用客户端驱动程序的事件回调函数为完全可操作的状态，使设备时启动从设备到达状态图底部的顺序：

<img src="images/netadaptercx-powerup.png" alt="Device enumeration and power-up sequence for NetAdapterCx client driver" title="NetAdapterCx 客户端驱动程序的设备枚举和增益道具序列" style="width: 600px;"/>

广泛的水平线将标记中启动设备所涉及的步骤。 图左侧列描述相应步骤，并在右侧列列出完成该操作的事件回调。 虽然其他步骤普遍适用于所有基于 WDF 驱动程序，有特定的 NetAdapterCx，标记为蓝色文本的步骤。

在该图底部，设备不存在系统上。 框架在用户插入设备，首先调用驱动程序的[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调，以便该驱动程序可以创建一个设备对象来表示该设备。 框架将继续进行向上访问序列，直到该设备正常调用驱动程序的回调例程。 请记住，框架会因此调用图中所示的自下而上的顺序中的事件回调[ *EvtDeviceFilterRemoveResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540872)之前调用[ *EvtDeviceFilterAddResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540870) ，依此类推。 如果设备已停止来重新平衡资源，或以物理方式存在，但在低功耗状态，并非所有的步骤是必需的如图所示。

