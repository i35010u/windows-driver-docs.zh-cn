---
title: 处理 IRP_MN_STOP_DEVICE 请求（Windows 2000 和更高版本）
description: 处理 IRP_MN_STOP_DEVICE 请求（Windows 2000 和更高版本）
ms.assetid: 5e91748c-d03a-48f7-a9cc-df2801d8a555
keywords:
- IRP_MN_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6f992c337719cefb3229e43f8224f83e06b0a82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836592"
---
# <a name="handling-an-irp_mn_stop_device-request-windows-2000-and-later"></a>处理 IRP\_MN\_停止\_设备请求（Windows 2000 和更高版本）





[**IRP\_MN\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)请求首先由设备堆栈中的顶层驱动程序处理，然后再由下一个较低的驱动程序处理。 驱动程序处理其[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中的停止 irp。

驱动程序使用以下过程处理**IRP\_MN\_停止\_设备**请求：

1.  确保设备已暂停。

    如果驱动程序未完全暂停设备以响应[**IRP\_MN\_QUERY\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)请求，则它现在必须这样做。 在设备扩展中设置保留\_新的\_请求标志，并执行任何其他必需操作来暂停设备。

    设备在资源重新平衡操作期间可能会断电，因此可能会丢失设备状态。 设备的驱动程序应保存所有设备状态信息，并在接收到后续[**IRP\_MN\_START\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求时还原。

2.  释放设备的硬件资源。

    在函数驱动程序中，准确的操作依赖于设备和驱动程序，但可以包括断开中断与[**IoDisconnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt)的连接、释放使用[**MmUnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)的物理地址范围以及释放 i/o 端口。

    如果筛选器或总线驱动程序已获取设备的任何硬件资源，则该驱动程序必须释放资源以响应**IRP\_MN\_停止\_设备**请求。

3.  将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS。

4.  将 IRP 传递到下一个较低版本的驱动程序或完成 IRP。

    -   在函数或筛选器驱动程序中，使用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)设置下一个堆栈位置，使用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)将 IRP 传递到下一个较低的驱动程序，并从**IoCallDriver**返回状态作为返回状态*DispatchPnP*例程。 不要完成 IRP。

    -   在总线驱动程序中，使用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)和 IO 来完成 IRP\_不\_递增，并从*DispatchPnP*例程返回。

当设备停止重新平衡资源时，驱动程序无法启动任何访问该设备的 Irp。 驱动程序必须对此类 Irp 进行排队，如[设备暂停时保留传入的 irp](holding-incoming-irps-when-a-device-is-paused.md)中所述; 如果驱动程序未实现 IRP 持有的队列且不能丢弃 i/o 请求，则必须对其进行故障转移。

 

 




