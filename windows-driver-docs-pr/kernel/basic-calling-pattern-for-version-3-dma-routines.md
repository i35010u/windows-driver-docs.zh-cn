---
title: DMA 例程版本 3 的基本调用模式
description: 若要执行使用 DMA 操作接口的版本 3 中的例程的 DMA 传输，您的驱动程序应遵循以下列表中所述的步骤。
ms.assetid: 5D73120F-79F5-4C9A-8AE5-25D5CF9B06F5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4388b99b25791bd7440c3e611f65d375f4de6f29
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326047"
---
# <a name="basic-calling-pattern-for-version-3-dma-routines"></a>DMA 例程版本 3 的基本调用模式


若要执行使用 DMA 操作接口的版本 3 中的例程的 DMA 传输，您的驱动程序应遵循以下列表中所述的步骤。 这些步骤是通用的从属设备和总线母版设备。 从 Windows 8 开始提供此接口的版本 3。 有关此接口中的例程的详细信息，请参阅[ **DMA\_OPERATIONS**](https://msdn.microsoft.com/library/windows/hardware/ff544071)。

## <a name="step-1-obtain-a-dma-adapter-object"></a>第 1 步：获取 DMA 适配器对象


在为了准备 DMA 传输，该驱动程序调用[ **IoGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff549220)例程，以获取 DMA 适配器对象。 DMA 适配器对象是表示一总线主控台设备或请求行系统 DMA 控制器上的软件对象。 此对象包含用于将数据传入或从设备的总线的 DMA 操作接口。 此外，此对象同步到执行传输所需的共享资源的驱动程序的访问。 有关详细信息，请参阅[适配器对象简介](introduction-to-adapter-objects.md)。

## <a name="step-2-obtain-a-description-of-the-required-dma-resources"></a>步骤 2：获取所需的 DMA 资源的说明


驱动程序调用[ **GetDmaTransferInfo** ](https://msdn.microsoft.com/library/windows/hardware/hh451125)例程，以获取它需要对其执行传输的 DMA 资源的说明。

此调用的输入的参数描述要使用的传输和传输的方向 （读取或写入） 的内存缓冲区。

此调用中获取的资源要求包括的映射寄存器的数量和描述适用于传输的数据缓冲区所需的分散/聚拢列表的大小。 在后续调用中[ **AllocateAdapterChannelEx** ](https://msdn.microsoft.com/library/windows/hardware/hh406340)例程 (请参阅[步骤 3](#step-3-request-the-required-dma-resources))，驱动程序提供的映射注册计数作为输入参数。

## <a name="step-3-request-the-required-dma-resources"></a>步骤 3:请求所需的 DMA 资源


驱动程序调用[ **AllocateAdapterChannelEx** ](https://msdn.microsoft.com/library/windows/hardware/hh406340)例程来分配资源要分配给 DMA 适配器对象。 这些资源包括 DMA 通道，并将映射寄存器。

**AllocateAdapterChannelEx**调用可以是异步或同步。

如果 DMA\_同步\_回调标志未设置，调用是异步的。 在这种情况下， *ExecutionRoutine*参数指向请求的资源可用时调用的调用方提供执行例程。 如果成功，异步**AllocateAdapterChannelEx**调用将返回状态\_而无需等待执行例程运行成功。

如果 DMA\_同步\_设置回调标志，则**AllocateAdapterChannelEx**调用是同步的。 在这种情况下， *ExecutionRoutine*调用中的参数是可选的并且**AllocateAdapterChannelEx**行为，如下所示：

-   如果*ExecutionRoutine*为非 NULL 和 DMA 资源可立即分配**AllocateAdapterChannelEx**调用线程的上下文中调用执行例程。 执行例程完成运行后, **AllocateAdapterChannelEx**将返回状态\_成功。 如果资源不立即可用**AllocateAdapterChannelEx**失败并返回错误状态代码状态\_不足\_资源。

-   如果*ExecutionRoutine*为 NULL，并且**AllocateAdapterChannelEx**立即分配 DMA 资源**AllocateAdapterChannelEx**返回状态\_成功。 如果不立即可用的所有资源，调用将失败，错误状态代码状态\_不足\_资源。

返回状态的同步调用\_成功后，如果*MapRegisterBase*参数**AllocateAdapterChannelEx**为非 NULL **AllocateAdapterChannelEx**指向的写入到的地址注册分配的映射的基址*MapRegisterBase*参数。 如果*ExecutionRoutine*为 NULL， *MapRegisterBase*必须为非 NULL。 如果*ExecutionRoutine*为非 NULL *MapRegisterBase*参数**AllocateAdapterChannelEx**是可选的并执行例程接收映射寄存器作为输入参数的基址。

有关异步**AllocateAdapterChannelEx**调用， *ExecutionRoutine*必须为非 NULL，并执行例程接收作为输入参数的映射注册基址。

在后续调用[ **MapTransferEx** ](https://msdn.microsoft.com/library/windows/hardware/hh406521)例程 (请参阅[第 5 步](#step-5-initialize-the-dma-resources-and-start-the-dma-transfer))，驱动程序提供作为输入参数的映射注册基址。

如果*ExecutionRoutine*为非 NULL 执行例程将返回一个指示已分配的资源的处置状态值。 对于系统 DMA 传输，此返回值必须是**KeepObject**。 此值通知操作系统该适配器对象 （和所有其已分配的资源） 正在使用中，不会释放。 如果未不提供任何执行例程，则该驱动程序必须改为调用[ **FreeAdapterObject** ](https://msdn.microsoft.com/library/windows/hardware/hh451107)例程和提供**KeepObject**作为*AllocationOption*参数。

## <a name="step-4-if-necessary-cancel-the-pending-resource-request"></a>步骤 4：如有必要，取消挂起的资源请求


之后**AllocateAdapterChannelEx**调用的队列可以使用 DMA 适配器来等待 DMA 资源、 驱动程序，如有必要，请调用[ **CancelAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/hh406374)到例程取消挂起的资源请求。

如果**CancelAdapterChannel**返回 TRUE，则已成功取消资源请求。 如果在提供了执行例程**AllocateAdapterChannelEx**调用时，此例程不会运行。

如果**CancelAdapterChannel**返回 FALSE，因为它已被授予无法取消资源请求。 如果在提供了执行例程**AllocateAdapterChannelEx**调用时，将调用此例程。

## <a name="step-5-initialize-the-dma-resources-and-start-the-dma-transfer"></a>步骤 5：初始化 DMA 资源并启动 DMA 传输


驱动程序调用[ **MapTransferEx** ](https://msdn.microsoft.com/library/windows/hardware/hh406521)初始化 DMA 资源以及用于启动 DMA 传输。 此调用中调用的相同驱动程序线程可能会发生**AllocateAdapterChannelEx**，或该驱动程序提供给执行例程中可能会发生**AllocateAdapterChannelEx**。 如果多个**MapTransferEx**传输整个 DMA 数据缓冲区，所需的调用更高版本**MapTransferEx**早期调用在完成例程中可能出现**MapTransferEx**调用。

**MapTransferEx**支持链接 MDLs 作为输入参数。 每个 MDL 介绍的是虚拟内存中连续的 DMA 缓冲区的区域。 当**MapTransferEx**生成散播-聚集列表中，它将自动处理从一个几乎连续缓冲区区域转换到而无需驱动程序干预下一步。 有关详细信息，请参阅[使用 MapTransferEx 例程](using-the-maptransferex-routine.md)。

对于系统 DMA 传输，指向 DMA 完成例程的指针可以传递给**MapTransferEx**可选*DmaCompletionRoutine*参数。 此例程计划要在调度运行以响应来自表明 DMA 传输已完成的系统 DMA 控制器中断的级别。

如果**MapTransferEx**是无法将映射整个请求的传输大小，它将设置\**长度*输出的映射，长度参数并返回状态\_成功。

## <a name="step-6-if-necessary-perform-hardware-specific-operations"></a>步骤 6：如有必要，执行特定于硬件的操作


**MapTransferEx**将返回状态\_成功指示 DMA 传输已成功启动。 在某些平台上驱动程序可能需要执行一些其他操作，之外**MapTransferEx**调用，以启动传输，但这种延迟的启动不是必需的所有平台。 驱动程序必须不依赖于此类延迟了有关使用和释放已分配的资源的决策。

DMA 操作接口中的例程的 DMA 传输对使用这些例程的驱动程序是透明的方式维护缓存一致性。 平台上，不会强制使用硬件、 缓存协调性**MapTransferEx**可确保，将处理器数据缓存刷新之前写入 （内存设备） 传输。 读取 （设备内存） 传输的缓存失效在调用[ **FlushAdapterBuffersEx** ](https://msdn.microsoft.com/library/windows/hardware/hh451102)例程 (请参阅[步骤 8](#step-8-flush-any-data-that-remains-in-the-cache)) 后面的每个**MapTransferEx**调用。

## <a name="step-7-receive-notification-when-the-dma-transfer-finishes"></a>步骤 7：DMA 传输完成后收到通知


DMA 传输完成后，该驱动程序通知这两种方式之一：

-   到的设备驱动程序，总线主设备中断
-   使用系统 DMA 控制器的从属设备的驱动程序提供完成例程的执行

对于系统 DMA 传输，驱动程序可以提供到完成例程**MapTransferEx**作为输入参数。
## <a name="step-8-flush-any-data-that-remains-in-the-cache"></a>步骤 8：将保留在缓存中任何数据刷新


DMA 传输完成后，该驱动程序必须调用[ **FlushAdapterBuffersEx** ](https://msdn.microsoft.com/library/windows/hardware/hh451102)例程将保留在缓存中任何数据刷新。 该驱动程序必须调用**FlushAdapterBuffersEx**后每个**MapTransferEx**调用。

如果**MapTransferEx**调用映射仅 DMA 数据缓冲区的一部分，该驱动程序必须调用**MapTransferEx**再次将剩余的数据映射。 复杂传输可能需要若干**MapTransferEx**调用。 每个额外**MapTransferEx**调用，请重复步骤 5 至 8。

## <a name="step-9-free-the-dma-channel-and-map-registers"></a>步骤 9：免费 DMA 通道和映射寄存器


已成功映射整个 DMA 数据缓冲区并在最后一个传输完成后，该驱动程序必须调用[ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff549101)例程来释放 DMA 通道和任何以前分配的映射注册。

## <a name="step-10-release-the-dma-adapter-object"></a>步骤 10：释放 DMA 适配器对象


所有 DMA 传输都已完成并释放任何以前分配的映射寄存器后，该驱动程序会调用[ **PutDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff559965)例程来释放适配器对象。

 

 




