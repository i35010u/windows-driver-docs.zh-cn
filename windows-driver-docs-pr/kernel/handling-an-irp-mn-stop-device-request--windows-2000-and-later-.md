---
title: 处理 IRP_MN_STOP_DEVICE 请求（Windows 2000 和更高版本）
description: 处理 IRP_MN_STOP_DEVICE 请求（Windows 2000 和更高版本）
keywords:
- IRP_MN_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5530eb634d2534a9d6838c9308c46718f5626687
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801707"
---
# <a name="handling-an-irp_mn_stop_device-request-windows-2000-and-later"></a>处理 IRP \_ MN \_ 停止 \_ 设备请求 (Windows 2000 和更高版本) 





[**IRP \_ MN \_ 停止 \_ 设备**](./irp-mn-stop-device.md)请求首先由设备堆栈中的顶层驱动程序处理，然后再由下一个较低的驱动程序处理。 驱动程序处理其 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中的停止 irp。

驱动程序使用如下所示的过程来处理 **IRP \_ MN \_ 停止 \_ 设备** 请求：

1.  确保设备已暂停。

    如果驱动程序未完全暂停设备以响应 [**IRP \_ MN \_ 查询 \_ 停止 \_ 设备**](./irp-mn-query-stop-device.md) 请求，则必须立即执行此操作。 \_ \_ 在设备扩展中设置 "保存新请求" 标志，并执行任何其他必需操作来暂停设备。

    设备在资源重新平衡操作期间可能会断电，因此可能会丢失设备状态。 设备的驱动程序应保存所有设备状态信息，并在收到后续 [**IRP \_ MN \_ START \_ 设备**](./irp-mn-start-device.md) 请求时还原。

2.  释放设备的硬件资源。

    在函数驱动程序中，准确的操作依赖于设备和驱动程序，但可以包括断开中断与 [**IoDisconnectInterrupt**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt)的连接、释放使用 [**MmUnmapIoSpace**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)的物理地址范围以及释放 i/o 端口。

    如果筛选器或总线驱动程序已获取设备的任何硬件资源，则该驱动程序必须释放资源以响应 **IRP \_ MN \_ 停止 \_ 设备** 请求。

3.  将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"。

4.  将 IRP 传递到下一个较低版本的驱动程序或完成 IRP。

    -   在函数或筛选器驱动程序中，使用 [**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md)设置下一个堆栈位置，使用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)将 IRP 传递到下一个较低的驱动程序，并从 **IoCallDriver** 返回状态作为 *DispatchPnP* 例程的返回状态。 不要完成 IRP。

    -   在总线驱动程序中，使用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 和 IO 无增量来完成 IRP， \_ \_ 并从 *DispatchPnP* 例程中返回。

当设备停止重新平衡资源时，驱动程序无法启动任何访问该设备的 Irp。 驱动程序必须对此类 Irp 进行排队，如 [设备暂停时保留传入的 irp](holding-incoming-irps-when-a-device-is-paused.md)中所述; 如果驱动程序未实现 IRP 持有的队列且不能丢弃 i/o 请求，则必须对其进行故障转移。

 

