---
title: 处理请求以停止设备
description: 处理请求以停止设备
ms.assetid: 4c8f37b3-7961-4c78-a88b-3eec58155e66
keywords:
- PnP WDK KMDF，停用该设备
- 插 WDK KMDF，停用该设备
- 重新分发资源 WDK KMDF
- 资源重新分发 WDK KMDF
- 删除设备 WDK KMDF
- 设备停止请求 WDK KMDF
- 设备停止请求 WKD KMDF，即插即用
- 临时设备断电 WDK KMDF
- 临时设备断电 WDK KMDF，即插即用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3bc2b67b1e68ed78850175f0aa53cb15f0f0c61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542466"
---
# <a name="handling-requests-to-stop-a-device"></a>处理请求以停止设备


有两种情况下，在其中，然后才能咨询要停用设备的设备的驱动程序 PnP 管理器会要求驱动程序是否停止该设备是一个好主意：

-   用户已插入新的设备，并 PnP 管理器必须[重新发布系统的硬件资源](#redistributing-resources)以容纳新设备。

-   用户已指明，他或她想要[中删除该设备](#a-user-removes-or-disables-a-device)。

有几种方法在其中一个驱动程序可以处理这些情况下：

-   如果您的驱动程序已调用[ **WdfDeviceSetSpecialFileSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff546903)由于设备一种支持的特殊文件，并且如果在设备上打开的特殊文件，该框架不允许设备要停止.

-   若要暂时防止相对较短的时间中的所有中断，该驱动程序可以调用[ **WdfDeviceSetStaticStopRemove**](https://msdn.microsoft.com/library/windows/hardware/ff546915)。

-   若要评估并单独处理每次停止尝试后，该驱动程序可以提供[ *EvtDeviceQueryStop* ](https://msdn.microsoft.com/library/windows/hardware/ff540885)并[ *EvtDeviceQueryRemove* ](https://msdn.microsoft.com/library/windows/hardware/ff540883)回调函数。

如果设备不支持特殊文件，并且如果停止或删除设备永远不会是个问题的驱动程序或设备，该驱动程序不提供*EvtDeviceQueryStop*并*EvtDeviceQueryRemove*回调函数并永远不会调用**WdfDeviceSetStaticStopRemove**。 在这种情况下的即插即用的管理器始终使设备停止而无需先检查以确定驱动程序允许它。

### <a href="" id="redistributing-resources"></a> 重新分发的资源

有时 PnP 管理器必须重新分发系统的硬件资源。 通常情况下，因为总线驱动程序已报告新设备具有已接通电源，并在新设备需要已分配资源，会发生此重新分发。 必须先停止设备重新分配资源。

如果您的驱动程序有时禁止 PnP 管理器停止繁忙的设备，该驱动程序可以提供所需[ *EvtDeviceQueryStop* ](https://msdn.microsoft.com/library/windows/hardware/ff540885)回调函数。 如果您的驱动程序*EvtDeviceQueryStop*回调函数返回一个错误状态值，即插即用管理器不会停止设备。

如果该驱动程序确定，则可以安全地停用设备，该回调函数将返回状态\_成功。 如果没有任何设备的其他驱动程序阻止在断电、 即插即用管理器暂时停止设备。

有关在其中框架驱动程序的事件回调函数时调用的即插即用的管理器停止要重新分发的资源的设备的顺序的信息，请参阅[PnP 管理器将重新分发的系统资源](the-pnp-manager-redistributes-system-resources.md)。

### <a href="" id="a-user-removes-or-disables-a-device"></a> 用户删除或禁用的设备

用户可以删除或禁用某些设备。 例如：

-   如果您的驱动程序已设置**可移动**成员 (而非**SurpriseRemovalOK**成员) 的设备的[ **WDF\_设备\_PNP\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff551257)结构，用户可以运行拔出或弹出硬件程序然后拔出或弹出该设备。

-   如果您的驱动程序没有设置**NotDisableable**的设备的成员[ **WDF\_设备\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff551284)结构，用户可以使用设备若要禁用设备的管理器。

在这种情况下，即插即用管理器尝试停用设备之前用户将其删除。

如果需要为您的驱动程序有时会阻碍正忙的设备中删除，该驱动程序可以提供[ *EvtDeviceQueryRemove* ](https://msdn.microsoft.com/library/windows/hardware/ff540883)回调函数。 如果任何驱动程序*EvtDeviceQueryRemove*回调函数返回一个错误状态值，即插即用管理器不会停止设备。

如果该驱动程序确定要删除设备的用户的安全，回调函数将返回状态\_成功。 如果没有任何设备的其他驱动程序阻止删除，PnP 管理器使设备停止。

有关在其中框架将调用驱动程序的事件回调函数停止删除设备时的顺序的信息，请参阅[用户断开设备](a-user-unplugs-a-device.md)。

 

 





