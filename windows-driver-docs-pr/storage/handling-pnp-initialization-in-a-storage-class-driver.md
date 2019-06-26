---
title: 处理存储类驱动程序中的 PnP 初始化
description: 处理存储类驱动程序中的 PnP 初始化
ms.assetid: 472e52c8-a214-418b-a82f-fd4a9bcc894e
keywords:
- 存储类驱动程序 WDK，即插即用
- 类驱动程序 WDK 存储，即插即用
- 即插即用 WDK 存储
- 插 WDK 存储
- 正在初始化存储类驱动程序
- 存储类驱动程序 WDK，初始化
- 类驱动程序 WDK 存储初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dcc6294eec9bbee80c5b0d7a59dced8c4ef21ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378515"
---
# <a name="handling-pnp-initialization-in-a-storage-class-driver"></a>处理存储类驱动程序中的 PnP 初始化


## <span id="ddk_handling_pnp_initialization_in_a_storage_class_driver_kg"></span><span id="DDK_HANDLING_PNP_INITIALIZATION_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


初始化的存储类驱动程序是类似于任何即插即用驱动程序的初始化。

存储类驱动程序初始化时即插即用管理器会调用驱动程序的开始[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程，以加载和初始化的驱动程序。 然后，即插即用管理器调用的存储类驱动程序的[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程，将指针传递到物理设备对象 (PDO)，表示目标设备。

在其*AddDevice*例程，类驱动程序调用[ **IoGetAttachedDeviceReference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iogetattacheddevicereference)并发出 SRB\_函数\_声明\_设备命令 (请参阅[ **SCSI\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)) 到设备对象返回，以防止旧类驱动程序声明设备。 类驱动程序必须在此阶段中的初始化过程将不包含其他命令发送到设备。

如果类驱动程序已成功对声明该设备，它创建功能的设备对象 (FDO)，并将其附加到设备堆栈通过调用[ **IoAttachDeviceToDeviceStack** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack) PDO 中的输入。 当*AddDevice*返回时，该驱动程序必须准备好处理即插即用启动请求 (IRP\_MJ\_与 PNP [ **IRP\_MN\_开始\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device))。 PnP 管理器已构造的驱动程序堆栈 （其中可能包括分层的上方和下方的类驱动程序的一个或多个筛选器驱动程序） 后启动请求颁发给目标设备的驱动程序堆栈中的最顶层驱动程序。

如果类驱动程序无法成功声明设备，它必须不尝试将 FDO 附加到设备堆栈，并只应返回成功状态从其*AddDevice*例程。 这样的驱动程序将不会收到该设备，即插即用的启动请求，尽管 PnP 管理器可能会调用其*AddDevice*例程再次为相同或不同的设备。

有关初始化存储类驱动程序的详细信息，请参阅：

[存储类驱动程序 DriverEntry 例程](storage-class-driver-s-driverentry-routine.md)

[存储类驱动程序 AddDevice 例程](storage-class-driver-s-adddevice-routine.md)

另请参阅[插](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。

 

 




