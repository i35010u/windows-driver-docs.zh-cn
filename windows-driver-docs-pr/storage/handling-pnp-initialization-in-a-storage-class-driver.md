---
title: 处理存储类驱动程序中的 PnP 初始化
description: 处理存储类驱动程序中的 PnP 初始化
ms.assetid: 472e52c8-a214-418b-a82f-fd4a9bcc894e
keywords:
- 存储类驱动程序 WDK、PnP
- 类驱动程序 WDK 存储，PnP
- PnP WDK 存储
- 即插即用 WDK 存储
- 初始化存储类驱动程序
- 存储类驱动程序 WDK，初始化
- 类驱动程序 WDK 存储，初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c031265b857e0178c2862fdc034bb708bdf77011
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837558"
---
# <a name="handling-pnp-initialization-in-a-storage-class-driver"></a>处理存储类驱动程序中的 PnP 初始化


## <span id="ddk_handling_pnp_initialization_in_a_storage_class_driver_kg"></span><span id="DDK_HANDLING_PNP_INITIALIZATION_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


存储类驱动程序的初始化与任何 PnP 驱动程序的初始化大致相同。

当 PnP 管理器调用驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程来加载和初始化驱动程序时，将开始存储类驱动程序初始化。 然后，PnP 管理器调用存储类驱动程序的[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程，并传递一个指向表示目标设备的物理设备对象（PDO）的指针。

类驱动程序在其*AddDevice*例程中调用[**IoGetAttachedDeviceReference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference) ，并发出 SRB\_函数\_声明\_设备命令（请参阅[**SCSI\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)）到设备对象返回，以防止旧式驱动程序声称设备。 类驱动程序在此初始化阶段不能向设备发送任何其他命令。

如果类驱动程序成功声明设备，它将创建一个功能设备对象（FDO），并通过使用输入 PDO 调用[**IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)将其附加到设备堆栈。 当*AddDevice*返回时，驱动程序必须准备好处理 pnp 启动请求（IRP\_MJ\_pnp，并使用[**irp\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)）。 在 PnP 管理器完成构造驱动程序堆栈（可能包括一个或多个筛选器驱动程序，该类驱动程序的上方和下方）后，它会向目标设备的驱动程序堆栈中最顶层的驱动程序发出启动请求。

如果类驱动程序无法成功声明设备，则它不能尝试将 FDO 附加到设备堆栈，只需从其*AddDevice*例程返回成功状态。 此类驱动程序将不会收到设备的 PnP 启动请求，但 PnP 管理器可能会为同一设备或不同设备再次调用其*AddDevice*例程。

有关初始化存储类驱动程序的详细信息，请参阅以下内容：

[存储类驱动程序的 DriverEntry 例程](storage-class-driver-s-driverentry-routine.md)

[存储类驱动程序的 AddDevice 例程](storage-class-driver-s-adddevice-routine.md)

另请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。

 

 




