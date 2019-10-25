---
title: 延迟上下文简介
description: 延迟上下文简介
ms.assetid: a417bcc7-ca86-4853-baa3-415214da348f
keywords:
- Direct3D 版本 11 WDK Windows 7 显示，延迟上下文，简介
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示，延迟上下文，简介
- 延迟的上下文 WDK Windows 7 显示，简介
- 延迟的上下文 WDK Windows Server 2008 R2 显示，简介
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6769a5c0f1d57664365be1e5cf5fcd6ddf9cb28
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840350"
---
# <a name="introduction-to-deferred-contexts"></a>延迟上下文简介


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

应用程序使用延迟的上下文创建命令列表。 如果用户模式显示驱动程序指示它支持通过 D3D11DDICAPS\_COMMANDLISTS\_生成\_2 标志的[**D3D11DDI\_线程\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_threading_caps)结构，则它还必须支持创建和操作延迟的上下文。 有关驱动程序如何指示线程功能的详细信息，请参阅[支持线程处理、命令列表和三维管道](supporting-threading--command-lists--and-3-d-pipeline.md)。 延迟上下文不同于直接上下文，因为在应用程序通过执行生成的命令列表显式请求执行这些命令之前，不能执行延迟的上下文记录的命令。 若要创建和使用延迟上下文，Direct3D 版本11提供以下新的 DDI 函数。 这些函数是创建设备/立即上下文组合所需的信息的子集。

-   [**AbandonCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_abandoncommandlist)

-   [**CalcPrivateDeferredContextSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatedeferredcontextsize)

-   [**CreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)

-   [**RecycleCreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatedeferredcontext)

[**CalcPrivateDeferredContextSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatedeferredcontextsize)和[**CreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)函数的语义类似于其他类似的 DDI 函数。

Direct3D 运行时为每个对驱动程序的[**CreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)函数的调用传入新的驱动程序句柄和核心层句柄，以创建每个延迟的上下文。 每个延迟上下文的管道状态必须与在其上执行清除状态操作后立即上下文具有的管道状态等效。 驱动程序必须将[**D3D11DDIARG\_CREATEDEFERREDCONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext)结构的**p11ContextFuncs**成员指向的[**D3D11DDI\_DEVICEFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs)结构的成员填充到其函数中的一个函数子集数据表运行时使用每个对应的延迟上下文 D3D10DDI\_HDEVICE 句柄值，D3D11DDIARG\_CREATEDEFERREDCONTEXT 的**hDrvContext**成员指定此函数表。

驱动程序必须继续为延迟上下文提供以*pfnCreate*、 *pfnOpen*和*pfnDestroy*开头的函数。 这些函数与延迟上下文的其余部分共享相同的线程语义，它们用于打开和关闭上下文本地 DDI 句柄，如[使用上下文本地 Ddi 句柄](using-context-local-ddi-handles.md)中所述。 以*pfnCalcPrivate*或*pfnCheck*开头的函数不用于延迟的上下文;因此，当创建延迟的上下文时，驱动程序可以将这些函数的[**D3D11DDI\_DEVICEFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs)的成员设置为**NULL** 。 大多数剩余的设备函数都利用延迟的上下文支持。 不过，驱动程序不会利用它的[**QueryGetData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_querygetdata)函数。 但是，驱动程序利用了其[**windows.applicationmodel.resources.core.resourcemap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)和[**ResourceUnmap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceunmap)函数。 驱动程序仅在即时上下文中通过使用即时上下文句柄，为 Direct3D 版本11资源夹紧支持[**ResourceIsStagingBusy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceisstagingbusy)函数和新的 DDI 函数。 有关不能用于延迟上下文的函数的完整列表，请参阅[排除延迟上下文的 DDI 函数](excluding-ddi-functions-for-deferred-contexts.md)。

该驱动程序利用内存块中提供的核心层回调函数，这些函数在[**D3D11DDIARG\_CREATEDEFERREDCONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext)指向的**p11UMCallbacks**成员。 这些核心层回调函数为每个延迟的上下文提供刷新状态 DDI。 但最重要的是，添加了[**pfnPerformAmortizedProcessingCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb)回调函数，该函数在[Direct3D 10 的更改](changes-from-direct3d-10.md)中进行了介绍。

驱动程序不应期望 D3D11DDI\_CORELAYER\_的**pfnDisableDeferredStagingResourceDestruction**成员的[**PFNDISABLEDEFERREDSTAGINGRESOURCEDESTRUCTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_disable_deferred_staging_resource_destruction_cb)回调函数[**DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_corelayer_devicecallbacks)指向有效的点。 对于设备/直接上下文，驱动程序应在[**CreateDevice （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数内调用**pfnDisableDeferredStagingResourceDestruction** ;此后，驱动程序绝不应通过新的 Direct3D 版本 11 DDI 语义调用**pfnDisableDeferredStagingResourceDestruction** 。

驱动程序的[**RecycleCreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatedeferredcontext)函数必须清除延迟上下文的管道状态，类似于驱动程序的[**CreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)清除延迟上下文的管道状态的方式。 运行时调用驱动程序的[**AbandonCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_abandoncommandlist)、 [**CreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcommandlist)或[**RecycleCreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)后，运行时可以将延迟的上下文句柄用于驱动程序的[**DestroyDevice （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroydevice)或**RecycleCreateDeferredContext**函数。 有关**RecycleCreateDeferredContext**的详细信息，请参阅[小型命令列表的优化](supporting-command-lists.md)。

 

 





