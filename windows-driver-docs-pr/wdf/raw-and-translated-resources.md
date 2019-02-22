---
title: 原始和已翻译资源
description: 原始和已翻译资源
ms.assetid: dfc1376d-7a1a-421c-82ae-e183cac77ec8
keywords:
- 硬件资源 WDK KMDF，原始资源
- 资源列出了 WDK KMDF
- 硬件资源 WDK KMDF，翻译后的资源
- 已翻译的资源 WDK KMDF
- 原始资源 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d608551898ea3ce4cce0756ec06010418b0a937
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547972"
---
# <a name="raw-and-translated-resources"></a>原始和已翻译资源


当驱动程序的[ *EvtDeviceRemoveAddedResources* ](https://msdn.microsoft.com/library/windows/hardware/ff540892)或[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调函数接收资源列表中，它会收到两个版本的列表。 一个版本表示的设备*原始资源*，和另一个表示设备的*资源转换*。 这两个版本表示同一组中的顺序相同的硬件资源。

-   原始资源是由相对于该设备连接到总线的地址标识的资源。 通常情况下，程序设备驱动程序提供这些地址到设备。

-   翻译后的资源是由系统驱动程序用于访问资源的物理地址标识的资源。

PCI 总线设备驱动程序接收到设备中出现的顺序列出的资源*基本地址注册*（条形图）。 但是，可能会更多资源描述符交错在列表中，以便索引处的资源*X*栏中可能不匹配资源列表中的同一个索引位置处的资源。

有关原始和已翻译的资源的详细信息，请参阅成员的说明[ **CM\_分部\_资源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff541977)结构。

如果设备的翻译资源列表包含具有的资源**类型**CM 成员\_分部\_资源\_描述符结构设置为**CmResourceTypeMemory**，每个访问该资源的驱动程序必须执行以下操作：

-   在驱动程序[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调函数必须调用[ **MmMapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff554618)将映射到系统物理地址系统虚拟地址。
-   在驱动程序[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)回调函数必须调用[ **MmUnmapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff556387)取消地址的映射。

有关映射总线相对地址的详细信息，请参阅[映射到的虚拟地址的总线相对地址](https://msdn.microsoft.com/library/windows/hardware/ff554399)。

 

 





