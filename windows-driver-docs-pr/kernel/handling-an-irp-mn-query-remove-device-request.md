---
title: 处理 IRP_MN_QUERY_REMOVE_DEVICE 请求
description: 处理 IRP_MN_QUERY_REMOVE_DEVICE 请求
keywords:
- IRP_MN_QUERY_REMOVE_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0983bb4869fd3d45fef67515f549aee032e5aa5f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801723"
---
# <a name="handling-an-irp_mn_query_remove_device-request"></a>处理 IRP \_ MN \_ 查询 \_ 删除 \_ 设备请求





PnP 管理器发送此 IRP，以通知驱动程序要从计算机中删除设备，并询问是否可以在不中断计算机的情况下删除设备。 当用户请求更新设备的驱动程序时，它还会发送此 IRP。

PnP 管理器在 \_ 系统线程的上下文中以 IRQL 被动级别发送此 IRP。

在将此 IRP 发送到设备的驱动程序之前，它将执行以下操作：

-   通知所有用户模式应用程序，这些应用程序在设备 (或相关设备) 上注册了通知。

    这包括在设备上注册了通知的应用程序、设备的一个子代 (子设备、子的子项等等) 或某个设备的删除关系。 应用程序通过调用 **RegisterDeviceNotification** 注册此类通知。

    为响应此通知，应用程序准备设备删除 (关闭设备的句柄) 或查询失败。

-   通知所有已注册到设备上的通知的内核模式驱动程序 (或相关设备) 。

    这包括在设备上注册了通知的驱动程序、设备的一个子代或某个设备的删除关系。 驱动程序通过调用事件类别为 **EventCategoryTargetDeviceChange** 的 [**IoRegisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)注册此通知。

    为响应此通知，驱动程序将准备设备删除 (关闭设备的句柄) 或查询失败。

-   将 [**IRP \_ MN \_ 查询 \_ 删除 \_ 设备**](./irp-mn-query-remove-device.md) irp 发送到设备后代的驱动程序。

-    (Windows 2000 及更高版本的系统) 如果在设备上装入了文件系统，则 PnP 管理器会将查询删除请求发送到文件系统和任何文件系统筛选器。 如果设备有打开的句柄，则文件系统通常无法通过查询-删除请求。 如果不是，则文件系统通常会锁定卷，以防以后再进行创建。 如果已装载的文件系统不支持查询删除请求，则 PnP 管理器将无法对设备执行查询删除请求。

如果上述所有步骤都成功，则 PnP 管理器会将 **IRP \_ MN \_ 查询 \_ 删除 \_ 设备** 发送到设备的驱动程序。

**IRP \_ MN \_ 查询 \_ 删除 \_ 设备** 请求首先由设备堆栈中的顶层驱动程序处理，然后再由下一个较低的驱动程序处理。 驱动程序会在其 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中处理删除 irp。

为了响应 **IRP \_ MN \_ 查询 \_ 删除 \_ 设备**，驱动程序必须执行以下操作：

1.  确定是否可以从计算机中删除设备而不中断操作。

    如果满足以下任一条件，则驱动程序必须使查询删除 IRP 失败：

    -   如果删除该设备，可能会导致数据丢失。

    -   如果组件具有设备的打开句柄，则为。  (仅在 Windows 98/Me 上出现问题。 Windows 2000 和更高版本的 Windows 跟踪打开句柄，如果 **IRP \_ MN \_ 查询 \_ 删除 \_ 设备** 完成后有打开句柄，则查询将失败。 ) 

    -   如果已通过 [**IRP \_ MN \_ 设备 \_ 使用情况 \_ 通知**](./irp-mn-device-usage-notification.md) IRP (通知了驱动程序，则) 设备位于分页、故障转储或休眠文件的路径中。

    -   如果驱动程序对设备具有未完成的接口引用，则为。 也就是说，驱动程序提供了一个接口，以响应 [**IRP \_ MN \_ 查询 \_ 接口**](./irp-mn-query-interface.md) 请求，但未取消引用接口。

2.  如果无法删除设备，则查询-删除 IRP 失败。

    将 **Irp- &gt; IoStatus** 设置为适当的错误状态 (通常状态为 \_ "不成功") ，使用 IO 无增量调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ， \_ \_ 并从驱动程序的 *DispatchPnP* 例程返回。 不要将 IRP 传递到下一个较低版本的驱动程序。

3.  如果驱动程序以前发送了 [**IRP \_ MN \_ 等待 \_ 唤醒**](./irp-mn-wait-wake.md) 请求以启用设备进行唤醒，请取消等待唤醒 IRP。

4.  记录设备以前的 PnP 状态。

    当驱动程序收到 [**IRP \_ MN \_ query \_ REMOVE \_ device**](./irp-mn-query-remove-device.md) 请求时，驱动程序应记录设备所在的 PnP 状态，因为如果删除该查询，则该驱动程序必须将该设备返回到该状态 ([**IRP \_ MN \_ CANCEL \_ REMOVE \_ device**](./irp-mn-cancel-remove-device.md)) 。 以前的状态通常为 "已启动"，即设备在驱动程序成功完成 [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md) 请求时输入的状态。

    但是，其他以前的状态是可能的。 例如，用户可能已通过设备管理器禁用了该设备。 或者，为响应 **IRP \_ MN \_ 查询 \_ 功能** 请求， (或总线驱动程序上的筛选器驱动程序) 可能报告设备的硬件已禁用。 在任一情况下，已禁用设备的驱动程序都可以在收到 **irp \_ MN \_ START \_ 设备** 请求之前接收 **irp \_ MN \_ 查询 \_ 删除 \_ 设备** 请求。

5.  完成 IRP：

    在函数或筛选器驱动程序中：

    -   将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"。

    -   用 [**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md) 设置下一个堆栈位置，并将 IRP 传递到下一个带 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的驱动程序。

    -   将状态从 **IoCallDriver** 作为返回状态从 *DispatchPnP* 例程传播。

    -   不要完成 IRP。

    在总线驱动程序中：

    -   将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"。

    -   完成 IRP ([**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) ，IO \_ 无 \_ 增量。

    -   从 *DispatchPnP* 例程返回。

如果设备堆栈中的任何驱动程序无法使用 **irp \_ MN \_ 查询 \_ 删除 \_ 设备**，PnP 管理器会将 **irp \_ MN \_ 取消 \_ 删除 \_ 设备** 发送到设备堆栈。 这可以防止驱动程序要求使用 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程进行查询-删除 irp 来检测低级驱动程序是否失败了 irp。

一旦驱动程序成功了 **IRP \_ MN \_ 查询 \_ 删除 \_ 设备** ，并认为设备处于 "消除挂起" 状态，则驱动程序必须对设备的任何后续创建请求失败。 驱动程序会照常处理所有其他 Irp，直到驱动程序收到 **IRP \_ MN \_ CANCEL \_ remove \_ 设备** 或 **irp \_ MN \_ 删除 \_ 设备**。

 

