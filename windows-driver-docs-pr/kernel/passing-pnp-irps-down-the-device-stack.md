---
title: 向设备堆栈的下层传递 PnP IRP
description: 向设备堆栈的下层传递 PnP IRP
ms.assetid: 339ef4b4-1b4f-42ac-ab57-c53b83120f0d
keywords:
- 即插即用 WDK 内核，将 Irp 传递下设备堆栈
- 即插即用和播放 WDK 内核，将 Irp 传递下设备堆栈
- WDK PnP Irp
- I/O 请求数据包 WDK 即插即用
- 将 Irp 传递下设备堆栈 WDK
- IoCompletion 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 758c438b51ed24e8875a6222135d800cf9096bb4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384748"
---
# <a name="passing-pnp-irps-down-the-device-stack"></a>向设备堆栈的下层传递 PnP IRP





PnP 管理器使用 Irp 直接驱动程序来启动、 停止和删除的设备和查询有关他们的设备的驱动程序。 所有 PnP Irp 具有主要函数代码[ **IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)，并且所有即插即用驱动程序必须提供[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程，以服务此函数代码。 PnP 管理器初始化**Irp-&gt;IoStatus.Status**于状态\_不\_支持发送 IRP 时。 有关详细信息，请参阅[DispatchPnP 例程](dispatchpnp-routines.md)。

即插即用次要 Irp 的列表，请参阅[即插即用和播放次要 Irp](plug-and-play-minor-irps.md)。

设备的所有驱动程序必须具有应对 PnP IRP，除非在堆栈中的驱动程序失败 IRP 的机会。 （请参阅下图。）

![说明传递设备堆栈的下层插 irp 的关系图](images/passpnp.png)

设备没有单个驱动程序可以假定它是唯一 PnP IRP 将响应的驱动因素。 举个例子，功能驱动程序用于响应[ **IRP\_MN\_查询\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)请求和完成而无需将其传递给 IRP下一步较低的驱动程序。 无较低的驱动程序支持的功能，如唯一实例 ID 或电源支持由父总线驱动程序管理功能报告。

当父总线驱动程序调用时，备份设备堆栈传输时 PnP IRP [ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) I/O 管理器调用任何[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程注册的函数驱动程序或筛选器驱动程序。

当它收到 PnP IRP，函数或筛选器驱动程序必须执行以下操作：

-   如果该驱动程序将 IRP 到响应中执行操作：
    1.  执行相应的操作。
    2.  设置**Irp-&gt;IoStatus.Status**到相应的状态，如状态\_成功。 设置**Irp-&gt;IoStatus.Information**，如果适合 IRP。
    3.  设置下一步堆栈位置与[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)或[ **IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)。 如果将调用后一种的例程*IoCompletion*例程。
    4.  设置*IoCompletion*例程，如有必要。
    5.  无法完成 IRP。 (不要调用**IoCompleteRequest**。)父总线驱动程序将完成 IRP。
-   如果该驱动程序不会执行此 IRP 的操作，它只是准备将 IRP 传递到下一步的驱动程序：
    1.  调用**IoSkipCurrentIrpStackLocation**从 IRP 删除其堆栈位置。
    2.  中未设置任何字段**Irp-&gt;IoStatus**。
    3.  未设置*IoCompletion*例程。
    4.  无法完成 IRP。 (不要调用**IoCompleteRequest**。)父总线驱动程序将完成 IRP。

如果函数或筛选器驱动程序没有失败 IRP，它将到下一个较低的驱动程序与传递 IRP [ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。 驱动程序都有指向下一个较低的驱动程序;从返回该指针[ **IoAttachDeviceToDeviceStack** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)更高版本的驱动程序中调用[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程。

父总线驱动程序完成后执行任何任务来响应 IRP IRP。 总线驱动程序调用后**IoCompleteRequest**，I/O 管理器调用任意*IoCompletion*例程注册的设备的函数或筛选器驱动程序。

 

 




