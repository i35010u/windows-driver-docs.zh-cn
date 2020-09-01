---
title: 存储类驱动程序的 AddDevice 例程
description: 存储类驱动程序的 AddDevice 例程
ms.assetid: ff07ae84-2748-44b4-88c6-e67f1d4c9268
keywords:
- AddDevice 例程 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d1a2769f0ba79de0ae12c77f9bebfbaf8e1f3c5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189025"
---
# <a name="storage-class-drivers-adddevice-routine"></a>存储类驱动程序的 AddDevice 例程


## <span id="ddk_storage_class_drivers_adddevice_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_ADDDEVICE_ROUTINE_KG"></span>


PnP 管理器会在检测到由该驱动程序控制的设备时调用存储类驱动程序的 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程。 存储类驱动程序的 *AddDevice* 例程：

-   声明设备，如 [存储类驱动程序的 ClaimDevice 例程](storage-class-driver-s-claimdevice-routine.md)中所述，如果驱动程序无法声明设备，则返回状态 " \_ 成功"。

-   如果驱动程序成功声明设备， (FDO) 创建设备对象。

-   注册应用程序和其他系统设备可使用的设备接口。 类驱动程序在收到 PnP 启动请求时会启用此类接口。

-   准备设备对象以处理开始请求，如 [编写 AddDevice 例程](../kernel/writing-an-adddevice-routine.md)中所述。

-   通过使用输入 PDO 调用 [**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack) ，将设备对象附加到设备堆栈。

-   如果设备在已知电源状态下启动，则调用 [**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)。

-   清除 \_ \_ 新设备对象上的 "执行设备初始化" 标志。

存储类驱动程序在其自己的设备对象的设备扩展中存储由 **IoAttachDeviceToDeviceStack** 返回的指针 (FDO) 表示新声明的设备，并且 *必须在类驱动程序发送到下一个较低驱动程序的所有后续请求中使用此指针*。 驱动程序还在设备扩展中存储了指向输入 PDO 的指针，但在 **IoAttachDeviceToDeviceStack** 返回后，驱动程序必须仅在调用 PnP **Io * * * Xxx* 例程（将此类指针作为参数）时使用指针。

有关详细信息，请参阅 [编写 AddDevice 例程](../kernel/writing-an-adddevice-routine.md)。

 

