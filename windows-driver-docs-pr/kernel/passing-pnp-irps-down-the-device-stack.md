---
title: 向设备堆栈的下层传递 PnP IRP
description: 向设备堆栈的下层传递 PnP IRP
ms.assetid: 339ef4b4-1b4f-42ac-ab57-c53b83120f0d
keywords:
- PnP WDK 内核，将 Irp 向下传递到设备堆栈
- 即插即用 WDK 内核，将 Irp 向下传递到设备堆栈
- Irp WDK PnP
- I/o 请求数据包 WDK PnP
- 将 Irp 向下传递设备堆栈 WDK
- IoCompletion 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d76dd93e9d875c315ec4649e2238b8b414b298d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838517"
---
# <a name="passing-pnp-irps-down-the-device-stack"></a>向设备堆栈的下层传递 PnP IRP





PnP 管理器使用 Irp 定向驱动程序来启动、停止和删除设备，并查询有关其设备的驱动程序。 所有 PnP Irp 的主要功能代码[**IRP 都\_MJ\_PnP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)，所有 pnp 驱动程序都必须提供[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程来为此函数代码提供服务。 PnP 管理器会将**irp&gt;IoStatus**状态初始化为状态\_在发送 IRP 时不\_支持。 有关详细信息，请参阅[DispatchPnP 例程](dispatchpnp-routines.md)。

有关 PnP 次要 Irp 的列表，请参阅[即插即用次 irp](plug-and-play-minor-irps.md)。

设备的所有驱动程序都必须有机会响应 PnP IRP，除非堆栈中的驱动程序失败 IRP。 （请参见下图。）

![说明如何将即插即用 irp 向下传递到设备堆栈的关系图](images/passpnp.png)

设备没有单个驱动程序可以假定它是将响应 PnP IRP 的唯一驱动程序。 例如，请考虑一个用于响应[**IRP\_MN\_查询\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)请求并完成 IRP 的函数驱动程序，而不将其传递到下一个较低版本的驱动程序。 不会报告低级驱动程序支持的任何功能，例如唯一的实例 ID 或父总线驱动程序支持的电源管理功能。

当父总线驱动程序调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)并且 i/o 管理器调用由函数驱动程序或筛选器驱动程序注册的任何[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程时，PnP IRP 将在设备堆栈中向上移动。

函数或筛选器驱动程序在收到 PnP IRP 时必须执行以下操作：

-   如果驱动程序执行操作来响应 IRP：
    1.  执行相应的操作。
    2.  将**Irp&gt;IoStatus**设置为适当的状态，如 STATUS\_SUCCESS。 如果适用于 IRP，请设置**irp&gt;IoStatus。**
    3.  设置下一个堆栈位置，其中包含[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)或[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)。 如果设置了*IoCompletion*例程，则调用后一例程。
    4.  如有必要，请设置*IoCompletion*例程。
    5.  不要完成 IRP。 （请勿调用**IoCompleteRequest**。）父总线驱动程序将完成 IRP。
-   如果该驱动程序不执行此 IRP 的操作，它只是准备将 IRP 传递到下一个驱动程序：
    1.  调用**IoSkipCurrentIrpStackLocation**从 IRP 中删除其堆栈位置。
    2.  请勿在**Irp&gt;IoStatus**中设置任何字段。
    3.  不要设置*IoCompletion*例程。
    4.  不要完成 IRP。 （请勿调用**IoCompleteRequest**。）父总线驱动程序将完成 IRP。

如果函数或筛选器驱动程序未失败 IRP，它会将 IRP 传递到带有[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的下一个较低版本的驱动程序。 驱动程序具有指向下一个较低驱动程序的指针;该指针是从较高驱动程序的[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程中的[**IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)调用返回的。

父总线驱动程序在执行任何任务以响应 IRP 后完成 IRP。 在总线驱动程序调用**IoCompleteRequest**后，i/o 管理器将调用由该函数注册的任何*IoCompletion*例程或该设备的筛选器驱动程序。

 

 




