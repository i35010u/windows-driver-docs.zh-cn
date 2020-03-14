---
title: 处理停止设备的请求
description: 处理停止设备的请求
ms.assetid: 4c8f37b3-7961-4c78-a88b-3eec58155e66
keywords:
- PnP WDK KMDF，停止设备
- 即插即用 WDK KMDF，停止设备
- 重新分发资源 WDK KMDF
- 资源重新分发 WDK KMDF
- 删除设备 WDK KMDF
- 设备停止请求 WDK KMDF
- device stop requests WKD KMDF，PnP
- 临时设备停止 WDK KMDF
- 临时设备停止 WDK KMDF，PnP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 095f190f07ef38e22b496081ca73ba136487e01a
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242910"
---
# <a name="handling-requests-to-stop-a-device"></a>处理停止设备的请求


在这两种情况下，在要求设备的驱动程序停止设备之前，PnP 管理器会询问驱动程序，因为停止设备是个好主意：

-   用户已插入新设备，PnP 管理器必须重新[分发系统的硬件资源](#redistributing-resources)，才能容纳新的设备。

-   用户已指示要[删除该设备](#a-user-removes-or-disables-a-device)。

驱动程序可以通过多种方式来处理这些情况：

-   如果你的驱动程序调用了[**WdfDeviceSetSpecialFileSupport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport) ，因为设备支持特殊的文件，并且在设备上打开了某个特殊文件，则该框架将不允许设备停止。

-   若要暂时阻止所有中断一段较短的时间，驱动程序可以调用[**WdfDeviceSetStaticStopRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetstaticstopremove)。

-   若要单独评估并处理每次停止尝试，驱动程序可以提供[*EvtDeviceQueryStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop)和[*EvtDeviceQueryRemove*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove)回调函数。

如果设备不支持特殊文件，并且对于驱动程序或设备，停止或删除设备决不会出现问题，则驱动程序不会提供*EvtDeviceQueryStop*和*EvtDeviceQueryRemove*回调函数，并且永远不会调用**WdfDeviceSetStaticStopRemove**。 在这种情况下，PnP 管理器始终停止设备，而不首先检查驱动程序是否允许该设备。

### <a href="" id="redistributing-resources"></a>重新分发资源

有时 PnP 管理器必须重新分发系统的硬件资源。 通常，这是因为总线驱动程序报告已插入新设备，而新设备需要已分配的资源。 重新分配资源之前，必须停止设备。

如果你的驱动程序有时会阻止 PnP 管理器停止繁忙的设备，则驱动程序可以提供[*EvtDeviceQueryStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop)回调函数。 如果驱动程序的*EvtDeviceQueryStop*回调函数返回错误状态值，则 PnP 管理器不会停止该设备。

如果驱动程序确定停止设备是安全的，则回调函数将返回状态\_"成功"。 如果设备的其他驱动程序都不能阻止中断，则 PnP 管理器会暂时停止该设备。

有关当 PnP 管理器停止设备重新分配资源时框架调用驱动程序的事件回调函数的顺序的信息，请参阅[Pnp 管理器重新分发系统资源](the-pnp-manager-redistributes-system-resources.md)。

### <a href="" id="a-user-removes-or-disables-a-device"></a>用户删除或禁用设备

用户可以删除或禁用某些设备。 例如：

-   如果你的驱动程序已设置设备的 WDF\_设备的**可移动**成员（而不是**SurpriseRemovalOK**成员） [ **\_PNP\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_pnp_capabilities)结构，则用户可以运行拔出或弹出硬件程序，然后拔出或弹出设备。

-   如果你的驱动程序未将设备的[**WDF\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_state)的**NotDisableable**成员设置\_状态结构，则用户可以使用设备管理器来禁用该设备。

在这种情况下，PnP 管理器会先尝试停止设备，然后再将其删除。

如果你的驱动程序有时会阻止删除繁忙的设备，则驱动程序可以提供[*EvtDeviceQueryRemove*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove)回调函数。 如果任何驱动程序的*EvtDeviceQueryRemove*回调函数返回错误状态值，则 PnP 管理器不会停止该设备。

如果驱动程序确定用户删除设备是安全的，则回调函数将返回状态\_"成功"。 如果设备的其他驱动程序都不能阻止删除，则 PnP 管理器将停止该设备。

有关框架在停止设备以进行删除时调用驱动程序的事件回调函数的顺序的信息，请参阅[用户断开设备](a-user-unplugs-a-device.md)。

 

 





