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
ms.openlocfilehash: eff7e74aa147a917f26dfe5e2ef7921a617eec1d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184703"
---
# <a name="handling-pnp-initialization-in-a-storage-class-driver"></a>处理存储类驱动程序中的 PnP 初始化


## <span id="ddk_handling_pnp_initialization_in_a_storage_class_driver_kg"></span><span id="DDK_HANDLING_PNP_INITIALIZATION_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


存储类驱动程序的初始化与任何 PnP 驱动程序的初始化大致相同。

当 PnP 管理器调用驱动程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程来加载和初始化驱动程序时，将开始存储类驱动程序初始化。 然后，PnP 管理器调用存储类驱动程序的 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程，并将一个指针传递到一个物理设备对象 (PDO) 表示目标设备。

在其 *AddDevice* 例程中，类驱动程序调用 [**IOGETATTACHEDDEVICEREFERENCE**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference) 并发出 SRB \_ 函数 \_ 声明 \_ 设备命令 (查看返回的设备对象的 [**SCSI \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)) ，以防止遗留类驱动程序声称设备。 类驱动程序在此初始化阶段不能向设备发送任何其他命令。

如果类驱动程序成功声明设备，它将创建一个功能设备对象 (FDO) ，并通过使用输入 PDO 调用 [**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack) 将其附加到设备堆栈。 当 *AddDevice* 返回时，驱动程序必须准备好处理 PnP 启动请求， (irp \_ MJ \_ PnP 和 [**irp \_ MN \_ start \_ DEVICE**](../kernel/irp-mn-start-device.md)) 。 PnP 管理器完成构造驱动程序堆栈后 (可能包括一个或多个筛选器驱动程序堆叠在类驱动程序的上方和下方时) 它向目标设备的驱动程序堆栈中的最顶层驱动程序发出启动请求。

如果类驱动程序无法成功声明设备，则它不能尝试将 FDO 附加到设备堆栈，只需从其 *AddDevice* 例程返回成功状态。 此类驱动程序将不会收到设备的 PnP 启动请求，但 PnP 管理器可能会为同一设备或不同设备再次调用其 *AddDevice* 例程。

有关初始化存储类驱动程序的详细信息，请参阅以下内容：

[存储类驱动程序的 DriverEntry 例程](storage-class-driver-s-driverentry-routine.md)

[存储类驱动程序的 AddDevice 例程](storage-class-driver-s-adddevice-routine.md)

另请参阅 [即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。

 

