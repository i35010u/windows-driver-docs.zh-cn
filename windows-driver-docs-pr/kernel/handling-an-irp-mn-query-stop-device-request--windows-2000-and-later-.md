---
title: " (Windows 2000 和更高版本处理 IRP_MN_QUERY_STOP_DEVICE 请求) "
description: " (Windows 2000 和更高版本处理 IRP_MN_QUERY_STOP_DEVICE 请求) "
ms.assetid: 668a920c-aadb-405a-9a1d-091982ca2c04
keywords:
- IRP_MN_QUERY_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5168c52e89a995e0a04f27ed02d4fdd4ce1db3e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186007"
---
# <a name="handling-an-irp_mn_query_stop_device-request-windows-2000-and-later"></a>处理 IRP \_ MN \_ 查询 \_ 停止 \_ 设备请求 (Windows 2000 和更高版本) 





[**IRP \_ MN \_ 查询 \_ 停止 \_ 设备**](./irp-mn-query-stop-device.md)请求首先由设备堆栈中的顶层驱动程序处理，然后再由下一个较低的驱动程序处理。 驱动程序处理其 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中的停止 irp。

为了响应 **IRP \_ MN \_ 查询 \_ 停止 \_ 设备**，驱动程序必须执行以下操作：

1.  确定是否可以停止设备，并释放其硬件资源，而不会产生负面影响。

    如果满足以下任一条件，则驱动程序必须使查询停止 IRP 失败：

    -   已通过 [**IRP \_ MN \_ 设备 \_ 使用 \_ 通知**](./irp-mn-device-usage-notification.md) (通知了驱动程序，) 设备位于分页、休眠或故障转储文件的路径中。

    -   无法释放设备的硬件资源。

    如果满足以下条件，驱动程序可能会导致查询停止 IRP 失败：

    -   驱动程序不得丢弃 i/o 请求，而且没有用于对 Irp 进行排队的机制。

        当设备处于停止状态时，驱动程序必须保留需要访问设备的 Irp。 如果驱动程序未将 Irp 排队，则它不得允许设备停止，因此必须使查询停止 IRP 失败。

        此规则的例外情况是允许删除 i/o 的设备。 此类设备的驱动程序可以成功地停止和停止请求，而无需对 Irp 进行排队。

2.  如果无法停止设备，则查询停止 IRP 将失败。

    将 **Irp &gt; IoStatus** 设置为适当的错误状态，使用 IO 无增量调用 **IoCompleteRequest** ， \_ \_ 并从驱动程序的 *DispatchPnP* 例程返回。 不要将 IRP 传递到下一个较低版本的驱动程序。

3.  如果设备可以停止并且驱动程序对 Irp 进行排队，请 \_ \_ 在设备扩展中设置 "保存新请求" 标志，使后续的 irp 排队 (请参阅 [在设备暂停时保留传入的 irp](holding-incoming-irps-when-a-device-is-paused.md)) 。

    或者，设备的驱动程序可以延迟完全暂停设备，直到驱动程序收到后续 [**IRP \_ MN \_ 停止 \_ 设备**](./irp-mn-stop-device.md) 请求。 但是，此类驱动程序必须将任何请求排队的请求排队，以防停止 IRP 到达时立即停止 IRP。 在重新启动设备之前，此类驱动程序必须对请求进行排队，如下所示：

    -   [**IRP \_MN \_ 设备 \_ 使用 \_ 通知**](./irp-mn-device-usage-notification.md) 请求 (例如，将页面文件放置在设备) 上。

    -   对同步传输的请求。

    -   创建会阻止驱动程序成功停止 IRP 的请求。

4.  如果设备不能有正在进行的 IRP，请确保传递给其他驱动程序例程和更低的驱动程序的所有未处理请求均已完成。

    驱动程序可以实现此目的的一种方法是使用引用计数和事件来确保所有请求都已完成：

    -   在其 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程中，驱动程序在设备扩展中定义一个 i/o 引用计数，并将该计数初始化为一个。

    -   此外，在其 *AddDevice* 例程中，驱动程序使用 [**KeInitializeEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent) 创建一个事件，并使用 [**KeClearEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keclearevent)将该事件初始化为未终止状态。
    -   每次处理 IRP 时，驱动程序将使用 [**InterlockedIncrement**](/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement)来递增引用计数。

    -   每次完成请求时，驱动程序都会将引用计数减为 [**InterlockedDecrement**](/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockeddecrement)。

        如果请求有一个，则驱动程序将在[*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程中递减引用计数，如果该驱动程序对该请求不使用*IoCompletion*例程，则会在调用[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)后立即递减引用计数。

    -   当驱动程序收到 **IRP \_ MN \_ 查询 \_ 停止 \_ 设备**时，它会将引用计数减为 **InterlockedDecrement**。 如果没有未完成的请求，则这会将引用计数减少到零。

    -   当引用计数达到零时，驱动程序会将事件设置为 [**KeSetEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent) 信号，指示查询停止代码可以继续。

    作为上述过程的替代方法，驱动程序可以将 **irp \_ MN \_ 查询 \_ 停止 \_ 设备** IRP 置于正在进行的任何 irp 之后。

5.  执行将设备置于停止挂起状态所需的任何其他步骤。

    当驱动程序成功执行查询停止 IRP 后，它必须已准备就绪，使 **irp \_ MN \_ 停止 \_ 设备**成功。

6.  完成 IRP。

    在函数或筛选器驱动程序中：

    -   将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"。

    -   用 [**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md) 设置下一个堆栈位置，并将 IRP 传递到下一个带 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的驱动程序。

    -   将状态从 **IoCallDriver** 作为返回状态从 *DispatchPnP* 例程传播。

    -   不要完成 IRP。

    在总线驱动程序中：

    -   将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"。

        然而，如果总线上的设备使用硬件资源，请重新评估总线和子设备的资源要求。 如果任何要求已更改，返回状态 \_ 资源 \_ 需求 \_ 更改而不是状态 \_ 成功。 此状态表示成功，但要求 PnP 管理器在发送停止 IRP 之前再次查询资源。

    -   完成 IRP ([**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) ，IO \_ 无 \_ 增量。

    -   从 *DispatchPnP* 例程返回。

如果设备堆栈中的任何驱动程序无法使用 **irp \_ MN \_ 查询 \_ 停止 \_ 设备**，PnP 管理器会将 [**irp \_ MN \_ 取消 \_ 停止 \_ 设备**](./irp-mn-cancel-stop-device.md) 发送到设备堆栈。 这可以防止驱动程序要求使用 *IoCompletion* 例程进行查询停止 irp，以检测低级驱动程序是否失败了 IRP。

 

