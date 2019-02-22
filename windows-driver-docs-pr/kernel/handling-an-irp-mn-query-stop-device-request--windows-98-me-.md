---
title: 处理一个 IRP_MN_QUERY_STOP_DEVICE 请求 (Windows 98 / 我)
description: 处理一个 IRP_MN_QUERY_STOP_DEVICE 请求 (Windows 98 / 我)
ms.assetid: 2a12af98-c5ed-4a24-b957-b363683cc491
keywords:
- IRP_MN_QUERY_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fc2a7682541ff599f4336ab4d7d1499b179c4b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543508"
---
# <a name="handling-an-irpmnquerystopdevice-request-windows-98me"></a>处理 IRP\_MN\_查询\_停止\_设备请求 (Windows 98 / 我)





[ **IRP\_MN\_查询\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551725)设备堆栈中顶部驱动程序，然后按每个下一步的较低的驱动程序第一次处理请求。 驱动程序句柄停止 Irp 中的其[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

以响应**IRP\_MN\_查询\_停止\_设备**，驱动程序必须执行以下操作：

1.  确定是否可以停止而不会负面影响的设备。

    如果下列任何条件成立，驱动程序必须失败查询停止 IRP:

    -   通知驱动程序 (通过[ **IRP\_MN\_设备\_使用情况\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff550841)) 的设备位于路径中的分页、 休眠或崩溃转储文件。

    -   不能释放设备的硬件资源。

    -   有打开的句柄到设备。

    如果满足下列条件时，驱动程序可能会失败查询停止 IRP:

    -   该驱动程序必须删除 I/O 请求。

2.  如果不能停用设备，失败查询停止 IRP。

    设置**Irp-&gt;IoStatus.Status**到相应的错误状态，调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)与 IO\_否\_增量并返回来自驱动程序的[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 不将 IRP 传递给下一个较低的驱动程序。

3.  如果可以停用设备，则调用[ **IoSetDeviceInterfaceState** ](https://msdn.microsoft.com/library/windows/hardware/ff549700)并[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)若要禁用和取消注册任何用户模式下的接口。 然后开始失败要求设备的访问权限的任何传入的 I/O 请求。

    或者，设备的驱动程序可以推迟完全暂停设备，直到驱动程序接收后续**IRP\_MN\_停止\_设备**请求。 此类驱动程序，但是，应禁用并取消注册处理查询停止请求，以防止任何其他句柄打开到设备时，其用户模式接口。

    此外，此类驱动程序必须失败会阻止其到达时立即成功停止 IRP 的任何请求。 直到重新启动设备，此类驱动程序必须如下所示的请求失败：

    -   **IRP\_MN\_设备\_使用情况\_通知**（例如，若要将放在设备上的分页文件） 的请求。

    -   对同步传输的请求。

    -   创建将阻止驱动程序成功停止 IRP 的请求。

4.  如果设备不能允许 IRP，正在进行故障，请确保已完成的其他驱动程序例程并降低驱动程序传递任何未完成请求。

    驱动程序，可以实现此目的的一种方法是使用引用计数和事件以确保所有请求已都完成：

    -   在其[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程，该驱动程序设备扩展中定义的 I/O 引用计数并初始化一个计数。

    -   另外，在其*AddDevice*例程，该驱动程序创建的事件[ **KeInitializeEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff552137)并初始化为未发出信号状态与事件[**KeClearEvent**](https://msdn.microsoft.com/library/windows/hardware/ff551980)。

    -   每次处理 IRP，驱动程序使用的引用计数递增[ **InterlockedIncrement**](https://msdn.microsoft.com/library/windows/hardware/ff547910)。

    -   每次完成一个请求时驱动程序递减引用计数与[ **InterlockedDecrement**](https://msdn.microsoft.com/library/windows/hardware/ff547871)。

        驱动程序递减引用计数在[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程中，如果请求具有一个，或在调用后立即[ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)如果驱动程序使用无*IoCompletion*例程请求。

    -   当驱动程序收到**IRP\_MN\_查询\_停止\_设备**，则递减引用计数与**InterlockedDecrement**。 如果不有任何未完成的请求，这将减少引用计数为零。

    -   当引用计数达到零时，该驱动程序设置具有事件[ **KeSetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553253)发出信号表示查询停止代码可以继续。

    作为替代方法与上面的过程，驱动程序可以序列化**IRP\_MN\_查询\_停止\_设备**IRP 背后任何 Irp 正在进行中。

5.  执行将停止挂起状态中的设备所需的任何其他步骤。

    驱动程序成功查询停止 IRP 后，它必须准备好成功**IRP\_MN\_停止\_设备**。

6.  完成 IRP。

    在函数或筛选器驱动程序：

    -   设置**Irp-&gt;IoStatus.Status**于状态\_成功。

    -   设置下一步堆栈位置与[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355) ，并将 IRP 传递到下一个较低的驱动程序与[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336).

    -   传播将状态从**IoCallDriver**作为返回的状态*DispatchPnP*例程。

    -   无法完成 IRP。

    在总线驱动程序：

    -   设置**Irp-&gt;IoStatus.Status**于状态\_成功。

        不过，总线上的设备使用的硬件资源，请重新评估总线和子设备的资源的要求。 如果已更改的任何条件，则返回状态\_资源\_要求\_而不是状态更改\_成功。 此状态表示成功，但需要即插即用管理器再次发送停止 IRP 之前查询你的资源。

    -   完成 IRP ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)) 与 IO\_否\_增量。

    -   返回从*DispatchPnP*例程。

如果设备堆栈中的任何驱动程序失败**IRP\_MN\_查询\_停止\_设备**，即插即用管理器将发送[ **IRP\_MN\_取消\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff550826)到设备堆栈。 这可以防止驱动程序要求*IoCompletion*查询停止 IRP，以检测是否较低的驱动程序失败 IRP 的例程。

 

 




