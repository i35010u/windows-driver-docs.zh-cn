---
title: 在函数驱动程序中删除设备
description: 在函数驱动程序中删除设备
ms.assetid: 46a75647-e72a-4194-be9d-070e3ac95650
keywords:
- 功能的驱动程序 WDK 即插即用
- DispatchPnP 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7bb956681e48579ca6d2b4a973c0cd1c5c41f05
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716919"
---
# <a name="removing-a-device-in-a-function-driver"></a>在函数驱动程序中删除设备





功能驱动程序时删除设备，必须撤消任何操作它执行添加和启动设备。 本文包括功能的外围设备的驱动程序和功能的总线的设备的驱动程序。

功能驱动程序将使用的过程如下所示在设备中删除其[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程：

1. 这是总线设备功能驱动程序？

   如果是这样，可能是删除任何未处理的子 PDOs 总线上的设备。

   如果总线驱动程序处理先前[ **IRP\_MN\_惊讶\_删除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)请求子设备，但该驱动程序尚未收到后续[ **IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求，总线驱动程序使子 PDO 保持不变。 在某些更高版本时，所有子设备句柄都关闭时，即插即用管理器将发送删除 IRP 子设备和总线驱动程序在当时删除的子节点 PDO。

   如果总线驱动程序处理先前**IRP\_MN\_删除\_设备**请求设备，而且已进行了任何后续**IRP\_MN\_惊讶\_删除**请求，然后总线驱动程序删除子 PDO。 在这种情况下，即插即用管理器可确保任何函数和筛选器驱动程序具有从子设备中删除 (DOs FDO 和筛选器已被删除) 之前它将删除 IRP 发送到父总线设备。 子 PDO 仍可能会显示，因此总线驱动程序之前必须先删除子 PDO 删除总线设备。

2. 该驱动程序已经处理先前**IRP\_MN\_惊讶\_删除**此 FDO 请求？

   如果是这样，执行任何剩余清理并跳到步骤 8 中， [ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。

   驱动程序通常维护设备扩展，该值指示是否已处理该驱动程序中的标志**IRP\_MN\_惊讶\_删除**对设备的请求。

3. 如果该驱动程序先前启用了唤醒设备，取消[ **IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)请求。

4. 请确保设备处于非活动状态。

   如果设备还不是处于非活动状态以响应前面**IRP\_MN\_查询\_删除\_设备**，驱动程序必须将设备标记为不接受新请求，并且必须完成在此驱动程序中对排队的任何请求。 该驱动程序时不能要求设备的访问权限的任何未完成请求。

   驱动程序可以使用**Io*Xxx*RemoveLock<em>Xxx</em>** 计数未完成 i/o 操作并设置一个事件，指示该删除处理例程可以继续。

5. 执行任何电源关闭操作。

   每个设备的驱动程序执行其电源关闭操作，如果有的话，当它收到**IRP\_MN\_删除\_设备**请求。 通常函数驱动程序，设备的电源策略所有者不会发送一个单独[ **IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)请求设置设备电源到 D3 的状态。 父总线驱动程序通常向插槽下提供支持，并通知使用电源管理器[ **PoSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerstate)总线驱动程序时获取删除 IRP。 有关其他信息，请参阅[电源管理](implementing-power-management.md)。

6. 通过调用来禁用任何设备接口[ **IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)。

7. 释放由驱动程序中使用的设备所有硬件资源。

   具体操作取决于设备和驱动程序，但可以包括断开与中断[ **IoDisconnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterrupt)，释放物理地址范围和[ **MmUnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmapiospace)，和释放 I/O 端口。

8. 传递**IRP\_MN\_删除\_设备**向下一步的驱动程序的请求。

   设置与下一个较低的驱动程序的 IRP 堆栈位置[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) ，并将 IRP 传递到下一步驱动程序与[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver).

   驱动程序不需要等待基础驱动程序来完成它们的删除操作后才能继续使用它删除活动。

9. 从设备堆栈中删除设备对象[ **IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodetachdevice)。

   指定为下一个较低的设备对象指针*目标设备*参数。 该驱动程序接收一个指针，此类调用[ **IoAttachDeviceToDeviceStack** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)中的驱动程序[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程。

10. 清理任何特定于设备的分配、 内存、 事件和等。

11. 免费使用 FDO [ **IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)。

12. 返回从[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程，将返回的状态传播**IoCallDriver**。

功能驱动程序未指定[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例行删除 IRP，也不会为它完成 IRP。 删除 Irp 父总线驱动程序已完成。

 

 




