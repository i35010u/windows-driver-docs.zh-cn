---
title: 处理一个 IRP_MN_QUERY_REMOVE_DEVICE 请求
description: 处理一个 IRP_MN_QUERY_REMOVE_DEVICE 请求
ms.assetid: 30177e51-5312-4a24-972e-0c1c2d183d18
keywords:
- IRP_MN_QUERY_REMOVE_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a34dcd72d4c683f819630b16bf211f4d947915d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542152"
---
# <a name="handling-an-irpmnqueryremovedevice-request"></a>处理 IRP\_MN\_查询\_删除\_设备请求





PnP 管理器将发送此 IRP，以通知设备是要从计算机中删除并询问是否可以无需中断在计算机中删除该设备驱动程序。 它还会发送此 IRP，当用户请求来更新设备驱动程序。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别在系统线程的上下文中。

它执行以下操作之前将此 IRP 发送到设备的驱动程序：

-   通知所有用户模式应用程序注册的设备 （或相关的设备） 上的通知。

    这包括为通知或某个设备的删除关系上设备的后代 （子设备，子节点和等的子级） 之一的设备上注册的应用程序。 应用程序通过调用此类通知注册**RegisterDeviceNotification**。

    在响应此通知，应用程序准备用于设备删除 （设备关闭句柄） 或查询失败。

-   通知所有内核模式驱动程序的注册设备 （或相关的设备） 上的通知。

    这包括为通知或某个设备的删除关系上设备的后代之一的设备上注册的驱动程序。 驱动程序通过调用注册此通知[ **IoRegisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff549526)事件类别**EventCategoryTargetDeviceChange**。

    在响应此通知时，驱动程序准备用于设备删除 （设备关闭句柄） 或查询失败。

-   将发送[ **IRP\_MN\_查询\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551705) Irp 到设备的后代的驱动程序。

-   （Windows 2000 和更高版本系统）如果在设备上装载文件系统后，即插即用管理器将查询删除请求发送到文件系统和任何文件系统筛选器。 如果有打开的句柄到设备，文件系统通常会失败的查询删除请求。 如果不是，文件系统通常锁定以防止未来的卷创建成功。 如果已装载的文件系统不支持查询和删除请求，即插即用管理器进行故障设备的查询删除请求。

如果所有上述步骤成功，即插即用管理器发送**IRP\_MN\_查询\_删除\_设备**到设备的驱动程序。

**IRP\_MN\_查询\_删除\_设备**设备堆栈中顶部驱动程序，然后按每个下一步的较低的驱动程序第一次处理请求。 驱动程序句柄删除 Irp 中的其[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

以响应**IRP\_MN\_查询\_删除\_设备**，驱动程序必须执行以下操作：

1.  确定是否在设备可以从计算机中删除无需中断操作。

    如果下列任何条件成立，驱动程序必须失败查询删除 IRP:

    -   如果删除该设备可能会导致数据丢失。

    -   如果组件具有设备的打开句柄。 (这是 Windows 98 上的问题 / 只是我。 Windows 2000 和更高版本的 Windows 跟踪打开的句柄和失败查询是否存在后打开的句柄**IRP\_MN\_查询\_删除\_设备**完成。)

    -   如果驱动程序通知 (通过[ **IRP\_MN\_设备\_使用情况\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff550841) IRP) 设备正在分页的路径故障转储或休眠文件。

    -   如果该驱动程序具有对该设备的未完成的接口引用。 也就是说，该驱动程序提供响应的接口[ **IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687)请求和接口不已取消引用。

2.  如果不能删除该设备，失败查询删除 IRP。

    设置**Irp-&gt;IoStatus.Status**到相应的错误状态 (通常状态\_未成功)，调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)与IO\_否\_增量和从驱动程序的返回*DispatchPnP*例程。 不将 IRP 传递给下一个较低的驱动程序。

3.  如果该驱动程序以前发送[ **IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766)启用唤醒设备，请取消等待唤醒 IRP 的请求。

4.  记录的前一的即插即用设备状态。

    驱动程序应记录时驱动程序收到所在设备的即插即用状态[ **IRP\_MN\_查询\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551705)请求因为该驱动程序必须将设备恢复为该状态如果查询已取消 ([**IRP\_MN\_取消\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff550823)). 以前的状态通常"启动"，这是设备驱动程序已成功完成时将进入的状态[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求。

    但是，其他以前的状态是可能的。 例如，用户可能会禁用设备通过设备管理器。 或者，以响应**IRP\_MN\_查询\_功能**请求时，父总线驱动程序 （或总线驱动程序上的筛选器驱动程序） 可能已报告设备的硬件已禁用。 已禁用的设备的驱动程序可以在任一情况下，接收**IRP\_MN\_查询\_删除\_设备**之前收到请求**IRP\_MN\_启动\_设备**请求。

5.  完成 IRP:

    在函数或筛选器驱动程序：

    -   设置**Irp-&gt;IoStatus.Status**于状态\_成功。

    -   设置下一步堆栈位置与[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355) ，并将 IRP 传递到下一个较低的驱动程序与[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336).

    -   传播将状态从**IoCallDriver**作为返回的状态*DispatchPnP*例程。

    -   无法完成 IRP。

    在总线驱动程序：

    -   设置**Irp-&gt;IoStatus.Status**于状态\_成功。

    -   完成 IRP ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)) 与 IO\_否\_增量。

    -   返回从*DispatchPnP*例程。

如果设备堆栈中的任何驱动程序失败**IRP\_MN\_查询\_删除\_设备**，即插即用管理器将发送**IRP\_MN\_取消\_删除\_设备**到设备堆栈。 这可以防止驱动程序要求[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)查询删除 IRP，以检测是否较低的驱动程序失败 IRP 的例程。

驱动程序成功后**IRP\_MN\_查询\_删除\_设备**并且它认为设备处于挂起删除状态，该驱动程序必须失败任何后续的创建设备的请求数。 该驱动程序处理所有其他 Irp 像往常一样，直到该驱动程序收到**IRP\_MN\_取消\_删除\_设备**或者**IRP\_MN\_删除\_设备**。

 

 




