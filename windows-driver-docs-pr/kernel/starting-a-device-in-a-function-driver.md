---
title: 在函数驱动程序中启动设备
description: 在函数驱动程序中启动设备
ms.assetid: 148a3128-9cb1-4a2c-a62e-45199476d968
keywords:
- 函数驱动程序 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb7b5f39d6526a13b60bcf42266cdfae4766ed66
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838410"
---
# <a name="starting-a-device-in-a-function-driver"></a>在函数驱动程序中启动设备





函数驱动程序设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，传递[**IRP\_MN\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)在设备堆栈中\_设备请求，并推迟其启动操作，直到所有较低版本的驱动程序都已使用 IRP 完成。 有关使用内核事件的详细信息，请参阅[推迟 PNP IRP 处理](postponing-pnp-irp-processing-until-lower-drivers-finish.md)，并使用*IOCOMPLETION*例程延迟 IRP 处理。

如果在所有较低版本的驱动程序都完成了 IRP 后， [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程重新获得控制权，则函数驱动程序将执行其任务以启动设备。 函数驱动程序使用如下所示的过程启动设备：

1.  如果低级驱动程序失败，IRP （[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)返回错误），则不会继续处理 irp。 执行任何必要的清理并从*DispatchPnP*例程返回（请执行到此列表中的最后一个步骤）。

2.  如果较低的驱动程序成功处理了 IRP，则启动设备。

    启动设备的具体步骤因设备而异。 此类步骤可能包括映射 i/o 空间，初始化硬件注册，将设备设置为 D0 电源状态，并将中断连接到[**IoConnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)。 如果在[**IRP\_MN\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)请求之后，驱动程序正在重新启动设备，则驱动程序的设备状态可能为 "正在还原"。

    必须打开设备，然后任何驱动程序才能访问设备。 有关详细信息，请参阅[打开设备](powering-up-a-device.md)。

    如果应为设备启用唤醒，则其电源策略所有者（通常为功能驱动程序）应在启动设备后、完成**IRP\_MN\_START\_设备**请求之前发送等待/唤醒 IRP。 有关详细信息，请参阅[发送等待/唤醒 IRP](sending-a-wait-wake-irp.md)。

3.  在 IRP 中启动 irp-保存队列。

    清除 "驱动程序定义的保留\_新建\_请求" 标志，并在 IRP 保留队列中启动 Irp。 当首次启动设备时，以及在查询停止或停止 IRP 后重新启动设备时，驱动程序应执行此操作。 有关详细信息，请参阅[在设备暂停时保留传入 irp](holding-incoming-irps-when-a-device-is-paused.md) 。

4.  \[可选\] 通过调用[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)来启用设备接口。

    启用驱动程序先前在其[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程中注册的接口（如果有），或在 INF 或其他组件（如共同安装程序）中注册。

    在 Windows 2000 和更高版本的 Windows 上，PnP 管理器不会发送设备接口到达通知，直到**IRP\_MN\_START\_设备**IRP 完成，指出设备的所有驱动程序都具有已完成其启动操作。 PnP 管理器还会使在设备的所有驱动程序都完成启动 IRP 之前到达的任何创建请求失败。

5.  完成 IRP。

    函数驱动程序的*IoCompletion*例程返回状态\_\_需要更多的\_处理，如[推迟 PnP IRP 处理直到较低的驱动程序完成](postponing-pnp-irp-processing-until-lower-drivers-finish.md)，使函数驱动程序的*DispatchPnP*例程必须调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)才能恢复 i/o 完成处理。

    如果函数驱动程序的启动操作成功，则驱动程序将**Irp&gt;IOSTATUS**状态设置为 STATUS\_SUCCESS，调用**IoCompleteRequest** ，同时提升 IO\_no\_增量，并返回状态从*DispatchPnP*例程成功\_。

    如果函数驱动程序在启动操作过程中遇到错误，则驱动程序会在 IRP 中设置错误状态，使用 IO\_调用**IoCompleteRequest** ，而不\_增量，并从其*DispatchPnP*例程返回错误。

    如果低级驱动程序失败，IRP （**IoCallDriver**返回了一个错误），则函数驱动程序将使用 IO 调用**IOCOMPLETEREQUEST** ，\_不\_递增，并从其*DispatchPnP*例程返回**IoCallDriver**错误。 在这种情况下，函数驱动程序不会设置**Irp&gt;IoStatus** ，因为状态已由降级 Irp 的低级驱动程序设置。

当函数驱动程序收到**IRP\_MN\_开始\_设备**请求时，它应检查**IrpSp-&gt;参数 StartDevice 的结构。 AllocatedResources**和**IrpSp-&gt;StartDevice. AllocatedResourcesTranslated**，分别描述 PnP 管理器分配给设备的原始资源和已转换资源。 驱动程序应将每个资源列表的副本作为调试辅助保存在设备扩展中。

资源列表是成对的[**CM\_资源\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)结构，其中原始列表的每个元素对应于已翻译列表的同一个元素。 例如，如果**AllocatedResources**\[0\] 描述原始 i/o 端口范围，则**AllocatedResourcesTranslated**\[0\] 在转换后描述相同的范围。 每个翻译的资源都包含物理地址和资源的类型。

如果为驱动程序分配了已转换的内存资源（**CmResourceTypeMemory**），则它必须调用[**MmMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)将物理地址映射到可通过其访问设备寄存器的虚拟地址。 若要使驱动程序以独立于平台的方式运行，应检查每个返回的已转换资源，并根据需要对其进行映射。

函数驱动程序应执行以下操作来响应**IRP\_MN\_启动\_设备**，以确保对所有设备资源的访问：

1.  将**IrpSp-&gt;StartDevice. AllocatedResources**复制到设备扩展。

2.  将**IrpSp-&gt;StartDevice. AllocatedResourcesTranslated**复制到设备扩展。

3.  在循环中，检查**AllocatedResourcesTranslated**中的每个描述符元素。 如果描述符资源类型为**CmResourceTypeMemory**，则调用**MmMapIoSpace**，同时传递已转换资源的物理地址和长度。

当驱动程序收到**IRP\_MN\_停止\_设备**， **irp\_MN\_删除\_设备**，或**irp\_MN\_意外\_删除**请求，它必须通过在类似循环中调用[**MmUnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)来释放映射。 如果 **\_启动\_设备**请求，则该驱动程序还应调用**MmUnmapIoSpace** ，从而使 IRP\_MN 无法启动。

有关详细信息，请参阅[将与总线相关的地址映射到虚拟地址](mapping-bus-relative-addresses-to-virtual-addresses.md)。

 

 




