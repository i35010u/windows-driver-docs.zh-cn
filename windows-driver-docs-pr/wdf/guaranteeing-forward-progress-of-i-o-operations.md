---
title: 保证向前推进的 I/O 操作
description: 保证向前推进的 I/O 操作
ms.assetid: e230eb3b-54ac-43b1-ac2b-8fa137cee43e
keywords:
- 保证向前推进 WDK KMDF
- 取得进展，保证 WDK KMDF
- 内存不足的情况下 WDK KMDF
- I/O 队列 WDK KMDF，保证向前推进
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed4c7cb4dbb8dc4d12a848f6d0d6ddb4d416a642
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547075"
---
# <a name="guaranteeing-forward-progress-of-io-operations"></a>保证向前推进的 I/O 操作


某些驱动程序，例如存储驱动程序对于系统的分页设备，必须至少执行某些支持 I/O 操作而不会失败，若要避免丢失重要的系统数据。 驱动程序故障的一个潜在的原因是内存不足的情况。 如果框架或驱动程序无法分配足够的内存来处理 I/O 请求，一个或另一个可能失败的 I/O 请求[完成](completing-i-o-requests.md)它并显示错误状态的值。

在之前版本 1.9 KMDF 的版本，框架为总是失败的 I/O 请求如果它不能为 I/O 管理器已发送到驱动程序到 I/O 请求数据包 (IRP) 分配一个框架请求对象。 若要提供的驱动程序期间内存不足的情况下处理 I/O 请求的功能，版本 1.9 及更高版本的 framework 提供*保证向前推进*I/O 队列的功能。

此功能使框架和预分配的内存的驱动程序的请求对象和与请求相关的驱动程序的上下文缓冲区，分别设置。 框架和驱动程序使用此预先分配的内存的系统内存量较低时仅。

### <a name="features-of-guaranteed-forward-progress"></a>有保证的向前推进的功能

通过使用 I/O 队列框架的有保证的向前推进，驱动程序可以：

-   让 framework 预分配的请求对象期间内存不足的情况下使用与特定的 I/O 队列集。

-   提供预分配期间内存不足的情况下从框架接收预分配的请求对象时，可以使用该驱动程序的特定于请求的资源的回调函数。

-   提供的 I/O 请求分配特定于驱动程序的资源时内存不足的情况下具有另一个回调函数*不*已检测到。 如果此回调函数的分配失败由于内存不足的情况下，它可以指示是否在框架应使用的一个预分配的请求对象。

-   指定的 I/O 请求都需要使用预先分配的请求对象。 选项包括使用所有 Irp，分页 I/O 操作正在进行，或具有一个其他驱动程序的回调函数检查每个 IRP，以确定是否使用预分配的对象，才都使用这些预分配的对象。

如果驱动程序实现保证向前推进的一个或多个其 I/O 队列，该驱动程序将会更好能够成功[处理 I/O 请求](processing-i-o-requests.md)期间内存不足的情况。 可以实现有保证的向前推进，对于设备的默认 I/O 队列，并通过调用任何 I/O 队列用于配置您的驱动程序[ **WdfDeviceConfigureRequestDispatching**](https://msdn.microsoft.com/library/windows/hardware/ff545920)。

该框架的保证您的驱动程序和驱动程序的向前推进功能适用的驱动程序才[I/O 目标](using-i-o-targets.md)实现能保证向前推进。 换而言之，如果驱动程序实现有保证向前推进的设备，设备的驱动程序堆栈中的所有低级驱动程序还必须都实现有保证的向前推进。

### <a name="enabling-guaranteed-forward-progress-for-an-io-queue"></a>启用保证向前推进的 I/O 队列

若要启用的 I/O 队列保证向前推进，您的驱动程序初始化[ **WDF\_IO\_队列\_向前\_进度\_策略**](https://msdn.microsoft.com/library/windows/hardware/ff552364)结构，然后调用[ **WdfIoQueueAssignForwardProgressPolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff547395)方法。 如果该驱动程序调用[ **WdfDeviceConfigureRequestDispatching** ](https://msdn.microsoft.com/library/windows/hardware/ff545920)若要配置的 I/O 队列，它必须这样做之前，它调用**WdfIoQueueAssignForwardProgressPolicy**。

当驱动程序调用[ **WdfIoQueueAssignForwardProgressPolicy**](https://msdn.microsoft.com/library/windows/hardware/ff547395)，它可以指定以下三个事件回调函数，所有这些都是可选：

<a href="" id="evtioallocateresourcesforreservedrequest"></a>[*EvtIoAllocateResourcesForReservedRequest*](https://msdn.microsoft.com/library/windows/hardware/ff541751)  
驱动程序的[ *EvtIoAllocateResourcesForReservedRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff541751)回调函数分配，并存储特定于请求的资源的请求对象的框架保留的内存不足情况。

框架调用此回调函数每次时，它创建一个保留的请求对象。 该驱动程序应特定于请求的资源为分配一个 I/O 请求，通常通过使用保留的请求对象的[上下文空间](framework-object-context-space.md)。

<a href="" id="evtioallocaterequestresources"></a>[*EvtIoAllocateRequestResources*](https://msdn.microsoft.com/library/windows/hardware/ff541747)  
驱动程序的[ *EvtIoAllocateRequestResources* ](https://msdn.microsoft.com/library/windows/hardware/ff541747)回调函数会立即使用分配特定于请求的资源。 该框架已接收 IRP 和 IRP 为创建一个请求对象后，立即调用它。

如果回调函数尝试将资源分配失败，回调函数将返回一个错误状态的值。 然后，框架删除新创建的请求对象，并使用其中一个保留的请求对象。 接下来，驱动程序的[请求处理程序](request-handlers.md)使用的特定于请求的资源，其[ *EvtIoAllocateRequestResources* ](https://msdn.microsoft.com/library/windows/hardware/ff541747)以前分配的回调函数。

<a href="" id="evtiowdmirpforforwardprogress"></a>[*EvtIoWdmIrpForForwardProgress*](https://msdn.microsoft.com/library/windows/hardware/ff541808)  
驱动程序的[ *EvtIoWdmIrpForForwardProgress* ](https://msdn.microsoft.com/library/windows/hardware/ff541808)回调函数检查 IRP，并指示框架是否要保留的请求对象用于 IRP，或通过完成其与失败的 I/O 请求错误状态的值。

框架调用此回调函数，仅当该框架是无法创建新的请求对象，指示 (通过在驱动程序中设置一个标志[ **WDF\_IO\_队列\_转发\_进度\_策略**](https://msdn.microsoft.com/library/windows/hardware/ff552364)结构) 想要检查期间内存不足的情况下 Irp 的驱动程序。 换而言之，您的驱动程序可以评估每个 IRP，并确定它是否其中一个必须甚至期间内存不足的情况下处理。

当您的驱动程序调用[ **WdfIoQueueAssignForwardProgressPolicy**](https://msdn.microsoft.com/library/windows/hardware/ff547395)，它还指定你想要预先分配的内存不足的情况下的框架保留请求数对象。 可以选择适合你的设备和驱动程序的请求对象的数目。 若要防止性能降低的情况，您的驱动程序通常应指定一个近似于驱动程序和设备可以并行处理的 I/O 请求数的数字。

但是，如果您的驱动程序调用[ **WdfIoQueueAssignForwardProgressPolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff547395)并将其[ *EvtIoAllocateResourcesForReservedRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff541751)回调函数预分配保留的请求对象太多或过多特定于请求的资源的内存，尝试处理内存不足的情况下可以实际参与您的驱动程序。 应测试驱动程序和设备的性能，并包括内存不足的模拟，以确定最佳的编号，以选择。

之前[ **WdfIoQueueAssignForwardProgressPolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff547395)返回时，框架将创建和保留已指定驱动程序的请求对象的数目。 每次它保留了一个请求对象时，框架将立即调用的驱动程序[ *EvtIoAllocateResourcesForReservedRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff541751)回调函数，以便该驱动程序可以分配并保存特定于请求的资源，在用例 framework 实际上使用保留的请求对象。

当一个驱动程序的[请求处理程序](request-handlers.md)接收的 I/O 请求从 I/O 队列，它可以调用[ **WdfRequestIsReserved** ](https://msdn.microsoft.com/library/windows/hardware/ff549980)方法，以确定是否请求对象是一个框架预分配的内存不足的情况。 如果此方法返回 **，则返回 TRUE**，则驱动程序应使用的资源，其[ *EvtIoAllocateResourcesForReservedRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff541751)保留的回调函数。

如果框架使用的一个保留的请求对象，它返回的对象为其保留对象的集后，驱动程序完成请求。 该框架将请求对象和驱动程序通过调用创建的任何上下文空间保存[ **WdfDeviceInitSetRequestAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff546786)或[ **WdfObjectAllocateContext**](https://msdn.microsoft.com/library/windows/hardware/ff548723)，以供重复使用另一个内存不足的情况下发生。

### <a name="how-the-framework-and-driver-support-guaranteed-forward-progress"></a>框架和驱动程序如何支持保证向前推进

下面是为 I/O 队列支持保证向前推进的驱动程序和框架执行的步骤：

1.  驱动程序调用[ **WdfIoQueueAssignForwardProgressPolicy**](https://msdn.microsoft.com/library/windows/hardware/ff547395)。

    在响应中，框架会分配并将存储驱动程序指定的请求对象的数目。 如果该驱动程序之前调用[ **WdfDeviceInitSetRequestAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff546786)，每个分配包括上下文的空间， **WdfDeviceInitSetRequestAttributes**指定。

    此外，如果提供了驱动程序[ *EvtIoAllocateResourcesForReservedRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff541751)回调函数，该框架调用的回调函数每次它会分配并将存储请求对象。

2.  框架接收到的 I/O 管理器将发送到该驱动程序的 I/O 请求数据包 (IRP)。

    框架尝试为 IRP 分配请求对象。 如果为请求类型创建的驱动程序支持的 I/O 队列保证向前推进下, 一步取决于分配是否成功或失败时：

    -   请求对象分配成功。

        如果该驱动程序提供[ *EvtIoAllocateRequestResources* ](https://msdn.microsoft.com/library/windows/hardware/ff541747)回调函数，框架调用它。 如果回调函数将返回状态\_成功，则框架会将请求添加到 I/O 队列。 如果回调函数返回一个错误状态值，框架会删除它只需创建并使用其预先分配的请求对象之一的请求对象。 当驱动程序的请求处理程序收到的请求对象时，它确定是否请求对象是预分配，因此它是使用驱动程序的预分配资源。

        如果该驱动程序这样做*不*提供[ *EvtIoAllocateRequestResources* ](https://msdn.microsoft.com/library/windows/hardware/ff541747)回调函数，则框架会将请求添加到 I/O 队列，就像该驱动程序并没有启用有保证的向前推进。

    -   请求对象分配将失败。

        框架执行下一步取决于为该驱动程序提供的值**ForwardProgressReservedPolicy**的成员[ **WDF\_IO\_队列\_前滚\_进度\_策略**](https://msdn.microsoft.com/library/windows/hardware/ff552364)结构。 此成员告知框架何时使用保留的请求： 往常一样，仅当 I/O 请求是分页 I/O 操作，或仅当[ *EvtIoWdmIrpForForwardProgress* ](https://msdn.microsoft.com/library/windows/hardware/ff541808)指示回调函数应使用保留的请求。

    在所有情况下，驱动程序的请求处理程序可以调用[ **WdfRequestIsReserved** ](https://msdn.microsoft.com/library/windows/hardware/ff549980)确定框架是否具有使用保留的请求对象。 如果该驱动程序因此，应使用的请求资源，其[ *EvtIoAllocateResourcesForReservedRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff541751)分配回调函数。

### <a name="guaranteed-forward-progress-scenario"></a>保证向前推进方案

你正在编写可能包含系统的分页文件的存储设备的驱动程序。 它很重要，它读取从操作和写入到分页文件的操作会成功。

你决定创建单独的 I/O 队列进行读取和写入操作，而若要启用保证向前推进这两个这些 I/O 队列。 您决定创建其他所有请求类型的第三个 I/O 队列而不启用保证向前推进。

您的驱动程序堆栈和设备是否能够处理并行情况下，四个写入操作，因此您设置**TotalForwardProgressRequests**的成员[ **WDF\_IO\_队列\_向前\_进度\_策略**](https://msdn.microsoft.com/library/windows/hardware/ff552364)结构到 4 之前，调用[ **WdfIoQueueAssignForwardProgressPolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff547395).

您决定，保证向前推进才是必要的驱动程序的设备是否分页设备，因此您的驱动程序设置**ForwardProgressReservedPolicy** WDF 成员\_IO\_队列\_前滚\_进度\_策略结构[ **WdfIoForwardProgressReservedPolicyPagingIO**](https://msdn.microsoft.com/library/windows/hardware/ff552357)。

由于您的驱动程序要求的 framework 内存对象为每次读请求和每个写入请求，你可以决定您的驱动程序应预先分配要用于对其调用某些内存对象[ **WdfIoTargetFormatRequestForRead**](https://msdn.microsoft.com/library/windows/hardware/ff548612)并[ **WdfIoTargetFormatRequestForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff548620)在内存不足的情况下。

因此，该驱动程序提供了[ *EvtIoAllocateResourcesForReservedRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff541751)读取的队列，另一个用于写入队列的回调函数。 框架将调用以上任何一个回调函数，每次该回调函数将调用[ **WdfMemoryCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff548706) ，并将保存内存不足的情况下返回的对象句柄。 由于回调函数接收预分配的请求对象的句柄，因此它可以对请求对象的内存对象的父级。 (DMA 设备的驱动程序还可能会预分配[framework DMA 对象](framework-dma-objects.md)。)

[请求处理程序](request-handlers.md)的读取和写入队列必须确定每个收到的请求对象是一个框架内存不足的情况下为保留的。 请求处理程序可以调用[ **WdfRequestIsReserved**](https://msdn.microsoft.com/library/windows/hardware/ff549980)，或者它可以将与所请求对象句柄进行比较的[ *EvtIoAllocateResourcesForReservedRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff541751)先前收到的回调函数。

该驱动程序还提供了[ *EvtIoAllocateRequestResources* ](https://msdn.microsoft.com/library/windows/hardware/ff541747)读取的队列，另一个用于写入队列的回调函数。 当它收到来自 I/O 管理器的读取或写入请求并已成功创建一个请求对象时，框架将调用这些回调函数之一。 每个回调函数调用[ **WdfMemoryCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff548706)为请求分配的内存对象。 如果分配失败，回调函数将返回错误状态值以通知框架只是发生内存不足的情况。 Framework 中，检测错误返回值，删除它只需创建并使用其预先分配的对象之一的请求对象。

此驱动程序不提供[ *EvtIoWdmIrpForForwardProgress* ](https://msdn.microsoft.com/library/windows/hardware/ff541808)回调函数，因为它不需要检查各个读取或写入 Irp，框架将它们添加到的 I/O 队列之前。

请记住，当驱动程序实现有保证向前推进的设备，设备的驱动程序堆栈中的所有低级驱动程序还必须都实现有保证的向前推进。

 

 





