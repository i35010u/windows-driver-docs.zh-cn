---
title: 存储类驱动程序的 AddDevice 例程
description: 存储类驱动程序的 AddDevice 例程
ms.assetid: ff07ae84-2748-44b4-88c6-e67f1d4c9268
keywords:
- AddDevice 例程 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca0942a63632116577af7f9d25dd8df0dad16436
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845089"
---
# <a name="storage-class-drivers-adddevice-routine"></a>存储类驱动程序的 AddDevice 例程


## <span id="ddk_storage_class_drivers_adddevice_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_ADDDEVICE_ROUTINE_KG"></span>


PnP 管理器会在检测到由该驱动程序控制的设备时调用存储类驱动程序的[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程。 存储类驱动程序的*AddDevice*例程：

-   声明设备，如[存储类驱动程序的 ClaimDevice 例程](storage-class-driver-s-claimdevice-routine.md)中所述，如果驱动程序无法声明设备，则返回状态\_SUCCESS。

-   如果驱动程序成功声明设备，则创建一个设备对象（FDO）。

-   注册应用程序和其他系统设备可使用的设备接口。 类驱动程序在收到 PnP 启动请求时会启用此类接口。

-   准备设备对象以处理开始请求，如[编写 AddDevice 例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-an-adddevice-routine)中所述。

-   通过使用输入 PDO 调用[**IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack) ，将设备对象附加到设备堆栈。

-   如果设备在已知电源状态下启动，则调用[**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)。

-   清除在新设备对象上\_设备\_初始化标志。

存储类驱动程序在其自己的设备对象（FDO）的设备扩展中存储由**IoAttachDeviceToDeviceStack**返回的指针，该对象表示新声明的设备，并且*必须在类驱动程序将发送到下一个较低的驱动程序*。 驱动程序还在设备扩展中存储了指向输入 PDO 的指针，但在**IoAttachDeviceToDeviceStack**返回后，该驱动程序必须在调用 PnP **Io * * * Xxx*例程（将此类指针作为参数.

有关详细信息，请参阅[编写 AddDevice 例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-an-adddevice-routine)。

 

 




