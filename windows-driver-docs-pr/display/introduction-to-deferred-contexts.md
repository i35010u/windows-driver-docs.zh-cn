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
ms.openlocfilehash: 97a2ec4d8d7a7740bca9bcf5da6cb72a7eec3169
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066034"
---
# <a name="introduction-to-deferred-contexts"></a>延迟上下文简介


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

应用程序使用延迟的上下文创建命令列表。 如果用户模式显示驱动程序指示它通过 \_ \_ \_ [**D3D11DDI \_ 线程处理 \_ 端**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_threading_caps) 结构的 D3D11DDICAPS COMMANDLISTS BUILD 2 标志支持命令列表，则它还必须支持创建和操作延迟上下文的功能。 有关驱动程序如何指示线程功能的详细信息，请参阅 [支持线程处理、命令列表和三维管道](supporting-threading--command-lists--and-3-d-pipeline.md)。 延迟上下文不同于直接上下文，因为在应用程序通过执行生成的命令列表显式请求执行这些命令之前，不能执行延迟的上下文记录的命令。 若要创建和使用延迟上下文，Direct3D 版本11提供以下新的 DDI 函数。 这些函数是创建设备/立即上下文组合所需的信息的子集。

-   [**AbandonCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_abandoncommandlist)

-   [**CalcPrivateDeferredContextSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatedeferredcontextsize)

-   [**CreateDeferredContext**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)

-   [**RecycleCreateDeferredContext**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatedeferredcontext)

[**CalcPrivateDeferredContextSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatedeferredcontextsize)和[**CreateDeferredContext**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)函数的语义类似于其他类似的 DDI 函数。

Direct3D 运行时为每个对驱动程序的 [**CreateDeferredContext**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext) 函数的调用传入新的驱动程序句柄和核心层句柄，以创建每个延迟的上下文。 每个延迟上下文的管道状态必须与在其上执行清除状态操作后立即上下文具有的管道状态等效。 驱动程序必须填写[**D3D11DDI \_ DEVICEFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs)结构的成员， [**D3D11DDIARG \_ CREATEDEFERREDCONTEXT**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext)结构的**p11ContextFuncs**成员用它的函数表中的一个函数子集来指向它们; 运行时使用 D3D10DDI HDEVICE 的 hDrvContext 成员指定的每个相应延迟上下文 D3D11DDIARG CREATEDEFERREDCONTEXT \_ **hDrvContext**句柄值 \_ 。

驱动程序必须继续为延迟上下文提供以 *pfnCreate*、 *pfnOpen*和 *pfnDestroy* 开头的函数。 这些函数与延迟上下文的其余部分共享相同的线程语义，它们用于打开和关闭上下文本地 DDI 句柄，如 [使用上下文本地 Ddi 句柄](using-context-local-ddi-handles.md)中所述。 以 *pfnCalcPrivate* 或 *pfnCheck* 开头的函数不用于延迟的上下文;因此，当创建延迟的上下文时，驱动程序可以将这些函数的 [**D3D11DDI \_ DEVICEFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs) 的成员设置为 **NULL** 。 大多数剩余的设备函数都利用延迟的上下文支持。 不过，驱动程序不会利用它的 [**QueryGetData**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_querygetdata) 函数。 但是，驱动程序利用了其 [**windows.applicationmodel.resources.core.resourcemap**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap) 和 [**ResourceUnmap**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceunmap) 函数。 驱动程序仅在即时上下文中通过使用即时上下文句柄，为 Direct3D 版本11资源夹紧支持 [**ResourceIsStagingBusy**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceisstagingbusy) 函数和新的 DDI 函数。 有关不能用于延迟上下文的函数的完整列表，请参阅 [排除延迟上下文的 DDI 函数](excluding-ddi-functions-for-deferred-contexts.md)。

该驱动程序利用在[**D3D11DDIARG \_ CREATEDEFERREDCONTEXT**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext)的**p11UMCallbacks**成员指向的内存块中提供的核心层回调函数。 这些核心层回调函数为每个延迟的上下文提供刷新状态 DDI。 但最重要的是，添加了 [**pfnPerformAmortizedProcessingCb**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb) 回调函数，该函数在 [Direct3D 10 的更改](changes-from-direct3d-10.md)中进行了介绍。

驱动程序不应期望[**D3D11DDI \_ CORELAYER \_ DEVICECALLBACKS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_corelayer_devicecallbacks)的**pfnDisableDeferredStagingResourceDestruction**成员有效的[**pfnDisableDeferredStagingResourceDestruction**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_disable_deferred_staging_resource_destruction_cb)回调函数。 驱动程序应在设备/直接上下文的[**CreateDevice (D3D10) **](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数中调用**pfnDisableDeferredStagingResourceDestruction** ;此后，驱动程序绝不应通过新的 Direct3D 版本 11 DDI 语义调用**pfnDisableDeferredStagingResourceDestruction** 。

驱动程序的 [**RecycleCreateDeferredContext**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatedeferredcontext) 函数必须清除延迟上下文的管道状态，类似于驱动程序的 [**CreateDeferredContext**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext) 清除延迟上下文的管道状态的方式。 在运行时调用驱动程序的 [**AbandonCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_abandoncommandlist)、 [**CreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcommandlist)或 [**RecycleCreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)后，运行时可以对驱动程序的 [**DestroyDevice (D3D10) **](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroydevice) 或 **RecycleCreateDeferredContext** 函数使用延迟的上下文句柄。 有关 **RecycleCreateDeferredContext**的详细信息，请参阅 [小型命令列表的优化](supporting-command-lists.md)。

 

