---
title: 保证向前推进 I/O 操作
description: 保证向前推进 I/O 操作
ms.assetid: e230eb3b-54ac-43b1-ac2b-8fa137cee43e
keywords:
- 保证前进进度 WDK KMDF
- 前进进度，保证 WDK KMDF
- 低内存情况 WDK KMDF
- I/o 队列 WDK KMDF，保证前进进度
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fe35f4ab690b814511a35bbd37f64d4aeac0412
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192011"
---
# <a name="guaranteeing-forward-progress-of-io-operations"></a>保证向前推进 I/O 操作


某些驱动程序，如系统的分页设备的存储驱动程序，必须至少执行其部分受支持的 i/o 操作，以避免丢失关键系统数据。 驱动程序故障的一个可能原因是内存不足的情况。 如果框架或驱动程序无法分配足够的内存来处理 i/o 请求，则一个或另一个可能必须通过使用错误状态值完成 i/o 请求，才能 [完成](completing-i-o-requests.md) i/o 请求。

在版本1.9 之前的 KMDF 版本中，如果不能为 i/o 请求包) i/o 管理器发送到驱动程序的 i/o 请求 (包分配框架请求对象，则该框架始终会失败。 为了使驱动程序能够在内存不足的情况下处理 i/o 请求，版本1.9 和更高版本的框架为 i/o 队列提供了一个可 *保证的前进进度* 功能。

此功能可让框架和驱动程序分别为请求对象集和请求相关的驱动程序上下文缓冲区预分配内存。 仅当系统内存量很低时，框架和驱动程序才使用此预分配内存。

### <a name="features-of-guaranteed-forward-progress"></a>保证前进进度的功能

通过使用框架的 i/o 队列的可保证前进进度，驱动程序可以：

-   要求框架在内存不足的情况下预先分配一组要用于特定 i/o 队列的请求对象。

-   提供一个回调函数，该函数预先分配在低内存情况下，驱动程序在从框架接收预分配请求对象时可以使用的特定于请求的资源。

-   当 *未* 检测到内存不足的情况时，提供另一个回调函数，该函数为 i/o 请求分配特定于驱动程序的资源。 如果此回调函数的分配由于内存不足而失败，则它可以指示框架是否应使用其预分配请求对象之一。

-   指定哪些 i/o 请求需要使用预先分配的请求对象。 选项包括对所有 Irp 使用预先分配的对象，仅在分页 i/o 操作正在进行时使用这些对象，或让每个 IRP 检查每个 IRP 来确定是否使用预先分配的对象。

如果驱动程序为其一个或多个 i/o 队列实现了保证前进进度，则驱动程序将能够更好地在内存不足的情况下成功 [处理 i/o 请求](processing-i-o-requests.md) 。 可以通过调用 [**WdfDeviceConfigureRequestDispatching**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)来实现设备的默认 i/o 队列和驱动程序配置的任何 i/o 队列的可保证前进进度。

只有当驱动程序和驱动程序的 [i/o 目标](using-i-o-targets.md) 都实现了保证前进进度时，框架的保证前进进度功能才适用于你的驱动程序。 换句话说，如果驱动程序实现了设备的保证前进进度，则设备的驱动程序堆栈中的所有较低级别的驱动程序还必须实施保证的前进进度。

### <a name="enabling-guaranteed-forward-progress-for-an-io-queue"></a>启用 i/o 队列的保证前进进度

若要为 i/o 队列启用有保证的前进进度，驱动程序将初始化 [**WDF \_ IO \_ queue \_ forward \_ 进度 \_ 策略**](/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy) 结构，然后调用 [**WdfIoQueueAssignForwardProgressPolicy**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy) 方法。 如果驱动程序调用 [**WdfDeviceConfigureRequestDispatching**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching) 来配置 i/o 队列，则必须在调用 **WdfIoQueueAssignForwardProgressPolicy**之前执行此操作。

当驱动程序调用 [**WdfIoQueueAssignForwardProgressPolicy**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)时，它可以指定以下三个事件回调函数，它们都是可选的：

<a href="" id="evtioallocateresourcesforreservedrequest"></a>[*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)  
驱动程序的 [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) 回调函数为框架为低内存情况保留的请求对象分配和存储特定于请求的资源。

每次创建保留请求对象时，框架都会调用此回调函数。 驱动程序应为一个 i/o 请求分配特定于请求的资源，通常使用保留的请求对象的 [上下文空间](framework-object-context-space.md)。

<a href="" id="evtioallocaterequestresources"></a>[*EvtIoAllocateRequestResources*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)  
驱动程序的 [*EvtIoAllocateRequestResources*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources) 回调函数将分配特定于请求的资源以便立即使用。 在框架收到 IRP 并为 IRP 创建请求对象之后立即调用此方法。

如果回调函数尝试分配资源失败，则回调函数将返回错误状态值。 然后，框架会删除新创建的请求对象并使用其保留的请求对象之一。 进而，驱动程序的 [请求处理程序](request-handlers.md) 使用其 [*EvtIoAllocateRequestResources*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources) 回调函数之前分配的特定于请求的资源。

<a href="" id="evtiowdmirpforforwardprogress"></a>[*EvtIoWdmIrpForForwardProgress*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress)  
驱动程序的 [*EvtIoWdmIrpForForwardProgress*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress) 回调函数检查 irp，并告诉 framework 是为 irp 使用保留的请求对象，还是通过使用错误状态值完成 i/o 请求来使 i/o 请求失败。

此框架仅在以下情况下调用此回调函数：框架无法创建新的请求对象，并通过在驱动程序的 [**WDF \_ IO \_ 队列 \_ 转发 \_ 进度 \_ 策略**](/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy) 结构中设置标志来表明 (，) 希望驱动程序在低内存情况下检查 irp。 换句话说，你的驱动程序可以评估每个 IRP，并决定是否在内存不足的情况下进行处理。

当你的驱动程序调用 [**WdfIoQueueAssignForwardProgressPolicy**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)时，它还指定你希望框架为低内存情况预先分配的保留请求对象的数量。 你可以选择适用于你的设备和驱动程序的请求对象的数量。 若要防止性能降低，驱动程序通常应指定一个数字，该数字应接近驱动程序和设备可以并行处理的 i/o 请求数。

但是，如果驱动程序对 [**WdfIoQueueAssignForwardProgressPolicy**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy) 及其 [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) 回调函数的调用预先分配过多的保留请求对象或过多的请求特定的资源内存，则您的驱动程序实际上可能会导致您尝试处理的低内存情况。 你应该测试驱动程序和设备的性能，并包括低内存模拟，以确定要选择的最佳数字。

在 [**WdfIoQueueAssignForwardProgressPolicy**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy) 返回之前，框架创建并保留驱动程序指定的请求对象数。 每次它保留一个请求对象时，框架会立即调用驱动程序的 [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) 回调函数，以便驱动程序可以分配并保存特定于请求的资源，以防框架实际使用保留的请求对象。

当某个驱动程序的 [请求处理程序](request-handlers.md) 收到 i/o 队列的 i/o 请求时，它可以调用 [**WdfRequestIsReserved**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestisreserved) 方法来确定该请求对象是否为框架为低内存情况预先分配的对象。 如果此方法返回 **TRUE**，则驱动程序应使用其 [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) 回调函数所保留的资源。

如果框架使用其保留的请求对象之一，则在驱动程序完成请求后，它会将对象返回到其保留对象集。 框架保存 request 对象，并保存驱动程序通过调用 [**WdfDeviceInitSetRequestAttributes**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes) 或 [**WdfObjectAllocateContext**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectallocatecontext)创建的任何上下文空间，以便在发生另一个低内存情况时重用。

### <a name="how-the-framework-and-driver-support-guaranteed-forward-progress"></a>框架和驱动程序支持如何保证前进进度

下面是驱动程序和框架为支持 i/o 队列保证前进进度而执行的步骤：

1.  驱动程序调用 [**WdfIoQueueAssignForwardProgressPolicy**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)。

    在响应中，框架分配并存储驱动程序指定的请求对象数。 如果驱动程序之前调用了 [**WdfDeviceInitSetRequestAttributes**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)，则每个分配都包含 **WdfDeviceInitSetRequestAttributes** 指定的上下文空间。

    此外，如果驱动程序提供了 [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) 回调函数，则在每次分配和存储请求对象时，框架都会调用回调函数。

2.  框架将接收 i/o 请求数据包 (IRP) i/o 管理器正在将其发送到该驱动程序。

    框架尝试为 IRP 分配请求对象。 如果 i/o 队列由为请求类型创建的驱动程序支持保证向前进度，则下一步将取决于分配是成功还是失败：

    -   请求对象分配成功。

        如果驱动程序提供了 [*EvtIoAllocateRequestResources*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources) 回调函数，则框架将调用它。 如果回调函数返回状态 \_ SUCCESS，则该框架会将请求添加到 i/o 队列。 如果回调函数返回错误状态值，则框架将删除刚刚创建的请求对象，并使用其预分配请求对象之一。 当驱动程序的请求处理程序收到 request 对象时，它将确定请求对象是否已预先分配，并因此是否应使用驱动程序的预分配资源。

        如果驱动程序未提供[*EvtIoAllocateRequestResources*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)回调函数，则该框架*会*将该请求添加到 i/o 队列，就好像驱动程序没有启用保证的前进进度一样。

    -   请求对象分配失败。

        框架接下来要执行的操作取决于为[**WDF \_ IO \_ 队列 \_ 转发 \_ 进度 \_ 策略**](/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy)结构的**ForwardProgressReservedPolicy**成员提供的值。 此成员通知框架何时使用保留的请求：总是，仅当 i/o 请求为分页 i/o 操作时，或仅当 [*EvtIoWdmIrpForForwardProgress*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress) 回调函数指示应使用保留的请求时。

    在所有情况下，驱动程序的请求处理程序都可以调用 [**WdfRequestIsReserved**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestisreserved) 来确定框架是否使用了保留的请求对象。 如果是这样，则驱动程序应使用 [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) 回调函数分配的请求资源。

### <a name="guaranteed-forward-progress-scenario"></a>保证前进进度情况

正在为可能包含系统页面文件的存储设备编写驱动程序。 对分页文件执行读操作和写入操作非常重要。

您决定为读写操作创建单独的 i/o 队列，并为这两个 i/o 队列启用有保证的前进进度。 您决定为所有其他请求类型创建第三个 i/o 队列，而无需保证前进进度。

你的驱动程序堆栈和设备能够并行处理四个写入操作，因此，在调用[**WdfIoQueueAssignForwardProgressPolicy**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)之前，将[**WDF \_ IO \_ 队列 \_ 前进 \_ 进度 \_ 策略**](/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy)结构的**TotalForwardProgressRequests**成员设置为4。

如果你的驱动程序的设备是寻呼设备，则你决定只有在驱动程序的设备为寻呼设备时**ForwardProgressReservedPolicy** ，才需要确保转发进度，因此，你的驱动程序将 WDF \_ IO \_ 队列 \_ 前进进度策略结构的 ForwardProgressReservedPolicy 成员设置 \_ \_ 为[**WdfIoForwardProgressReservedPolicyPagingIO**](/windows-hardware/drivers/ddi/wdfio/ne-wdfio-_wdf_io_forward_progress_reserved_policy)。

由于你的驱动程序需要每个读取请求和每个写入请求都有一个 framework memory 对象，因此你决定驱动程序应预先分配一些内存对象，以便在内存不足的情况下对 [**WdfIoTargetFormatRequestForRead**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread) 和 [**WdfIoTargetFormatRequestForWrite**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforwrite) 调用。

因此，驱动程序为读取队列提供了一个 [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) 回调函数，并为写入队列提供另一个。 此框架每次调用其中一个回调函数时，回调函数都会调用 [**WdfMemoryCreate**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate) ，并保存返回的对象句柄以减少内存不足的情况。 由于回调函数接收预分配请求对象的句柄，因此它可以将内存对象作为该请求对象的父级。  (DMA 设备的驱动程序还可能预先分配 [框架 DMA 对象](framework-dma-objects.md)。 ) 

读取和写入队列的 [请求处理程序](request-handlers.md) 必须确定每个接收的请求对象是否是框架为低内存情况保留的对象。 请求处理程序可以调用 [**WdfRequestIsReserved**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestisreserved)，也可以将请求对象句柄与 [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) 回调函数之前接收的句柄进行比较。

驱动程序还为读取队列提供一个 [*EvtIoAllocateRequestResources*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources) 回调函数，并为写入队列提供另一个。 框架在从 i/o 管理器接收读取或写入请求时调用其中一个回调函数，并成功创建请求对象。 其中每个回调函数都调用 [**WdfMemoryCreate**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate) 为请求分配内存对象。 如果分配失败，回调函数将返回一个错误状态值，通知框架发生了内存不足的情况。 框架（检测错误返回值）将删除刚刚创建的请求对象，并使用它的一个预分配对象。

此驱动程序不提供 [*EvtIoWdmIrpForForwardProgress*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress) 回调函数，因为它不需要在框架将其添加到 i/o 队列之前检查各个读取或写入 irp。

请记住，当驱动程序为设备实现了保证的转发进度时，设备的驱动程序堆栈中的所有较低级别的驱动程序还必须实施保证的前进进度。

 

