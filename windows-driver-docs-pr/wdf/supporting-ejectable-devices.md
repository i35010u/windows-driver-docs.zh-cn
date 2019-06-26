---
title: 支持可弹出设备
description: 支持可弹出设备
ms.assetid: 7820bb71-7218-4c5f-af2b-f41e1b5f696d
keywords:
- 即插即用 WDK KMDF，无可退出设备
- 插 WDK KMDF，无可退出设备
- 电源管理 WDK KMDF，无可退出设备
- 扩展坞 WDK KMDF
- 总线驱动程序 WDK KMDF
- 弹出设备 WDK KMDF
- 弹出关系 WDK KMDF
- 删除无可退出设备
- 列出无可退出设备 WDK KMDF
- 锁定无可退出设备 WDK KMDF
- 便携设备 WDK KMDF
- 移动设备 WDK、 KMDF
- 可移动设备 WDK KMDF
- WDK 的移动设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39f6d1bf883ef0306caab428139eb582bf2148c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368662"
---
# <a name="supporting-ejectable-devices"></a>支持可弹出设备


*无可退出设备*是可以插入到扩展坞，从扩展坞弹出的设备。 通常情况下，可以删除该设备之前，必须禁用无可退出设备的总线电源。

如果设备是无可退出，必须设置设备的总线的总线驱动程序**EjectSupported**的设备中的成员[ **WDF\_设备\_PNP\_功能** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_pnp_capabilities)结构。

当总线驱动程序确定其枚举的子设备之一是要弹出时，它会调用任一[ **WdfPdoRequestEject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdorequesteject)或[ **WdfChildListRequestChildEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nf-wdfchildlist-wdfchildlistrequestchildeject)。 例如，总线驱动程序可能检测到用户已按下一个弹出按钮。

当驱动程序调用[ **WdfChildListRequestChildEject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nf-wdfchildlist-wdfchildlistrequestchildeject)或[ **WdfPdoRequestEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdorequesteject)，即插即用管理器使用[有序地删除](a-user-unplugs-a-device.md#orderly-removal)方案以通知正在删除该设备的设备的驱动程序。 该框架已调用后[ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)总线驱动程序对于设备的总线，框架中的回调函数将调用总线驱动程序[ *EvtDeviceEject* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_eject)回调函数，用于执行所需以物理方式弹出该设备的任何操作。

如果弹出您的设备将导致其他设备还弹出，总线驱动程序可以维护一份*弹出关系*。 如果用户删除你的设备，即插即用管理器会通知的列表中的设备驱动程序也删除其设备。 若要维护一份弹出关系，总线驱动程序可以使用[ **WdfPdoAddEjectionRelationsPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoaddejectionrelationsphysicaldevice)， [ **WdfPdoRemoveEjectionRelationsPhysicalDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoremoveejectionrelationsphysicaldevice)，并[ **WdfPdoClearEjectionRelationsDevices** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoclearejectionrelationsdevices)方法。

如果可以在自己的扩展坞中锁定设备，必须设置总线驱动程序**LockSupported**的设备中的成员[ **WDF\_设备\_PNP\_功能** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_pnp_capabilities)结构。 总线驱动程序还必须提供[ *EvtDeviceSetLock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock)回调函数，以使设备能够禁用弹出或解锁设备后，若要启用弹出。

 

 





