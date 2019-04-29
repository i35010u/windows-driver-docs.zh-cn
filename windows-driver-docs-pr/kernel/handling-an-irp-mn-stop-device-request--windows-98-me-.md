---
title: 处理 IRP_MN_STOP_DEVICE 请求 (Windows 98/Me)
description: 处理 IRP_MN_STOP_DEVICE 请求 (Windows 98/Me)
ms.assetid: 8e44561a-f494-48ce-ab61-aa47cd4e1c64
keywords:
- IRP_MN_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03da1c3a70c56ef7c4575476d2117b23dd21206f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359779"
---
# <a name="handling-an-irpmnstopdevice-request-windows-98me"></a>处理 IRP\_MN\_停止\_设备请求 (Windows 98 / 我)





在 Windows 98 上 / 我，即插即用管理器通常会发送[ **IRP\_MN\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551755)后成功查询停止请求。 但是，如果设备堆栈之前失败[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求，即插即用管理器将发送**IRP\_MN\_停止\_设备**而无需上述查询的请求。

**IRP\_MN\_停止\_设备**设备堆栈中顶部驱动程序，然后按每个下一步的较低的驱动程序第一次处理请求。 驱动程序句柄停止 Irp 中的其[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

驱动程序处理**IRP\_MN\_停止\_设备**请求的过程如下所示：

1.  请确保设备已暂停。

    如果驱动程序未完全暂停设备响应[ **IRP\_MN\_查询\_停止**](https://msdn.microsoft.com/library/windows/hardware/ff551725)请求，它现在必须执行此操作。

    虽然它已停止，因此可能会丢失设备状态，设备可能会丢失电源。 这些设备驱动程序应保存的任何设备状态信息并将其还原时它们接收后续**IRP\_MN\_启动\_设备**请求。

2.  发布设备的硬件资源。

    到函数的驱动程序，具体操作取决于设备和驱动程序，但可以包括断开与中断[ **IoDisconnectInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff549089)，释放物理地址范围与[ **MmUnmapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff556387)，和释放 I/O 端口。

    如果筛选器或总线驱动程序获得设备的任何硬件资源，则该驱动程序必须释放资源以响应所**IRP\_MN\_停止\_设备**请求。

3.  设置**Irp-&gt;IoStatus.Status**于状态\_成功。

4.  将 IRP 传递给下一个较低的驱动程序或完成 IRP。

    -   在函数或筛选器驱动程序，将设置为下一步堆栈位置与[ **IoSkipCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff550355)，将 IRP 传递到下一个较低的驱动程序与[ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)，并返回从状态**IoCallDriver**返回的状态作为*DispatchPnP*例程。 无法完成 IRP。

    -   总线驱动程序，在完成 IRP 使用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)与 IO\_否\_增量和从返回*DispatchPnP*例程。

驱动程序无法启动时停止设备访问设备的任何 Irp。 驱动程序必须使此类 Irp 失败。

 

 




