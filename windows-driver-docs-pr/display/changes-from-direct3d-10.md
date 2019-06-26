---
title: 在 Direct3D 10 基础上的更改
description: 在 Direct3D 10 基础上的更改
ms.assetid: 014a5e44-f8c4-45c0-96e8-d82f37b8b28d
keywords:
- Direct3D 11 版 WDK Windows 7 显示，更改从 Direct3D 版本 10
- Direct3D 11 版 WDK Windows Server 2008 R2 显示，更改从 Direct3D 版本 10
- Direct3D 版本 10 WDK Windows 7 显示
- Direct3D 版本 10 WDK Windows 7 显示，Direct3D 版本 11 中的更改
- Direct3D 版本 10 WDK Windows Server 2008 R2 显示，Direct3D 版本 11 中的更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6ce864c55b0f0267f3e8cdacb1889428098d943
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384593"
---
# <a name="changes-from-direct3d-10"></a>在 Direct3D 10 基础上的更改


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

以下部分介绍如何 Direct3D 11 已从 Direct3D 10。

### <a name="driver-callback-functions-to-kernel-mode-services"></a>驱动程序到内核模式服务的回调函数

在 Direct3D 11 版运行时提供的特定于设备的回调函数[ **D3DDDI\_DEVICECALLBACKS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)时运行时调用用户模式显示驱动程序的结构[ **CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数将从内核句柄和内核函数签名的驱动程序隔离。 Direct3D 版本 11 运行时更改回调语义和回调函数来支持自由线程操作模式，实现，因此，而以前的 Direct3D 版本运行时不支持自由线程模式操作。 自由线程模式下操作的规则应用后，驱动程序表明它支持自由线程模式 (D3D11DDICAPS\_FREETHREADED); 否则为以前的严格限制的规则适用。 有关驱动程序如何指示支持自由线程模式的信息，请参阅[线程处理和命令将列出](supporting-threading--command-lists--and-3-d-pipeline.md)。 有关 Direct3D 版本 11 仍存在以下限制：

-   只有一个线程可以对 HCONTEXT 操作一次。 是现有的回叫函数，当前使用 HCONTEXT [ **pfnPresentCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)， [ **pfnRenderCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)， [ *pfnEscapeCb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_escapecb)， [ **pfnDestroyContextCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroycontextcb)， [ **pfnWaitForSynchronizationObjectCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobjectcb)，并[ **pfnSignalSynchronizationObjectCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectcb)。 因此，如果多个线程调用这些回调函数，并使用同一个 HCONTEXT，驱动程序必须同步回调函数的调用。 满足此要求是很自然，因为可能只能从操作即时上下文的线程调用这些回调函数。

-   驱动程序必须使用相同的线程调用这些驱动程序函数仅在对以下驱动程序函数的调用期间调用以下回调函数：

    <span id="pfnAllocateCb"></span><span id="pfnallocatecb"></span><span id="PFNALLOCATECB"></span>[**pfnAllocateCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)  
    该驱动程序必须调用[ *pfnAllocateCb* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)称为驱动程序的线程上[ **CreateResource(D3D11)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)时共享的功能创建资源。 与设备的常规非共享分配是完全的自由线程。

    <span id="pfnPresentCb"></span><span id="pfnpresentcb"></span><span id="PFNPRESENTCB"></span>[**pfnPresentCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)  
    该驱动程序必须调用[ **pfnPresentCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)仅在对驱动程序的调用期间[ **PresentDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数。

    <span id="pfnSetDisplayModeCb"></span><span id="pfnsetdisplaymodecb"></span><span id="PFNSETDISPLAYMODECB"></span>[**pfnSetDisplayModeCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setdisplaymodecb)  
    该驱动程序必须调用[ **pfnSetDisplayModeCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setdisplaymodecb)仅在对驱动程序的调用期间[ **SetDisplayModeDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_1_ddi_base_functions)函数。

    <span id="pfnRenderCb"></span><span id="pfnrendercb"></span><span id="PFNRENDERCB"></span>[**pfnRenderCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)  
    该驱动程序必须调用[ *pfnRenderCb* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)称为驱动程序的线程上[ **Flush(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_flush)函数。 此限制是很自然，因为存在 HCONTEXT 限制。

-   [ *PfnDeallocateCb* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)回调函数需特别注意，因为该驱动程序不需要调用*pfnDeallocateCb*驱动程序将返回从之前其[ **DestroyResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource)对于大多数资源类型的函数。 由于 DestroyResource(D3D10) 是自由线程的函数，该驱动程序必须操作延迟对象的析构驱动程序可以有效地确保任何现有的即时上下文引用保持 (也就是说，该驱动程序必须调用[ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)之前*pfnDeallocateCb*)。 此限制适用甚至对共享资源或任何其他使用 HRESOURCE 来补充使用 HRESOURCE 情况的回调函数[ **pfnAllocateCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)。 但是，此限制不适用于主副本。 有关主要例外的详细信息，请参阅[主要例外](#primary-exceptions)。 因为某些应用程序可能需要同步析构的外观，必须确保该驱动程序，它调用*pfnDeallocateCb*的任何以前被共享的资源销毁在调用其[ **Flush(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_flush)函数。 驱动程序必须也清除任何以前对其 Flush(D3D10) 函数; 的调用期间销毁对象 （仅将不会出现延迟管道的那些）该驱动程序必须执行此操作以确保运行时作为官方清理机制调用 Flush(D3D10) 延迟销毁的对象的那些可能需要一种机制，此类的几个应用程序。 有关此机制的详细信息，请参阅[延迟析构和 Flush(D3D10)](#deferred-destruction-and-flush-d3d10)。 该驱动程序还必须确保已延迟析构的任何对象完全销毁之前的驱动程序[ **DestroyDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroydevice)函数返回在清理过程。

### <a name="deprecate-ability-to-allow-modification-of-free-threaded-ddis"></a>不推荐使用的功能的自由线程 DDIs 进行修改

Direct3D 11 版，显示的 API 级别概念的设备和即时上下文仍然捆绑在一起 DDI 级别的显示设备的旧概念。 此捆绑内容的显示设备和即时上下文最大化与之前版本 DDIs 的兼容性 (例如， [Direct3D 版本 10 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index))，并支持通过多个 Api 的多个版本时减少驱动程序变动量DDIs 的版本。 但是，此捆绑内容的显示设备和即时上下文产生令人困惑，DDI 因为线程处理的域不是非常明确。 相反，若要了解多个接口和这些接口中的函数的线程处理的要求，驱动程序开发人员必须引用的文档。

Direct3D 11 版 API 是它允许多个线程进入的主要功能创建并同时销毁函数。 此类功能与允许换出函数表指针的创建和销毁，作为函数中指定的 Direct3D 版本 10 DDI 语义的驱动程序不兼容[ **D3D10DDI\_DEVICEFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddi_devicefuncs)并[ **D3D10\_1DDI\_DEVICEFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10_1ddi_devicefuncs)允许。 因此，该驱动程序传递回函数指针后将创建 ([**CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice))，该驱动程序不应尝试通过修改这些特定函数指针来更改行为当使用的 Direct3D 版本 11 DDI 驱动程序运行时和驱动程序支持 DDI 线程时。 此限制适用于以开头的所有设备函数*pfnCreate*， *pfnOpen*， *pfnDestroy*， *pfnCalcPrivate*，和*pfnCheck*。 设备功能的所有其余强与相关联的即时上下文。 单线程操作一次即时上下文，因为它是有明确定义，若要继续允许驱动程序添加到热插拔即时上下文函数表项。

### <a name="pfnrendercb-versus-pfnperformamortizedprocessingcb"></a>与 pfnPerformAmortizedProcessingCb pfnRenderCb

Direct3D 版本 10 API 函数挂钩 Direct3D 运行时[ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)内核回调函数来执行摊销的处理 (即，而不是执行某些操作每个 API 函数调用时，该驱动程序执行每个许多 API 函数调用的摊销的的操作）。 API 通常使用这一机会进行整理高水印并刷新其延迟的对象析构队列，等等。

若要允许内核回调函数是为自由线程尽可能驱动程序，Direct3D API 不再使用[ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)当驱动程序支持的 Direct3D 版本 11 DDI。 因此，驱动程序支持的 Direct3D 版本 11 DDI 必须手动调用[ **pfnPerformAmortizedProcessingCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb)内核输入 DDI 的驱动程序在同一个线程的回调函数函数后，驱动程序提交的即时上下文 （或类似的频率） 上的命令缓冲区。 该操作应剪裁高水印，因为它将更具优势利用时，该驱动程序将生成命令缓冲区前导之前进行如此[状态刷新 DDI 回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

此外，驱动程序应注意的 API 分期付款问题，并尝试平衡它使用何种频率[ **pfnPerformAmortizedProcessingCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb)内核回调函数。 上一个极端情况下，该驱动程序可能会导致过度处理。 例如，如果该驱动程序始终调用*pfnPerformAmortizedProcessingCb*两次 （连续），可能是因为多个引擎使用情况，将会更有效的驱动程序来调用*pfnPerformAmortizedProcessingCb*仅一次。 在其他极端情况下，该驱动程序可能不允许 Direct3D API 来完成整个帧的任何工作，如果驱动程序永远不会调用*pfnPerformAmortizedProcessingCb*，可能是因为交替的帧呈现设计。 该驱动程序不需要调用*pfnPerformAmortizedProcessingCb*比自然会是的因为已超过了任何更频繁地 (例如，如果该驱动程序未调用*pfnPerformAmortizedProcessingCb*1 毫秒时间范围，它必须是时间抽取 API)。 该驱动程序需要仅确定哪些现有[ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)调用应伴随**pfnPerformAmortizedProcessingCb**和正常情况下，符合该操作的线程处理语义。

有关支持命令列表的驱动程序，这些驱动程序还必须调用[ **pfnPerformAmortizedProcessingCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb)从延迟的上下文，只要这些驱动程序运行的空间不足 (以相似频率为每个即时上下文刷新）。 Direct3D 11 版运行时，需要在此类操作期间，至少剪裁其高水印。 因为与线程处理语义，它相关[ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)已宽松的 Direct3D 版本 11，并发问题必须解决以便 Direct3D 版本以继续挂钩11**pfnRenderCb**，而无任何限制。

### <a name="new-ddi-error-code"></a>新 DDI 错误代码

D3DDDIERR\_创建 APPLICATIONERROR 错误代码为允许驱动程序参与验证 Direct3D 11 版 API 没有。 以前，如果该驱动程序返回 E\_INVALIDARG 错误代码，这会导致引发异常的 API。 调试层存在将导致调试输出，指示该驱动程序必须返回了内部错误。 调试输出会建议对开发人员驱动程序存在一个 bug。 如果该驱动程序返回 D3DDDIERR\_APPLICATIONERROR，应用程序而出现故障，调试层确定。

### <a name="retroactively-requiring-free-threaded-calcprivate-ddis"></a>以追溯方式要求自由线程 CalcPrivate DDI

以开头的 Direct3D 版本 11 以追溯方式进行需要驱动程序函数*pfnCalcPrivate* Direct3D 版本 10 DDI 函数来自由线程上。 此追溯要求匹配的 Direct3D 版本 11 行为 DDI 为总是要求*pfnCalcPrivate\** 并[ **pfnCalcDeferredContextHandleSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcdeferredcontexthandlesize)函数是自由线程即使驱动程序指示它不支持 DDI 线程处理。 有关此追溯要求的详细信息，请参阅[Retroactively Requiring Free-Threaded CalcPrivate DDIs](retroactively-requiring-free-threaded-calcprivate-ddis.md)。

### <a name="deferred-destruction-and-flush-d3d10"></a>延迟的析构和刷新 D3D10

因为所有 destroy 函数现在都是自由线程，Direct3D 运行时不能在析构过程中刷新命令缓冲区。 因此，直到该驱动程序可以确保操作的即时上下文的线程不再依赖于该对象可以经受住 destroy 函数必须将推迟实际销毁对象。 每个离散的即时上下文方法不能有效地使用同步来解决此析构问题;因此，该驱动程序应同步仅当使用刷新命令缓冲区。 它必须处理类似问题时，Direct3D 运行时也使用此相同的设计。

由于延迟析构的批准，Direct3D 运行时负责支持无法容忍延迟析构的解决方法这些应用程序改为使用显式的机制。 因此，该驱动程序必须在调用到期间处理其延迟析构队列及其[ **Flush(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_flush)函数 （即使命令缓冲区为空） 以确保这些机制实际工作。

那些需要同步析构的窗体的应用程序必须使用以下模式之一，具体取决于如何重量级选手析构它们需要：

-   应用程序可确保释放该对象上的所有依赖项后 （即，命令列表、 视图、 中间件等），该应用程序使用以下模式：
    ```cpp
    Object::Release(); // Final release
    ImmediateContext::ClearState(); // Remove all ImmediateContext references as well.
    ImmediateContext::Flush(); // Destroy all objects as quickly as possible.
    ```

-   下面的模式是多个 heavywight 析构：
    ```cpp
    Object::Release(); // Final release
    ImmediateContext::ClearState(); // Remove all ImmediateContext references as well.
    ImmediateContext::Flush();
    ImmediateContext::End( EventQuery );
    while( S_FALSE == ImmediateContext::GetData( EventQuery ) ) ;
    ImmediateContext::Flush(); // Destroy all objects, completely.
    ```

### <a name="primary-exceptions"></a>主要异常

主副本是在对驱动程序的调用中，运行时创建的资源[ **CreateResource(D3D11)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)函数。 运行时通过设置创建一个主**pPrimaryDesc**的成员[ **D3D11DDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)指向的有效指针的结构[**DXGI\_DDI\_主\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)结构。 主数据库具有方面从 Direct3D 10 到 Direct3D 11 上述更改以下值得注意的例外情况：

-   这两个驱动程序[ **CreateResource(D3D11)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)并[ **DestroyResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource)函数的主副本不是自由线程，和它们共享线程处理域的即时上下文。 并发性可以仍存在包含函数的开头*pfnCreate*并*pfnDestroy*，其中包括 CreateResource(D3D11) 和 DestroyResource(D3D10)。 但是，存在并发性不能**CreateResource(D3D11)** 并**DestroyResource(D3D10)** 的主副本。 例如，对其 CreateResource(D3D11) 或 DestroyResource(D3D10) 函数的调用是为主要副本，并从而确定可以安全地使用或函数调用的持续时间内接触即时上下文内存，可以检测到驱动程序。

-   不能由 Direct3D 运行时，延迟主析构和驱动程序必须调用[ *pfnDeallocateCb* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)适当内驱动程序的调用的函数[ **DestroyResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource)函数。

 

 

