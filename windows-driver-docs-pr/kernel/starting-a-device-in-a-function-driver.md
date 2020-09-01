---
title: 在函数驱动程序中启动设备
description: 在函数驱动程序中启动设备
ms.assetid: 148a3128-9cb1-4a2c-a62e-45199476d968
keywords:
- 函数驱动程序 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9e387f81c654693b5dd8c45f8974244e0031b31
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189455"
---
# <a name="starting-a-device-in-a-function-driver"></a>在函数驱动程序中启动设备





函数驱动程序设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，在设备堆栈中传递 [**IRP \_ MN \_ start \_ 设备**](./irp-mn-start-device.md) 请求，并推迟其启动操作，直到所有较低版本的驱动程序都已完成 IRP。 有关使用内核事件的详细信息，请参阅 [推迟 PNP IRP 处理](postponing-pnp-irp-processing-until-lower-drivers-finish.md) ，并使用 *IOCOMPLETION* 例程延迟 IRP 处理。

如果在所有较低版本的驱动程序都完成了 IRP 后， [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程重新获得控制权，则函数驱动程序将执行其任务以启动设备。 函数驱动程序使用如下所示的过程启动设备：

1.  如果低级驱动程序失败，IRP ([**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 返回了错误) ，请不要继续处理 IRP。 执行任何必要的清理，并从 *DispatchPnP* 例程返回 (跳到此列表中的最后一步) 。

2.  如果较低的驱动程序成功处理了 IRP，则启动设备。

    启动设备的具体步骤因设备而异。 此类步骤可能包括映射 i/o 空间，初始化硬件注册，将设备设置为 D0 电源状态，并将中断连接到 [**IoConnectInterrupt**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)。 如果驱动程序在 [**IRP \_ MN \_ 停止 \_ 设备**](./irp-mn-stop-device.md) 请求后重新启动设备，则驱动程序的设备状态可能为 "正在还原"。

    必须打开设备，然后任何驱动程序才能访问设备。 有关详细信息，请参阅 [打开设备](powering-up-a-device.md) 。

    如果应启用设备进行唤醒，则其电源策略所有者通常 (功能驱动程序) 应在启动设备后、完成 **IRP \_ MN \_ 启动 \_ 设备** 请求后发送等待/唤醒 IRP。 有关详细信息，请参阅 [发送等待/唤醒 IRP](sending-a-wait-wake-irp.md)。

3.  在 IRP 中启动 irp-保存队列。

    清除 "驱动程序定义的保留 \_ 新 \_ 请求" 标志，并在 IRP 保留队列中启动 irp。 当首次启动设备时，以及在查询停止或停止 IRP 后重新启动设备时，驱动程序应执行此操作。 有关详细信息，请参阅 [在设备暂停时保留传入 irp](holding-incoming-irps-when-a-device-is-paused.md) 。

4.  \[\]可以通过调用[**IoSetDeviceInterfaceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)来启用设备的接口。

    启用驱动程序以前在其 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程中注册的接口（如果有） (或 INF 中，或由其他组件（如共同安装程序) ）。

    在 Windows 2000 和更高版本的 Windows 上，PnP 管理器不会发送设备接口到达通知，直到 **IRP \_ MN \_ 启动 \_ 设备** irp 完成，指出设备的所有驱动程序都已完成其启动操作。 PnP 管理器还会使在设备的所有驱动程序都完成启动 IRP 之前到达的任何创建请求失败。

5.  完成 IRP。

    函数驱动程序的 *IoCompletion* 例程返回了 \_ 所需的状态更多 \_ 处理 \_ ，如 [推迟 PnP IRP 处理直到较低的驱动程序完成](postponing-pnp-irp-processing-until-lower-drivers-finish.md)，从而使函数驱动程序的 *DispatchPnP* 例程必须调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 才能恢复 i/o 完成处理。

    如果函数驱动程序的启动操作成功，则驱动程序将 **Irp- &gt; IoStatus** 设置为状态 \_ "成功"，调用 **IoCompleteRequest** ，同时提升 IO \_ 无 \_ 增量，并 \_ 从其 *DispatchPnP* 例程返回状态 SUCCESS。

    如果函数驱动程序在其启动操作期间遇到错误，则驱动程序会在 IRP 中设置错误状态，使用 IO 无增量调用 **IoCompleteRequest** ， \_ \_ 并从其 *DispatchPnP* 例程返回错误。

    如果较低的驱动程序失败，IRP (**IoCallDriver**返回了错误) ，则函数驱动程序将使用 IO NO 增量调用**IoCompleteRequest** ， \_ \_ 并从其*DispatchPnP*例程返回**IoCallDriver**错误。 在这种情况下，函数驱动程序不会设置 ** &gt; IoStatus** ，因为状态已由 Irp 的低级驱动程序设置。

当函数驱动程序收到 **IRP \_ MN \_ START \_ 设备** 请求时，它应检查 **IrpSp- &gt; StartDevice. AllocatedResources** 和 IrpSp StartDevice 之间的结构 ** &gt; ，** 该结构分别描述了 PnP 管理器分配给设备的原始资源和已翻译资源。 驱动程序应将每个资源列表的副本作为调试辅助保存在设备扩展中。

资源列表是成对的 [**CM \_ 资源 \_ 列表**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list) 结构，其中原始列表的每个元素对应于已翻译列表的同一个元素。 例如，如果**AllocatedResources** \[ 0 \] 描述了原始 i/o 端口范围，则**AllocatedResourcesTranslated** \[ 0 \] 描述转换后的相同范围。 每个翻译的资源都包含物理地址和资源的类型。

如果 (**CmResourceTypeMemory**) 为驱动程序分配了已转换的内存资源，则它必须调用 [**MmMapIoSpace**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace) 将物理地址映射到可通过其访问设备寄存器的虚拟地址。 若要使驱动程序以独立于平台的方式运行，应检查每个返回的已转换资源，并根据需要对其进行映射。

函数驱动程序应执行以下操作来响应 **IRP \_ MN \_ 启动 \_ 设备** ，以确保对所有设备资源的访问：

1.  将 **IrpSp- &gt; StartDevice. AllocatedResources** 复制到设备扩展。

2.  将 **IrpSp- &gt; StartDevice. AllocatedResourcesTranslated** 复制到设备扩展。

3.  在循环中，检查 **AllocatedResourcesTranslated**中的每个描述符元素。 如果描述符资源类型为 **CmResourceTypeMemory**，则调用 **MmMapIoSpace**，同时传递已转换资源的物理地址和长度。

当驱动程序收到 **irp \_ MN \_ STOP \_ 设备**、 **irp \_ MN \_ REMOVE \_ 设备**或 **irp \_ MN \_ 意外 \_ 删除** 请求时，它必须通过在类似循环中调用 [**MmUnmapIoSpace**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace) 来释放映射。 如果该驱动程序必须失败**IRP \_ MN \_ 启动 \_ 设备**请求，则该驱动程序还应调用**MmUnmapIoSpace** 。

有关详细信息，请参阅 [将与总线相关的地址映射到虚拟地址](mapping-bus-relative-addresses-to-virtual-addresses.md) 。

 

