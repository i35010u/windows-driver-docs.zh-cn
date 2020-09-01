---
title: DMA 例程版本 3 的基本调用模式
description: 若要执行 dma 传输并使用 DMA 操作接口版本3中的例程，你的驱动程序应按照以下列表中所述的步骤进行操作。
ms.assetid: 5D73120F-79F5-4C9A-8AE5-25D5CF9B06F5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5cfb219785256ccfdb7b1ad2d8581d9753c918e6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189549"
---
# <a name="basic-calling-pattern-for-version-3-dma-routines"></a>DMA 例程版本 3 的基本调用模式


若要执行 dma 传输并使用 DMA 操作接口版本3中的例程，你的驱动程序应按照以下列表中所述的步骤进行操作。 这些步骤通常适用于从属设备和总线主机设备。 此接口的版本3从 Windows 8 开始可用。 有关此接口中例程的详细信息，请参阅 [**DMA \_ 操作**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations)。

## <a name="step-1-obtain-a-dma-adapter-object"></a>步骤1：获取 DMA 适配器对象


为实现 DMA 传输准备，驱动程序将调用 [**IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter) 例程以获取 dma 适配器对象。 DMA 适配器对象是一个软件对象，表示系统 DMA 控制器上的总线主控设备或请求线路。 此对象包含用于将数据传入或传出设备的总线的 DMA 操作接口。 此外，此对象会将驱动程序的访问权限同步到执行传输所需的共享资源。 有关详细信息，请参阅 [适配器对象简介](introduction-to-adapter-objects.md)。

## <a name="step-2-obtain-a-description-of-the-required-dma-resources"></a>步骤2：获取所需 DMA 资源的描述


驱动程序调用 [**GetDmaTransferInfo**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_dma_transfer_info) 例程来获取执行传输所需的 DMA 资源的说明。

此调用的输入参数描述用于传输的内存缓冲区，以及传输 (读取或写入) 的方向。

从此调用获得的资源要求包括映射寄存器的数目以及为传输描述数据缓冲区所需的分散/收集列表的大小。 在对 [**AllocateAdapterChannelEx**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel_ex) 例程的后续调用中 (参见 [步骤 3](#step-3-request-the-required-dma-resources)) ，驱动程序将映射寄存器计数作为输入参数提供。

## <a name="step-3-request-the-required-dma-resources"></a>步骤3：请求所需的 DMA 资源


驱动程序调用 [**AllocateAdapterChannelEx**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel_ex) 例程来分配要分配给 DMA 适配器对象的资源。 这些资源包括 DMA 通道和映射寄存器。

**AllocateAdapterChannelEx**调用可以是异步的或同步的。

如果 \_ \_ 未设置 DMA 同步回调标志，则调用是异步的。 在这种情况下， *ExecutionRoutine* 参数指向调用方提供的执行例程，该例程在请求的资源可用时调用。 如果成功，则异步 **AllocateAdapterChannelEx** 调用返回状态 \_ 成功，而不等待执行例程运行。

如果设置了 DMA \_ 同步 \_ 回调标志，则 **AllocateAdapterChannelEx** 调用是同步的。 在这种情况下，调用中的 *ExecutionRoutine* 参数是可选的， **AllocateAdapterChannelEx** 的行为如下所示：

-   如果 *ExecutionRoutine* 为非 NULL，并且可以立即分配 DMA 资源， **AllocateAdapterChannelEx** 将在调用线程的上下文中调用执行例程。 执行例程运行完毕后， **AllocateAdapterChannelEx** 将返回状态 " \_ 成功"。 如果资源不可用，则 **AllocateAdapterChannelEx** 将失败，并返回错误状态代码状态 \_ " \_ 资源不足"。

-   如果 *ExecutionRoutine* 为 NULL，并且 **AllocateAdapterChannelEx** 可以立即分配 DMA 资源， **AllocateAdapterChannelEx** 将返回状态 \_ SUCCESS。 如果所有资源都无法立即使用，则调用失败，并显示错误状态代码状态 " \_ 资源不足" \_ 。

对于返回状态成功的同步调用 \_ ，如果**AllocateAdapterChannelEx**的*MAPREGISTERBASE*参数为非 NULL，则**AllocateAdapterChannelEx**会将分配的映射寄存器的基址写入*MapRegisterBase*参数指向的地址。 如果 *ExecutionRoutine* 为 null，则 *MapRegisterBase* 必须为非 null。 如果*ExecutionRoutine*为非 NULL，则**AllocateAdapterChannelEx**的*MapRegisterBase*参数是可选的，并且执行例程接收映射寄存器基址作为输入参数。

对于异步 **AllocateAdapterChannelEx** 调用， *ExecutionRoutine* 必须为非 NULL，并且执行例程接收映射寄存器基址作为输入参数。

在对 [**MapTransferEx**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer_ex) 例程的后续调用中 (参阅 [步骤 5](#step-5-initialize-the-dma-resources-and-start-the-dma-transfer)) ，驱动程序将映射寄存器基址作为输入参数提供。

如果 *ExecutionRoutine* 不为 NULL，则执行例程将返回状态值以指示已分配资源的处置。 对于系统 DMA 传输，此返回值必须是 **KeepObject**。 此值通知操作系统适配器对象 (，其所有已分配资源) 正在使用中，不应将其释放。 如果未提供执行例程，则驱动程序必须改为调用 [**FreeAdapterObject**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_object) 例程，并提供 **KeepObject** 作为 *AllocationOption* 参数。

## <a name="step-4-if-necessary-cancel-the-pending-resource-request"></a>步骤4：如有必要，取消挂起的资源请求


在 **AllocateAdapterChannelEx** 调用将 dma 适配器排队以等待 dma 资源后，该驱动程序就可以根据需要调用 [**CancelAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pcancel_adapter_channel) 例程来取消挂起的资源请求。

如果 **CancelAdapterChannel** 返回 TRUE，则表示已成功取消资源请求。 如果在 **AllocateAdapterChannelEx** 调用中提供了执行例程，则此例程不会运行。

如果 **CancelAdapterChannel** 返回 FALSE，则无法取消资源请求，因为该请求已被授予。 如果在 **AllocateAdapterChannelEx** 调用中提供了执行例程，将调用此例程。

## <a name="step-5-initialize-the-dma-resources-and-start-the-dma-transfer"></a>步骤5：初始化 DMA 资源并启动 DMA 传输


驱动程序调用 [**MapTransferEx**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer_ex) 来初始化 dma 资源并启动 dma 传输。 此调用可能会在调用 **AllocateAdapterChannelEx**的同一驱动程序线程中发生，也可能出现在驱动程序提供给 **AllocateAdapterChannelEx**的执行例程中。 如果需要多个**MapTransferEx**调用来传输整个 DMA 数据缓冲区，则在上一**MapTransferEx**调用的完成例程中可能会发生更多的**MapTransferEx**调用。

**MapTransferEx** 支持将链式 MDLs 作为输入参数。 每个 MDL 都说明 DMA 缓冲区中的一个区域，该区域在虚拟内存中是连续的。 当 **MapTransferEx** 生成散点/集合列表时，它会自动处理从一个几乎不需要驱动程序干预转换到下一个虚拟的缓冲区区域的转换。 有关详细信息，请参阅 [使用 MapTransferEx 例程](using-the-maptransferex-routine.md)。

对于系统 DMA 传输，可以将指向 DMA 完成例程的指针传递到可选*DmaCompletionRoutine*参数中的**MapTransferEx** 。 此例程计划在调度级别运行，以响应系统 DMA 控制器中指示 DMA 传输已完成的中断。

如果**MapTransferEx**无法映射整个请求的传输大小，则会将 \* *length*输出参数设置为已映射的长度，并返回状态 \_ SUCCESS。

## <a name="step-6-if-necessary-perform-hardware-specific-operations"></a>步骤6：如有必要，执行特定于硬件的操作


**MapTransferEx** 返回状态 \_ SUCCESS 以指示已成功启动 DMA 传输。 在某些平台上，驱动程序可能需要在 **MapTransferEx** 调用之外执行一些其他操作来启动传输，但这种类型的延迟启动不需要用于所有平台。 驱动程序不得依赖于这些延迟来决定使用和释放已分配的资源。

DMA 操作接口中的例程为 DMA 传输维护缓存一致性，这种方式对于使用这些例程的驱动程序是透明的。 在不在硬件中强制进行缓存一致性的平台上， **MapTransferEx** 确保在写入 (内存到设备) 传输之前刷新处理器数据缓存。 若要读取 (设备到内存的) 传输，则在调用[**FlushAdapterBuffersEx**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers_ex)例程期间缓存会失效， (参阅每个**MapTransferEx**调用后面的[步骤 8](#step-8-flush-any-data-that-remains-in-the-cache)) 。

## <a name="step-7-receive-notification-when-the-dma-transfer-finishes"></a>步骤7：在 DMA 传输完成时接收通知


DMA 传输完成后，将通过以下两种方式之一通知驱动程序：

-   总线-主设备的设备驱动程序中断
-   为使用系统 DMA 控制器的从属设备执行驱动程序提供的完成例程

对于系统 DMA 传输，驱动程序可以将完成例程提供给 **MapTransferEx** 作为输入参数。
## <a name="step-8-flush-any-data-that-remains-in-the-cache"></a>步骤8：刷新缓存中保留的所有数据


DMA 传输完成后，驱动程序必须调用 [**FlushAdapterBuffersEx**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers_ex) 例程来刷新缓存中保留的所有数据。 驱动程序必须在每次**MapTransferEx**调用后调用**FlushAdapterBuffersEx** 。

如果 **MapTransferEx** 调用仅映射 DMA 数据缓冲区的一部分，则驱动程序必须再次调用 **MapTransferEx** 来映射剩余数据。 复杂传输可能需要多个 **MapTransferEx** 调用。 对于每个其他 **MapTransferEx** 调用，重复步骤5到步骤8。

## <a name="step-9-free-the-dma-channel-and-map-registers"></a>步骤9：释放 DMA 通道并映射寄存器


成功映射整个 DMA 数据缓冲区并完成最后一次传输后，驱动程序必须调用 [**FreeAdapterChannel**](./mmcreatemdl.md) 例程来释放 DMA 通道和任何以前分配的映射寄存器。

## <a name="step-10-release-the-dma-adapter-object"></a>步骤10：发布 DMA 适配器对象


完成所有 DMA 传输并释放以前分配的映射寄存器后，驱动程序将调用 [**PutDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_dma_adapter) 例程来释放适配器对象。

 

