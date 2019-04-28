---
title: 在函数驱动程序中启动设备
description: 在函数驱动程序中启动设备
ms.assetid: 148a3128-9cb1-4a2c-a62e-45199476d968
keywords:
- 功能的驱动程序 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4df2793edb316b5433edd1e2a7f62107bd362c95
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331961"
---
# <a name="starting-a-device-in-a-function-driver"></a>在函数驱动程序中启动设备





功能驱动程序设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程，传递[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)堆栈的下层设备，请求并推迟其开始操作，直到 IRP 用完所有较低的驱动程序。 请参阅[推迟 PnP IRP 处理直到较低的驱动程序完成](postponing-pnp-irp-processing-until-lower-drivers-finish.md)有关使用内核事件的详细信息和一个*IoCompletion*推迟 IRP 处理例程。

当其[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程重新获得控制 IRP 用完所有较低的驱动程序后，功能驱动程序执行其任务，用于启动设备。 功能驱动程序使设备开始使用的过程如下所示：

1.  如果较低的驱动程序失败 IRP ([**IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)返回了错误)，不要继续处理 IRP。 执行任何必要的清理，并返回从*DispatchPnP*例程 （转到此列表中的最后一步）。

2.  如果较低的驱动程序已成功处理 IRP，启动设备。

    若要启动设备的确切步骤不同设备的。 此类步骤可能包括映射 I/O 空间以及正在初始化硬件寄存器，D0 电源状态，在设置设备连接与中断[ **IoConnectInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff548371)。 如果该驱动程序正在重新启动后的设备[ **IRP\_MN\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551755)请求，该驱动程序可能必须要还原的设备状态。

    必须打开设备，任何驱动程序可以访问它。 请参阅[增强设备](powering-up-a-device.md)有关详细信息。

    如果设备应为唤醒启用之后设备并在完成之前为其提供支持,，其电源策略所有者 （通常是功能驱动程序） 应发送等待/唤醒 IRP **IRP\_MN\_启动\_设备**请求。 有关详细信息，请参阅[发送等待/唤醒 IRP](sending-a-wait-wake-irp.md)。

3.  启动 Irp IRP 控股队列中。

    清除该驱动程序定义的保留\_新建\_请求标志和启动 Irp IRP 控股队列中。 驱动程序应执行此操作在第一次并在查询停止后重新启动设备启动设备时，或停止 IRP。 请参阅[持有传入 Irp 时设备暂停](holding-incoming-irps-when-a-device-is-paused.md)有关详细信息。

4.  \[可选\]启用设备的接口，通过调用[ **IoSetDeviceInterfaceState**](https://msdn.microsoft.com/library/windows/hardware/ff549700)。

    启用在以前注册的驱动程序接口，如果有，其[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程 （或在 INF 或另一个组件，如共同安装程序）。

    在 Windows 2000 和更高版本的 Windows，即插即用管理器不会发送通知直到设备接口到达**IRP\_MN\_启动\_设备**IRP 完成后，该值指示所有设备的驱动程序已完成其启动操作。 PnP 管理器也会失败前该设备的所有驱动程序完成开始 IRP 到达任何创建请求。

5.  完成 IRP。

    功能驱动程序*IoCompletion*例程返回状态\_详细\_处理\_必需的如中所述[推迟 PnP IRP 处理直到较低的驱动程序完成](postponing-pnp-irp-processing-until-lower-drivers-finish.md)，因此功能驱动程序*DispatchPnP*例程必须调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)恢复 I/O 完成处理。

    如果函数驱动程序的启动操作已成功，驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功后，调用**IoCompleteRequest**优先级提高的 IO\_否\_递增，并返回状态\_成功从其*DispatchPnP*例程。

    功能驱动程序在其开始操作过程中遇到错误，如果驱动程序将 IRP，调用中设置错误状态**IoCompleteRequest**与 IO\_否\_递增，并从其返回错误*DispatchPnP*例程。

    如果较低的驱动程序失败 IRP (**IoCallDriver**返回了错误)，该函数将驱动程序调用**IoCompleteRequest**与 IO\_否\_增量，并返回**IoCallDriver**中的错误及其*DispatchPnP*例程。 功能驱动程序不会设置**Irp-&gt;IoStatus.Status**这种情况下由于已通过失败 IRP 的较低的驱动程序中设置了状态。

当功能驱动程序收到**IRP\_MN\_启动\_设备**请求，它应检查在结构**IrpSp-&gt;Parameters.StartDevice.AllocatedResources**并**IrpSp-&gt;Parameters.StartDevice.AllocatedResourcesTranslated**，分别描述的原始和已翻译的资源，即插即用的管理员分配给设备。 驱动程序应在设备扩展中保存一份每个资源的列表，帮助调试。

资源列表成对[ **CM\_资源\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff541994)结构，其中原始列表的每个元素对应于已翻译的列表的相同元素。 例如，如果**AllocatedResources.List**\[0\]描述的原始的 I/O 端口范围，然后**AllocatedResourcesTranslated.List**\[0\]介绍翻译后的相同的范围。 每个已翻译的资源包括物理地址和资源的类型。

如果驱动程序分配的已翻译的内存资源 (**CmResourceTypeMemory**)，必须调用[ **MmMapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff554618)物理地址映射到通过虚拟地址它可以访问设备注册。 驱动程序以平台无关的方式运行，它应该检查已翻译的每个返回的资源，并绘制其地图，如有必要。

功能驱动程序应执行以下操作以响应**IRP\_MN\_启动\_设备**以确保所有设备资源的访问权限：

1.  复制**IrpSp-&gt;Parameters.StartDevice.AllocatedResources**到设备扩展。

2.  复制**IrpSp-&gt;Parameters.StartDevice.AllocatedResourcesTranslated**到设备扩展。

3.  在循环中，检查的每个描述符元素**AllocatedResourcesTranslated**。 如果描述符资源类型为**CmResourceTypeMemory**，调用**MmMapIoSpace**，传递的物理地址和长度的已翻译的资源。

当驱动程序收到**IRP\_MN\_停止\_设备**， **IRP\_MN\_删除\_设备**，或**IRP\_MN\_惊讶\_删除**请求，它必须通过调用释放映射[ **MmUnmapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff556387)中类似的循环。 该驱动程序还应调用**MmUnmapIoSpace**如果必须故障**IRP\_MN\_启动\_设备**请求。

请参阅[映射到的虚拟地址的总线相对地址](mapping-bus-relative-addresses-to-virtual-addresses.md)有关详细信息。

 

 




