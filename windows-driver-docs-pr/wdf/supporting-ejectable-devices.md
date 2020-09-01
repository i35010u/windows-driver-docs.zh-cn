---
title: 支持可弹出设备
description: 支持可弹出设备
ms.assetid: 7820bb71-7218-4c5f-af2b-f41e1b5f696d
keywords:
- PnP WDK KMDF，ejectable 设备
- 即插即用 WDK KMDF，ejectable 设备
- 电源管理 WDK KMDF，ejectable 设备
- 接驳站 WDK KMDF
- 总线驱动程序 WDK KMDF
- 弹出设备 WDK KMDF
- 弹出关系 WDK KMDF
- 删除 ejectable 设备
- 列出 ejectable 设备 WDK KMDF
- 锁定 ejectable 设备 WDK KMDF
- 便携设备 WDK KMDF
- 移动设备 WDK，KMDF
- 可移动设备 WDK KMDF
- 移动设备 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cea22fde8d079f169c586cf019c8c575882df3c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190805"
---
# <a name="supporting-ejectable-devices"></a>支持可弹出设备


*Ejectable 设备* 是可以插入扩展坞并从扩展坞中弹出的设备。 通常，必须先禁用 ejectable 设备的总线电源，才能删除设备。

如果设备是 ejectable 的，则设备总线的总线驱动程序必须在设备的[**WDF \_ 设备 \_ PNP \_ 功能**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_pnp_capabilities)结构中设置**EjectSupported**成员。

当总线驱动程序确定要弹出某个枚举的子设备时，它将调用 [**WdfPdoRequestEject**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdorequesteject) 或 [**WdfChildListRequestChildEject**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistrequestchildeject)。 例如，总线驱动程序可能检测到用户已按下弹出按钮。

当驱动程序调用 [**WdfChildListRequestChildEject**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistrequestchildeject) 或 [**WdfPdoRequestEject**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdorequesteject)时，PnP 管理器使用有 [序删除](a-user-unplugs-a-device.md#orderly-removal) 方案来通知设备的驱动程序正在删除设备。 在框架为设备总线调用了总线驱动程序中的 [*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) 回调函数后，框架将调用总线驱动程序的 [*EvtDeviceEject*](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_eject) 回调函数，该函数将执行物理弹出该设备所需的任何操作。

如果弹出设备还会导致其他设备弹出，则总线驱动程序可以维护 *弹出关系*的列表。 当用户删除设备时，PnP 管理器将通知列表中设备的驱动程序，同时还会删除其设备。 若要维护弹出关系列表，总线驱动程序可使用 [**WdfPdoAddEjectionRelationsPhysicalDevice**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoaddejectionrelationsphysicaldevice)、 [**WdfPdoRemoveEjectionRelationsPhysicalDevice**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoremoveejectionrelationsphysicaldevice)和 [**WdfPdoClearEjectionRelationsDevices**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoclearejectionrelationsdevices) 方法。

如果设备可以在其扩展坞中锁定，则总线驱动程序必须在设备的[**WDF \_ 设备 \_ PNP \_ 功能**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_pnp_capabilities)结构中设置**LockSupported**成员。 总线驱动程序还必须提供一个 [*EvtDeviceSetLock*](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock) 回调函数，该函数会锁定设备以禁用弹出或解锁设备以启用弹出。

 

