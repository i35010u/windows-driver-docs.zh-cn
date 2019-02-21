---
title: 硬件资源简介
description: 硬件资源简介
ms.assetid: 34350031-daae-4213-b157-086a7a55e05b
keywords:
- 启动配置 WDK KMDF
- 逻辑配置 WDK KMDF
- 有关硬件资源的硬件资源 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee5116f18166276c8133d2276ba6111cb539dfc9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523818"
---
# <a name="introduction-to-hardware-resources"></a>硬件资源简介


用户插入的即插即用设备驱动程序后，[枚举设备](enumerating-the-devices-on-a-bus.md)通常会创建一个或多个[逻辑配置](https://msdn.microsoft.com/library/windows/hardware/ff547012#ddk-logical-configurations-kg)，这是设备可以使用的硬件资源的组合。 这些配置包括：

-   一个*启动配置*，它列出在设备需要在系统启动时的硬件资源。 （对于即插即用设备，此信息将提供由 BIOS。）

-   设备可以在其中操作的其他配置。 该驱动程序组中的这些其他配置[资源要求列表](https://msdn.microsoft.com/library/windows/hardware/ff547012)。 PnP 管理器最终将从要向设备分配此列表中选择资源。

驱动程序创建的逻辑配置后，它将其发送到框架，并且该框架将其发送到 PnP 管理器。

接下来，即插即用管理器确定哪些设备要求，并将它们加载如果它们不是已加载的驱动程序。 PnP 管理器将设备的硬件要求列表发送到设备的驱动程序，供查看。 函数和筛选器驱动程序可以修改此列表并将其发送回 PnP 管理器。

PnP 管理器检查修改后的硬件要求列表，并确定哪些指定的资源是在系统上实际可用。 如果设备需要即插即用管理器有以前分配给另一台设备的资源，即插即用管理器可能会尝试向[重新分发资源](handling-requests-to-stop-a-device.md#redistributing-resources)在系统的设备之间。

接下来，即插即用管理器创建[资源列表](https://msdn.microsoft.com/library/windows/hardware/ff547012)，这是一系列的即插即用的管理器想要分配到设备的资源。 PnP 管理器将此列表发送到设备的驱动程序，供查看。 此时的函数和筛选器驱动程序可以从列表中删除资源，但它们不能将资源添加到它。

最后，即插即用管理器将资源分配给设备。 Framework 传递到设备的函数和筛选器驱动程序和设备的功能驱动程序的资源列表执行，因此设备和驱动程序可访问的资源是必要的任何初始化。

以下步骤介绍了如何在更多详细信息：

1.  [用户插入设备](a-user-plugs-in-a-device.md)。

2.  总线驱动程序检测到设备和[枚举](enumerating-the-devices-on-a-bus.md)它。

3.  框架将调用总线驱动程序[ *EvtDeviceResourcesQuery* ](https://msdn.microsoft.com/library/windows/hardware/ff540895)回调函数，其中[创建资源列表](creating-a-resource-list-for-a-boot-configuration.md)描述设备的启动配置。

4.  框架将调用总线驱动程序[ *EvtDeviceResourceRequirementsQuery* ](https://msdn.microsoft.com/library/windows/hardware/ff540894)回调函数，其中[创建的资源要求列表](creating-a-resource-requirements-list.md)设备。

5.  PnP 管理器确定设备需要并加载它们，如果它们不是已加载，若要创建一个驱动程序堆栈，该设备的驱动程序。

6.  PnP 管理器将设备的资源要求列表发送到评审的驱动程序堆栈。 当列表传输驱动程序堆栈下时，框架将调用每个函数和筛选器驱动程序的[ *EvtDeviceFilterRemoveResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540872)回调函数。 当列表传输到堆栈时，框架将调用每个函数和筛选器驱动程序的[ *EvtDeviceFilterAddResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540870)回调函数。 这两个回调函数可以[修改的资源要求列表](modifying-a-resource-requirements-list.md)。

7.  PnP 管理器创建设备的资源列表，并将其发送到评审的驱动程序堆栈。 框架将调用每个函数和筛选器驱动程序的[ *EvtDeviceRemoveAddedResources* ](https://msdn.microsoft.com/library/windows/hardware/ff540892)回调函数，其中[中删除资源](modifying-a-resource-list.md)的驱动程序*EvtDeviceFilterAddResourceRequirements*添加，因此总线驱动程序不会尝试使用它们的回调函数。

8.  框架的即插即用的管理器从接收最终的资源列表，并将其存储。

9.  如果驱动程序调用[ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345)创建中断对象，该框架在资源列表中查找中断资源，并将其分配中断对象。

10. 在设备进入了未初始化的 D0 状态后，框架将调用每个驱动程序[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调函数，传递[原始和已翻译](raw-and-translated-resources.md)版本的设备的资源列表作为输入参数。 该驱动程序可以保存资源的列表，该框架将调用的驱动程序才有效[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)回调函数。

 

 





