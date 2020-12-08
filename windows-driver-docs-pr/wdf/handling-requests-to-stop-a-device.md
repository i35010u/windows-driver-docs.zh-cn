---
title: 处理停止设备的请求
description: 处理停止设备的请求
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
ms.openlocfilehash: c229329f00ab1b88c8c7bba72e81ab62aa90ca6b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815617"
---
# <a name="handling-requests-to-stop-a-device"></a>处理停止设备的请求


在这两种情况下，在要求设备的驱动程序停止设备之前，PnP 管理器会询问驱动程序，因为停止设备是个好主意：

-   用户已插入新设备，PnP 管理器必须重新 [分发系统的硬件资源](#redistributing-resources) ，才能容纳新的设备。

-   用户已指示要 [删除该设备](#a-user-removes-or-disables-a-device)。

驱动程序可以通过多种方式来处理这些情况：

-   如果你的驱动程序调用了 [**WdfDeviceSetSpecialFileSupport**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport) ，因为设备支持特殊的文件，并且在设备上打开了某个特殊文件，则该框架将不允许设备停止。

-   若要暂时阻止所有中断一段较短的时间，驱动程序可以调用 [**WdfDeviceSetStaticStopRemove**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetstaticstopremove)。

-   若要单独评估并处理每次停止尝试，驱动程序可以提供 [*EvtDeviceQueryStop*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop) 和 [*EvtDeviceQueryRemove*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove) 回调函数。

如果设备不支持特殊文件，并且对于驱动程序或设备，停止或删除设备决不会出现问题，则驱动程序不会提供 *EvtDeviceQueryStop* 和 *EvtDeviceQueryRemove* 回调函数，并且永远不会调用 **WdfDeviceSetStaticStopRemove**。 在这种情况下，PnP 管理器始终停止设备，而不首先检查驱动程序是否允许该设备。

### <a name="redistributing-resources"></a><a href="" id="redistributing-resources"></a> 重新分发资源

有时 PnP 管理器必须重新分发系统的硬件资源。 通常，这是因为总线驱动程序报告已插入新设备，而新设备需要已分配的资源。 重新分配资源之前，必须停止设备。

如果你的驱动程序有时会阻止 PnP 管理器停止繁忙的设备，则驱动程序可以提供 [*EvtDeviceQueryStop*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop) 回调函数。 如果驱动程序的 *EvtDeviceQueryStop* 回调函数返回错误状态值，则 PnP 管理器不会停止该设备。

如果驱动程序确定停止设备是安全的，则回调函数返回状态 "成功" \_ 。 如果设备的其他驱动程序都不能阻止中断，则 PnP 管理器会暂时停止该设备。

有关当 PnP 管理器停止设备重新分配资源时框架调用驱动程序的事件回调函数的顺序的信息，请参阅 [Pnp 管理器重新分发系统资源](the-pnp-manager-redistributes-system-resources.md)。

### <a name="a-user-removes-or-disables-a-device"></a><a href="" id="a-user-removes-or-disables-a-device"></a> 用户删除或禁用设备

用户可以删除或禁用某些设备。 例如：

-   如果你的驱动程序设置了 **可移动** 成员 (而不是设备的 [**WDF \_ 设备 \_ PNP \_ 功能**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_pnp_capabilities)结构的 **SurpriseRemovalOK** 成员) ，则用户可以运行拔出或弹出硬件程序，然后拔出或弹出设备。

-   如果你的驱动程序未设置设备的 [**WDF \_ 设备 \_ 状态**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_state)结构的 **NotDisableable** 成员，则用户可以使用设备管理器禁用该设备。

在这种情况下，PnP 管理器会先尝试停止设备，然后再将其删除。

如果你的驱动程序有时会阻止删除繁忙的设备，则驱动程序可以提供 [*EvtDeviceQueryRemove*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove) 回调函数。 如果任何驱动程序的 *EvtDeviceQueryRemove* 回调函数返回错误状态值，则 PnP 管理器不会停止该设备。

如果驱动程序确定用户删除设备是安全的，则回调函数返回状态 " \_ 成功"。 如果设备的其他驱动程序都不能阻止删除，则 PnP 管理器将停止该设备。

有关框架在停止设备以进行删除时调用驱动程序的事件回调函数的顺序的信息，请参阅 [用户断开设备](a-user-unplugs-a-device.md)。

 

