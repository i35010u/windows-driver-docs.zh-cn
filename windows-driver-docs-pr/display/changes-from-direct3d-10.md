---
title: 在 Direct3D 10 基础上的更改
description: 在 Direct3D 10 基础上的更改
keywords:
- Direct3D 版本 11 WDK Windows 7 显示，从 Direct3D 版本10进行的更改
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示，从 Direct3D 版本10进行的更改
- Direct3D 版本 10 WDK Windows 7 显示
- Direct3D 版本 10 WDK Windows 7 显示，Direct3D 版本11中的更改
- Direct3D 版本 10 WDK Windows Server 2008 R2 显示，Direct3D 版本11中的更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad25cc7e5b1fd45401cae7bc7674898206e7a739
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810337"
---
# <a name="changes-from-direct3d-10"></a>在 Direct3D 10 基础上的更改


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

以下各节介绍 Direct3D 11 在 Direct3D 10 中的更改。

### <a name="driver-callback-functions-to-kernel-mode-services"></a>用于 Kernel-Mode 服务的驱动程序回调函数

当运行时调用用户模式显示驱动程序的 [**CreateDevice (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数将驱动程序与内核句柄和内核函数签名隔离时，Direct3D 版本11运行时在 [**D3DDDI \_ DEVICECALLBACKS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)结构中提供的特定于设备的回调函数。 Direct3D 版本11运行时更改回调语义，因此，实现回调函数以支持自由线程模式的操作，而以前的 Direct3D 版本运行时不支持自由线程模式的操作。 自由线程模式操作的规则适用于驱动程序指示它支持 (D3D11DDICAPS FREETHREADED) 的自由线程模式 \_ ; 否则，将应用以前的严重限制规则。 有关驱动程序如何指示支持自由线程模式的信息，请参阅 [线程处理和命令列表](supporting-threading--command-lists--and-3-d-pipeline.md)。 对于 Direct3D 版本11仍然存在以下限制：

-   一次只能有一个线程可用于 HCONTEXT。 当前使用 HCONTEXT 的现有回调函数为 [**pfnPresentCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)、 [**pfnRenderCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)、 [*pfnEscapeCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_escapecb)、 [**pfnDestroyContextCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroycontextcb)、 [**pfnWaitForSynchronizationObjectCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobjectcb)和 [**pfnSignalSynchronizationObjectCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectcb)。 因此，如果有多个线程调用这些回调函数并使用相同的 HCONTEXT，则驱动程序必须同步对回调函数的调用。 满足此要求非常自然，因为这些回调函数可能只从操作直接上下文的线程调用。

-   只有在调用下列驱动程序函数时，驱动程序才必须调用以下回调函数：

    <span id="pfnAllocateCb"></span><span id="pfnallocatecb"></span><span id="PFNALLOCATECB"></span>[**pfnAllocateCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)  
    创建共享资源时，驱动程序必须在调用了驱动程序的 [**CreateResource (D3D11)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)函数的线程上调用 [*pfnAllocateCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb) 。 与设备的常规非共享分配完全免费。

    <span id="pfnPresentCb"></span><span id="pfnpresentcb"></span><span id="PFNPRESENTCB"></span>[**pfnPresentCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)  
    只有在调用驱动程序的 [**PresentDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数时，驱动程序才能调用 [**pfnPresentCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb) 。

    <span id="pfnSetDisplayModeCb"></span><span id="pfnsetdisplaymodecb"></span><span id="PFNSETDISPLAYMODECB"></span>[**pfnSetDisplayModeCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setdisplaymodecb)  
    只有在调用驱动程序的 [**SetDisplayModeDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_1_ddi_base_functions)函数时，驱动程序才能调用 [**pfnSetDisplayModeCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setdisplaymodecb) 。

    <span id="pfnRenderCb"></span><span id="pfnrendercb"></span><span id="PFNRENDERCB"></span>[**pfnRenderCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)  
    驱动程序必须在调用了驱动程序的 [**Flush (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_flush)函数的线程上调用 [*pfnRenderCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb) 。 由于 HCONTEXT 限制，此限制非常自然。

-   [*PfnDeallocateCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)回调函数值得特别指出，因为在驱动程序从其 [**DestroyResource (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource)函数返回到大多数资源类型之前，驱动程序不需要调用 *pfnDeallocateCb* 。 由于 DestroyResource (D3D10) 是一个自由线程的函数，因此驱动程序必须将对象的销毁延迟，直到驱动程序能够有效地确保不存在现有的即时上下文引用 (也就是说，驱动程序必须在 *pfnDeallocateCb*) 之前调用 [**pfnRenderCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb) 。 此限制甚至适用于共享资源或任何其他使用 HRESOURCE 来补充 HRESOURCE 使用 [**pfnAllocateCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)的回调函数。 但是，此限制不适用于主副本。 有关主要异常的详细信息，请参阅 [主要异常](#primary-exceptions)。 由于某些应用程序可能需要同步析构的外观，因此，驱动程序必须确保在调用其 [**Flush (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_flush)函数时，它会对任何以前已销毁的共享资源调用 *pfnDeallocateCb* 。 驱动程序还必须清除任何以前销毁的对象 (仅在调用其 Flush (D3D10) 函数的过程中不会将管道延迟) 的对象;驱动程序必须这样做，以确保运行时将 Flush () D3D10 作为一种官方机制来清理延迟销毁的对象，这些应用程序可能需要这种机制。 有关此机制的详细信息，请参阅 [延迟的析构和 Flush (D3D10) ](#deferred-destruction-and-flush-d3d10)。 驱动程序还必须确保在清理过程中在驱动程序的 [**DestroyDevice (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroydevice) 函数返回之前，会完全销毁销毁了其延迟的任何对象。

### <a name="deprecate-ability-to-allow-modification-of-free-threaded-ddis"></a>允许修改 Free-Threaded DDIs 的弃用功能

对于 Direct3D 版本11，显示设备的 API 级别概念和直接上下文仍将通过显示设备的旧版概念捆绑在 DDI 级别。 显示设备和直接上下文的这种绑定最大程度地提高了与先前版本的 DDIs (（如）的兼容性、 [Direct3D 版本 10 DDI](/windows-hardware/drivers/ddi/index)) ，并可通过多个版本的 DDIs 支持多个版本的 api 来减少驱动程序的变动。 但是，此显示设备和即时上下文捆绑会导致更混乱的 DDI，因为线程域并不是非常明确。 相反，若要了解多个接口的线程要求和这些接口中的函数，驱动程序开发人员必须参考文档。

Direct3D 版本 11 API 的主要功能是允许多个线程同时输入创建和销毁函数。 此类功能与允许驱动程序换出函数表指针以进行创建和销毁是不兼容的，作为在 [**D3D10DDI \_ DEVICEFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_devicefuncs) 和 [**D3D10 \_ 1DDI \_ DEVICEFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_1ddi_devicefuncs) 中指定的函数的 Direct3D 版本 10 DDI 语义。 因此，当驱动程序传递回用于创建 ([**CreateDevice (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)) 的函数指针后，当驱动程序在 Direct3D 版本 11 DDI 下运行并且驱动程序支持 DDI 线程处理时，驱动程序不应尝试更改行为。 此限制适用于以 *pfnCreate*、 *pfnOpen*、 *pfnDestroy*、 *pfnCalcPrivate* 和 *pfnCheck* 开头的所有设备函数。 所有剩余的设备函数都与直属上下文相关联。 由于单个线程一次会处理即时上下文，因此，它会被明确定义，以便继续允许驱动程序直接交换直接上下文函数表项。

### <a name="pfnrendercb-versus-pfnperformamortizedprocessingcb"></a>pfnRenderCb 与 pfnPerformAmortizedProcessingCb

Direct3D 版本 10 API 函数已挂钩 Direct3D 运行时的 [**pfnRenderCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb) 内核回调函数来执行摊销处理 (即，而不是针对每个 api 函数调用执行特定操作，驱动程序会针对每个如此多的 api 函数调用) 执行摊销操作。 此 API 通常使用此机会来剪裁高水位线，并刷新其延迟的对象析构队列。

若要允许核心回调函数为驱动程序提供尽可能自由的线程，当驱动程序支持 Direct3D 版本 11 DDI 时，Direct3D API 不再使用 [**pfnRenderCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb) 。 因此，支持 Direct3D 版本 11 DDI 的驱动程序必须在驱动程序在立即 (或类似频率) 上提交命令缓冲区后，从输入驱动程序 DDI 函数的同一线程中手动调用 [**pfnPerformAmortizedProcessingCb**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb) 内核回调函数。 由于该操作应剪裁高水位线，因此，在利用 [状态刷新 DDI 回调函数](/windows-hardware/drivers/ddi/index)在驱动程序生成命令缓冲区报头之前，执行此操作会有好处。

此外，驱动程序还应注意 API 摊销问题，并尝试平衡它使用 [**pfnPerformAmortizedProcessingCb**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb) 内核回调函数的频率。 在一个极端情况下，驱动程序可能会导致过度处理。 例如，如果驱动程序始终调用 *pfnPerformAmortizedProcessingCb* 两次 (后) ，可能是由于多引擎使用，因此，驱动程序只需调用 *pfnPerformAmortizedProcessingCb* 一次。 另一种极端情况是，如果驱动程序永远不会调用 *pfnPerformAmortizedProcessingCb*，则驱动程序可能不允许 Direct3D API 为整个帧执行任何工作，这可能是由于交互帧呈现设计引起的。 与此类似，驱动程序无需比自然更频繁地调用 *pfnPerformAmortizedProcessingCb* ，因为这是多余 (例如，如果驱动程序没有在1毫秒的时间内调用 *pfnPerformAmortizedProcessingCb* ，则必须是抽取 API) 的时间。 驱动程序只需确定哪些现有 [**pfnRenderCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb) 调用应伴随 **pfnPerformAmortizedProcessingCb** ，并自然符合操作的线程语义。

对于支持命令列表的驱动程序，这些驱动程序还必须从延迟的上下文中调用 [**pfnPerformAmortizedProcessingCb**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb) ，只要这些驱动程序的运行空间不足，就 () 的每个即时上下文刷新。 在此类操作期间，Direct3D 版本11运行时至少需要剪裁其高水印。 由于与 [**pfnRenderCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb) 相关的线程语义已为 Direct3D 版本11所宽松，因此必须解决并发性问题，以允许 Direct3D 版本11继续挂钩 **pfnRenderCb**，而无需进行限制。

### <a name="new-ddi-error-code"></a>新的 DDI 错误代码

创建 D3DDDIERR \_ APPLICATIONERROR 错误代码，以允许驱动程序参与验证，其中 Direct3D 版本 11 API 未执行此操作。 以前，如果驱动程序返回 E \_ INVALIDARG 错误代码，则会导致 API 引发异常。 调试层的存在会导致调试输出，并指示驱动程序返回了内部错误。 调试输出将向开发人员推荐驱动程序有 bug。 如果驱动程序返回 D3DDDIERR \_ APPLICATIONERROR，则调试层会确定该应用程序是否出错。

### <a name="retroactively-requiring-free-threaded-calcprivate-ddis"></a>以追溯方式要求自由线程 CalcPrivate DDI

Direct3D 版本11以追溯方式要求驱动程序函数以 *pfnCalcPrivate* on Direct3D 版本 10 DDI 函数开头以自由线程。 此追溯要求匹配 Direct3D 版本 11 DDI 的行为，始终要求 *pfnCalcPrivate \** 和 [**pfnCalcDeferredContextHandleSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcdeferredcontexthandlesize)函数为自由线程，即使驱动程序指示它不支持 DDI 线程处理也是如此。 有关此追溯要求的详细信息，请参阅 [以追溯方式需要 Free-Threaded CalcPrivate DDIs](retroactively-requiring-free-threaded-calcprivate-ddis.md)。

### <a name="deferred-destruction-and-flush-d3d10"></a>延迟的析构和刷新 D3D10

因为所有销毁函数现在都是可自由线程的，所以 Direct3D 运行时无法在析构期间刷新命令缓冲区。 因此，销毁函数必须将对象的实际销毁延迟，直到驱动程序可以确保操作即时上下文的线程不再依赖于该对象。 每个离散的直接上下文方法不能有效地使用同步来解决此销毁问题;因此，仅当驱动程序刷新命令缓冲区时，才应使用同步。 Direct3D 运行时还会使用此相同的设计，因为它必须处理类似的问题。

由于延迟的析构的 ratification，Direct3D 运行时是指那些不能容忍延迟析构解决方法的应用程序，而是使用显式机制。 因此，在调用其 [**Flush (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_flush) 函数时，驱动程序必须处理其延迟的队列 (即使命令缓冲区为空) ，才能确保这些机制实际工作。

需要某种形式的同步析构的那些应用程序必须使用下列模式之一，具体取决于析构的要求：

-   应用程序确保在该对象上的所有依赖项都已发布 (即，命令列表、视图、中间件，等等) ，应用程序使用以下模式：
    ```cpp
    Object::Release(); // Final release
    ImmediateContext::ClearState(); // Remove all ImmediateContext references as well.
    ImmediateContext::Flush(); // Destroy all objects as quickly as possible.
    ```

-   以下模式是 heavywight 的析构：
    ```cpp
    Object::Release(); // Final release
    ImmediateContext::ClearState(); // Remove all ImmediateContext references as well.
    ImmediateContext::Flush();
    ImmediateContext::End( EventQuery );
    while( S_FALSE == ImmediateContext::GetData( EventQuery ) ) ;
    ImmediateContext::Flush(); // Destroy all objects, completely.
    ```

### <a name="primary-exceptions"></a>主要异常

主副本是运行时在调用驱动程序的 [**CreateResource (D3D11)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource) 函数时创建的资源。 运行时通过将 [**D3D11DDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)结构的 **pPrimaryDesc** 成员设置为指向 [**DXGI \_ DDI \_ 主要 \_ DESC**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)结构的有效指针，来创建一个主副本。 对于以前从 Direct3D 10 到 Direct3D 11 的更改，主副本具有以下明显例外：

-   驱动程序的 [**CreateResource (D3D11)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource) 和 [**DestroyResource (D3D10 主副本的)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource) 函数不是自由线程的，它们共享直接的上下文线程域。 仍可与以 *pfnCreate* 和 *pfnDestroy* 开头的函数并存并发，其中包括 CreateResource (D3D11) 和 DestroyResource (D3D10) 。 但是，对于主副本， **CreateResource (D3D11)** 和 **DestroyResource (D3D10)** 中不能存在并发性。 例如，驱动程序可以检测到对其 CreateResource (D3D11) 或 DestroyResource (D3D10) 函数的调用是否适用于主要副本，从而确定它可以在函数调用期间安全使用或触摸即时上下文内存。

-   Direct3D 运行时无法延迟主要销毁，驱动程序必须在对驱动程序的 [**DestroyResource (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource)函数的调用中适当地调用 [*pfnDeallocateCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)函数。

 

