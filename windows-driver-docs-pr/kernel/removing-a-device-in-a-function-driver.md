---
title: 在函数驱动程序中删除设备
description: 在函数驱动程序中删除设备
ms.assetid: 46a75647-e72a-4194-be9d-070e3ac95650
keywords:
- 函数驱动程序 WDK PnP
- DispatchPnP 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3981fa0336a209a891b8cbeac33ca82b87ec698d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187581"
---
# <a name="removing-a-device-in-a-function-driver"></a>在函数驱动程序中删除设备





删除设备时，函数驱动程序必须撤消它为添加和启动设备执行的任何操作。 本讨论包含用于外围设备的功能驱动程序和总线设备的功能驱动程序。

函数驱动程序在其 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中使用如下所示的过程删除设备：

1. 这是否是总线设备的函数驱动程序？

   如果是这样，可能会为总线上的设备删除任何未完成的子 PDOs。

   如果总线驱动程序已处理子设备的上一个 [**irp \_ MN \_ 意外 \_ 删除**](./irp-mn-surprise-removal.md) 请求，但驱动程序尚未收到后续的 [**irp \_ MN \_ REMOVE \_ 设备**](./irp-mn-remove-device.md) 请求，则总线驱动程序会使子 PDO 保持不变。 稍后，当关闭子设备的所有句柄时，PnP 管理器将为子设备发送删除 IRP，并且总线驱动程序会在该时间删除子 PDO。

   如果总线驱动程序处理了以前的 **irp \_ MN \_ 删除 \_ ** 设备的设备请求，但没有后续 **irp MN 的 \_ \_ 意外 \_ 删除** 请求，则总线驱动程序将删除子 PDO。 在这种情况下，PnP 管理器可确保在将删除 IRP 发送到父总线设备之前，已)  (FDO 和 filter DOs 删除了子设备中的任何函数和筛选器驱动程序。 子 PDO 可能仍然存在，因此，在删除总线设备之前，总线驱动程序必须删除子 PDO。

2. 该驱动程序是否已处理过对此 FDO 的以前的 **IRP \_ MN \_ 意外 \_ 删除** 请求？

   如果是这样，请执行剩余的任何清理操作，并跳到步骤 8 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)。

   驱动程序通常在设备扩展中维护一个标志，该标志指示驱动程序是否已处理对设备的 **IRP \_ MN \_ 意外 \_ 删除** 请求。

3. 如果驱动程序先前启用了设备进行唤醒，则取消 [**IRP \_ MN \_ WAIT \_ 唤醒**](./irp-mn-wait-wake.md) 请求。

4. 确保设备处于非活动状态。

   如果设备未处于非活动状态，无法响应之前的 **IRP \_ MN \_ 查询 \_ 删除 \_ 设备**，则驱动程序必须将设备标记为不接受新请求，并且必须完成此驱动程序中排队的任何请求。 驱动程序必须对需要访问设备的任何未完成的请求失败。

   驱动程序可以使用**Io*Xxx*RemoveLock<em>Xxx</em> **例程来计算未完成 i/o，并设置一个事件，指示删除处理可以继续。

5. 执行任何关闭操作。

   设备的每个驱动程序在收到 **IRP \_ MN \_ REMOVE \_ 设备** 请求时执行其关机操作（如果有）。 设备的电源策略所有者（通常是函数驱动程序）不会发送单独的 [**IRP \_ MN \_ 设置 \_ 电源**](./irp-mn-set-power.md) 请求，以将设备电源状态设置为 D3。 父总线驱动程序通常会关闭槽，并在总线驱动程序获取删除 IRP 时向电源管理器通知 [**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate) 。 有关其他信息，请参阅 [电源管理](./introduction-to-power-management.md)。

6. 通过调用 [**IoSetDeviceInterfaceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)禁用任何设备接口。

7. 释放驱动程序使用的设备的所有硬件资源。

   具体的操作取决于设备和驱动程序，但可以包括通过 [**IoDisconnectInterrupt**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt)断开中断、释放使用 [**MmUnmapIoSpace**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)的物理地址范围以及释放 i/o 端口。

8. 将 **IRP \_ MN \_ 删除 \_ 设备** 请求向下传递到下一个驱动程序。

   为下一个较低版本的驱动程序设置 IRP 堆栈位置 [**，并将**](./mm-bad-pointer.md) irp 传递到带有 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的下一个驱动程序。

   在继续执行删除操作之前，驱动程序不需要等待底层驱动程序完成删除操作。

9. 从设备堆栈中删除具有 [**IoDetachDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)的设备对象。

   指定指向下一个较低设备对象的指针作为 *目标设备* 参数。 驱动程序从对驱动程序的[*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程的[**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)的调用接收此类指针。

10. 清理任何特定于设备的分配、内存和事件等。

11. 将 FDO 与 [**IoDeleteDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)一起释放。

12. 从 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程返回，并从 **IoCallDriver**传播返回状态。

函数驱动程序不会为删除 IRP 指定 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，也不会完成 irp。 删除 Irp 由父总线驱动程序完成。

 

