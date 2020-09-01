---
title: 处理设备通电 IRP
description: 处理设备通电 IRP
ms.assetid: 8fcfd324-97f9-4fd0-8fa1-87685c6b5ec3
keywords:
- 设置-power Irp WDK 内核
- 设备设置电源 Irp WDK 内核
- power Irp WDK 内核，设备更改
- 开启 Irp WDK 内核
- 启动电源管理 WDK 内核
- 正在还原电源 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18018efb1a5200b195161ca037f2de8650ee18c9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185267"
---
# <a name="handling-device-power-up-irps"></a>处理设备通电 IRP





设备开启 Irp 指定 [**IRP \_ MN \_ 设置 \_ 电源**](./irp-mn-set-power.md) 和设备电源状态，它需要比当前设备电源状态更多的功率。 通常，开机 IRP 指定设备工作状态 **PowerDeviceD0**。

必须首先通过设备的基础总线驱动程序处理设备的电源请求，然后在每个后续的驱动程序中备份堆栈。

下图显示了处理通电 IRP 所涉及的步骤。

![说明如何处理设备开机请求的关系图](images/devd0.png)

处理 **IRP \_ MN \_ 设置 \_ ** 电源请求以进行开机时，函数或筛选器驱动程序必须：

-   调用 [**IoAcquireRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) ，以确保在处理通电 IRP 时，驱动程序不会收到 [**IRP \_ MN \_ 删除 \_ 设备**](./irp-mn-remove-device.md) 请求。

    如果 **IoAcquireRemoveLock** 返回失败状态，驱动程序不应继续处理 IRP。 从 Windows Vista 开始，驱动程序应调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 来完成 IRP，然后返回失败状态。 在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序应调用 **IoCompleteRequest** 来完成 IRP，然后调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) 来启动下一个 power IRP，然后返回失败状态。

-   调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) ，将 IRP 标记为挂起。

-   调用 [**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) 以设置 IRP 堆栈位置。 如果驱动程序设置[*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，则不能调用**IoSkipCurrentIrpStackLocation** 。

-   调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 以设置开机 *IoCompletion* 例程。

    当处理设备开启 IRP 时，驱动程序应设置 *IoCompletion* 例程以还原上下文、释放删除锁定，并在 IRP 完成并且设备开机后执行其他必需的任务。 在完成 IRP 之前，驱动程序不应还原上下文。 有关详细信息，请参阅 [IoCompletion 例程 For Device Power irp](iocompletion-routines-for-device-power-irps.md)。

-   在 Windows 7 和 Windows Vista 中调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) () 或 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (Windows SERVER 2003、windows XP 和 WINDOWS 2000) 将 IRP 传递到下一个较低版本的驱动程序。 IRP 必须一直按设备堆栈向下移动到总线驱动程序。 仅允许总线驱动程序完成 IRP。

-   返回状态为 " \_ 挂起"。

当总线驱动程序收到 IRP 后，应该首先检查以确保设备仍然存在，并且在睡眠状态下未被删除或更换。 如果设备不再存在，则总线驱动程序应在父设备上调用 [**IoInvalidateDeviceRelations**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations) ，以通知即插即用管理器设备已消失。 在这种情况下，总线驱动程序可以使设备开启 IRP 失败。

如果设备仍然存在，则总线驱动程序会执行将设备恢复到操作条件所需的任务，调用 [**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate) 以通知电源管理器新设备电源状态，并完成 IRP ([**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) 。 如果驱动程序在设备进入睡眠状态时有排队 i/o，或者设备需要浪涌电源，则总线驱动程序会将电源应用到设备。 否则，当总线驱动程序必须与设备通信时，它就会应用电源。

若要获取从关机、待机和休眠状态快速启动时间的最佳实践列表，请参阅 [提高系统启动性能](improving-system-startup-performance.md)。

 

