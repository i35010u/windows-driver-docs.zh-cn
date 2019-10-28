---
title: 处理 IRP_MN_QUERY_STOP_DEVICE 请求（Windows 2000 及更高版本）
description: 处理 IRP_MN_QUERY_STOP_DEVICE 请求（Windows 2000 及更高版本）
ms.assetid: 668a920c-aadb-405a-9a1d-091982ca2c04
keywords:
- IRP_MN_QUERY_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e913c65594b193ea0ea2f4ce182a00229c611b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838666"
---
# <a name="handling-an-irp_mn_query_stop_device-request-windows-2000-and-later"></a>处理 IRP\_MN\_QUERY\_停止\_设备请求（Windows 2000 及更高版本）





将首先由设备堆栈中的顶层驱动程序处理[**IRP\_MN\_查询\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)请求，然后再处理下一个较低的驱动程序。 驱动程序处理其[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中的停止 irp。

为了响应**IRP\_MN\_QUERY\_停止\_设备**，驱动程序必须执行以下操作：

1.  确定是否可以停止设备，并释放其硬件资源，而不会产生负面影响。

    如果满足以下任一条件，则驱动程序必须使查询停止 IRP 失败：

    -   已通知驱动程序（通过[**IRP\_MN\_设备\_使用情况\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)），该设备位于分页、休眠或故障转储文件的路径中。

    -   无法释放设备的硬件资源。

    如果满足以下条件，驱动程序可能会导致查询停止 IRP 失败：

    -   驱动程序不得丢弃 i/o 请求，而且没有用于对 Irp 进行排队的机制。

        当设备处于停止状态时，驱动程序必须保留需要访问设备的 Irp。 如果驱动程序未将 Irp 排队，则它不得允许设备停止，因此必须使查询停止 IRP 失败。

        此规则的例外情况是允许删除 i/o 的设备。 此类设备的驱动程序可以成功地停止和停止请求，而无需对 Irp 进行排队。

2.  如果无法停止设备，则查询停止 IRP 将失败。

    将**Irp&gt;IoStatus**设置为适当的错误状态，使用 IO\_调用**IoCompleteRequest** ，不\_增量，并从驱动程序的*DispatchPnP*例程返回。 不要将 IRP 传递到下一个较低版本的驱动程序。

3.  如果设备可以停止并且驱动程序对 Irp 进行排队，请在设备扩展中设置 "保留\_新的\_请求" 标志，使后续的 Irp 排队（请参阅[在设备暂停时保留传入的 irp](holding-incoming-irps-when-a-device-is-paused.md)）。

    或者，设备的驱动程序可以延迟完全暂停设备，直到驱动程序收到后续[**IRP\_MN\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)请求。 但是，此类驱动程序必须将任何请求排队的请求排队，以防停止 IRP 到达时立即停止 IRP。 在重新启动设备之前，此类驱动程序必须对请求进行排队，如下所示：

    -   [**IRP\_MN\_设备\_使用\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)请求（例如，将分页文件放在设备上）。

    -   对同步传输的请求。

    -   创建会阻止驱动程序成功停止 IRP 的请求。

4.  如果设备不能有正在进行的 IRP，请确保传递给其他驱动程序例程和更低的驱动程序的所有未处理请求均已完成。

    驱动程序可以实现此目的的一种方法是使用引用计数和事件来确保所有请求都已完成：

    -   在其[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程中，驱动程序在设备扩展中定义一个 i/o 引用计数，并将该计数初始化为一个。

    -   此外，在其*AddDevice*例程中，驱动程序使用[**KeInitializeEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent)创建一个事件，并使用[**KeClearEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keclearevent)将该事件初始化为未终止状态。
    -   每次处理 IRP 时，驱动程序将使用[**InterlockedIncrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement)来递增引用计数。

    -   每次完成请求时，驱动程序都会将引用计数减为[**InterlockedDecrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockeddecrement)。

        如果请求有一个，则驱动程序将在[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程中递减引用计数，如果该驱动程序对该请求不使用*IoCompletion*例程，则会在调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)后立即递减引用计数。

    -   当驱动程序收到**IRP\_MN\_QUERY\_停止\_设备**时，它将使用**InterlockedDecrement**递减引用计数。 如果没有未完成的请求，则这会将引用计数减少到零。

    -   当引用计数达到零时，驱动程序会将事件设置为[**KeSetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)信号，指示查询停止代码可以继续。

    作为上述过程的替代方法，驱动程序可以将**IRP\_MN\_查询**序列化，\_停止正在进行的任何 irp 后面\_设备 IRP。

5.  执行将设备置于停止挂起状态所需的任何其他步骤。

    驱动程序成功执行查询停止 IRP 后，必须准备好成功 **\_MN\_停止\_设备**。

6.  完成 IRP。

    在函数或筛选器驱动程序中：

    -   将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS。

    -   用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)设置下一个堆栈位置，并将 IRP 传递到下一个带[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的驱动程序。

    -   将状态从**IoCallDriver**作为返回状态从*DispatchPnP*例程传播。

    -   不要完成 IRP。

    在总线驱动程序中：

    -   将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS。

        然而，如果总线上的设备使用硬件资源，请重新评估总线和子设备的资源要求。 如果任何要求已更改，则返回状态\_资源\_需求\_更改而不是状态\_成功。 此状态表示成功，但要求 PnP 管理器在发送停止 IRP 之前再次查询资源。

    -   通过 IO\_不\_递增来完成 IRP （[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)）。

    -   从*DispatchPnP*例程返回。

如果设备堆栈中的任何驱动程序失败， **IRP\_MN\_QUERY\_停止\_设备**，则 PnP 管理器会将[**irp\_MN\_取消\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)发送到设备堆栈。 这可以防止驱动程序要求使用*IoCompletion*例程进行查询停止 irp，以检测低级驱动程序是否失败了 IRP。

 

 




