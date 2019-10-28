---
title: 处理 IRP_MN_QUERY_REMOVE_DEVICE 请求
description: 处理 IRP_MN_QUERY_REMOVE_DEVICE 请求
ms.assetid: 30177e51-5312-4a24-972e-0c1c2d183d18
keywords:
- IRP_MN_QUERY_REMOVE_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd033b68d4ce3b38d86da4e8f2a02edcf93f8d96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838668"
---
# <a name="handling-an-irp_mn_query_remove_device-request"></a>处理 IRP\_MN\_查询\_删除\_设备请求





PnP 管理器发送此 IRP，以通知驱动程序要从计算机中删除设备，并询问是否可以在不中断计算机的情况下删除设备。 当用户请求更新设备的驱动程序时，它还会发送此 IRP。

PnP 管理器以 IRQL 被动\_级别在系统线程的上下文中发送此 IRP。

在将此 IRP 发送到设备的驱动程序之前，它将执行以下操作：

-   通知所有用户模式应用程序，这些应用程序在设备（或相关设备）上注册了通知。

    这包括在设备上注册了通知的应用程序、设备的一个子代（子设备、子项的子项等等），或某个设备的删除关系。 应用程序通过调用**RegisterDeviceNotification**注册此类通知。

    为响应此通知，应用程序将准备设备删除（关闭对设备的句柄）或查询失败。

-   通知所有在设备上注册为通知的内核模式驱动程序（或相关设备）。

    这包括在设备上注册了通知的驱动程序、设备的一个子代或某个设备的删除关系。 驱动程序通过调用事件类别为**EventCategoryTargetDeviceChange**的[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)注册此通知。

    响应此通知时，驱动程序会准备设备删除（关闭设备的句柄）或查询失败。

-   将[**IRP\_MN\_QUERY\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)irp 发送到设备后代的驱动程序。

-   （Windows 2000 及更高版本的系统）如果文件系统已装载到设备上，则 PnP 管理器会将查询-删除请求发送到文件系统和任何文件系统筛选器。 如果设备有打开的句柄，则文件系统通常无法通过查询-删除请求。 如果不是，则文件系统通常会锁定卷，以防以后再进行创建。 如果已装载的文件系统不支持查询删除请求，则 PnP 管理器将无法对设备执行查询删除请求。

如果上述所有步骤都成功，则 PnP 管理器会将**IRP\_MN\_QUERY\_删除\_设备**到设备的驱动程序中。

**IRP\_MN\_查询\_删除\_设备**请求首先由设备堆栈中的顶层驱动程序处理，然后再由下一个较低的驱动程序处理。 驱动程序会在其[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中处理删除 irp。

为了响应**IRP\_MN\_QUERY\_删除\_设备**，驱动程序必须执行以下操作：

1.  确定是否可以从计算机中删除设备而不中断操作。

    如果满足以下任一条件，则驱动程序必须使查询删除 IRP 失败：

    -   如果删除该设备，可能会导致数据丢失。

    -   如果组件具有设备的打开句柄，则为。 （这只是 Windows 98/Me 上的问题。 Windows 2000 和更高版本的 Windows 跟踪打开句柄，如果**IRP\_MN\_查询**后存在打开的句柄，则查询将失败，\_删除\_设备完成。）

    -   如果已收到驱动程序通知（通过[**IRP\_MN\_设备\_使用\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)IRP），则表示设备位于分页、故障转储或休眠文件的路径中。

    -   如果驱动程序对设备具有未完成的接口引用，则为。 也就是说，驱动程序提供了一个接口，以响应[**IRP\_MN\_QUERY\_接口**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)请求，但未取消引用接口。

2.  如果无法删除设备，则查询-删除 IRP 失败。

    将**Irp&gt;IoStatus**设置为适当的错误状态（通常\_状态为 "不成功"），使用 IO\_不\_增量调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ，并从驱动程序的*DispatchPnP*例程返回。 不要将 IRP 传递到下一个较低版本的驱动程序。

3.  如果驱动程序以前发送了[**IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)请求启用设备进行唤醒，则取消等待唤醒 IRP。

4.  记录设备以前的 PnP 状态。

    当驱动程序收到[**IRP\_MN\_query\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)请求时，驱动程序应记录设备所在的 PnP 状态，因为如果取消查询，驱动程序必须将设备返回到该状态（[**IRP\_MN\_取消\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)）。 以前的状态通常为 "已启动"，这是设备在驱动程序成功完成[**IRP\_MN\_开始\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求时输入的状态。

    但是，其他以前的状态是可能的。 例如，用户可能已通过设备管理器禁用了该设备。 或者，为了响应**IRP\_MN\_QUERY\_功能**请求，父总线驱动程序（或总线驱动程序上的筛选器驱动程序）可能报告设备的硬件已禁用。 在任一情况下，已禁用设备的驱动程序都可以接收**irp\_MN\_查询，\_** 在收到**irp\_MN\_START\_设备**请求之前，先删除\_设备请求。

5.  完成 IRP：

    在函数或筛选器驱动程序中：

    -   将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS。

    -   用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)设置下一个堆栈位置，并将 IRP 传递到下一个带[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的驱动程序。

    -   将状态从**IoCallDriver**作为返回状态从*DispatchPnP*例程传播。

    -   不要完成 IRP。

    在总线驱动程序中：

    -   将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS。

    -   通过 IO\_不\_递增来完成 IRP （[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)）。

    -   从*DispatchPnP*例程返回。

如果设备堆栈中的任何驱动程序未能通过**irp\_MN\_QUERY\_删除\_设备**，则 PnP 管理器会发送**IRP\_MN\_取消\_删除\_设备**到设备堆栈。 这可以防止驱动程序要求使用[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程进行查询-删除 irp 来检测低级驱动程序是否失败了 irp。

一旦驱动程序成功， **IRP\_MN\_QUERY\_删除\_设备**，并认为设备处于 "消除挂起" 状态，则驱动程序必须对设备的任何后续创建请求失败。 驱动程序会照常处理所有其他的 Irp，直到驱动程序收到**IRP\_MN\_CANCEL\_删除\_设备**或**IRP\_MN\_删除\_设备**。

 

 




