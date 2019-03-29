---
title: 延迟上下文简介
description: 延迟上下文简介
ms.assetid: a417bcc7-ca86-4853-baa3-415214da348f
keywords:
- Direct3D 11 版 WDK Windows 7 显示、 延迟的上下文简介
- Direct3D 11 版 WDK Windows Server 2008 R2 显示、 延迟的上下文简介
- 延迟的 WDK Windows 7 显示的上下文简介
- 延迟的上下文 WDK Windows Server 2008 R2 显示，简介
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf6bd9399a9c0ab4808fa3e28cde1ef2a8aa4680
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563704"
---
# <a name="introduction-to-deferred-contexts"></a>延迟上下文简介


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

延迟的上下文由应用程序中用于创建命令列表。 如果用户模式显示驱动程序表明它支持命令列表通过 D3D11DDICAPS\_COMMANDLISTS\_构建\_的 2 个标志[ **D3D11DDI\_线程处理\_CAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff542163)结构，它必须还支持创建和操作延迟的上下文的能力。 有关驱动程序如何指示线程功能的详细信息，请参阅[支持线程处理，命令将列出，和三维管道](supporting-threading--command-lists--and-3-d-pipeline.md)。 延迟的上下文不同从即时上下文，不能执行延迟的上下文记录的命令，直到应用程序显式请求执行命令，通过执行生成的命令列表。 若要创建和使用推迟的上下文，Direct3D 11 版提供了以下新 DDI 函数。 这些函数是信息的创建设备/即时上下文组合所需的子集。

-   [**AbandonCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff538199)

-   [**CalcPrivateDeferredContextSize**](https://msdn.microsoft.com/library/windows/hardware/ff538280)

-   [**CreateDeferredContext**](https://msdn.microsoft.com/library/windows/hardware/ff540622)

-   [**RecycleCreateDeferredContext**](https://msdn.microsoft.com/library/windows/hardware/ff569239)

语义[ **CalcPrivateDeferredContextSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538280)并[ **CreateDeferredContext** ](https://msdn.microsoft.com/library/windows/hardware/ff540622)函数是类似于其他类似DDI 函数。

驱动程序的每次调用，Direct3D 运行时将传递在新的驱动程序句柄和核心层句柄[ **CreateDeferredContext** ](https://msdn.microsoft.com/library/windows/hardware/ff540622)函数来创建每个推迟的上下文。 每个推迟的上下文的管道状态必须为等效于管道状态的即时上下文具有后对其执行清除状态操作。 该驱动程序必须填充的成员[ **D3D11DDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff542141)结构**p11ContextFuncs**隶属[ **D3D11DDIARG\_CREATEDEFERREDCONTEXT** ](https://msdn.microsoft.com/library/windows/hardware/ff542044)结构将用功能的一个子集的点从其函数表; 运行时使用每个相应推迟的上下文 D3D10DDI\_HDEVICE 句柄值**hDrvContext** D3D11DDIARG 成员\_CREATEDEFERREDCONTEXT 指定与此函数表。

该驱动程序必须继续提供函数的开头*pfnCreate*， *pfnOpen*，并*pfnDestroy*延迟的上下文。 这些函数共享相同的线程处理语义的推迟的上下文中，其余部分，它们用于打开和关闭上下文本地 DDI 句柄，如中所述[使用上下文本地 DDI 句柄](using-context-local-ddi-handles.md)。 函数的开头*pfnCalcPrivate*或*pfnCheck*不用于延迟上下文; 因此，该驱动程序可以设置的成员[ **D3D11DDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff542141)到这些函数的**NULL**推迟的上下文创建时。 推迟的上下文支持可利用大部分其余设备函数。 该驱动程序不会利用其[ **QueryGetData** ](https://msdn.microsoft.com/library/windows/hardware/ff569218)正常工作，不过。 但是，该驱动程序利用其[ **ResourceMap** ](https://msdn.microsoft.com/library/windows/hardware/ff569492)并[ **ResourceUnmap** ](https://msdn.microsoft.com/library/windows/hardware/ff569495)函数。 该驱动程序仅支持[ **ResourceIsStagingBusy** ](https://msdn.microsoft.com/library/windows/hardware/ff569491)函数和 Direct3D 11 版资源固定即时上下文通过使用即时上下文句柄的新 DDI 函数。 不用于延迟上下文的函数的完整列表，请参阅[延迟的上下文中不包括 DDI 函数](excluding-ddi-functions-for-deferred-contexts.md)。

核心层在内存中提供的回调函数驱动程序利用阻止**p11UMCallbacks**的成员[ **D3D11DDIARG\_CREATEDEFERREDCONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff542044)指向。 这些核心层回调函数为每个推迟的上下文条件刷新状态 DDI。 最重要的是，但是，是添加了[ **pfnPerformAmortizedProcessingCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568915)中所述的回调函数[从 Direct3D 10 更改](changes-from-direct3d-10.md)。

该驱动程序不应期望[ **pfnDisableDeferredStagingResourceDestruction** ](https://msdn.microsoft.com/library/windows/hardware/ff568906)所属的回调函数**pfnDisableDeferredStagingResourceDestruction**的成员[ **D3D11DDI\_CORELAYER\_DEVICECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff542137)点作为有效。 该驱动程序应具有名为**pfnDisableDeferredStagingResourceDestruction**内[ **CreateDevice(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540635)设备/即时上下文; 函数然后，该驱动程序应永远不会调用**pfnDisableDeferredStagingResourceDestruction**具有新的 Direct3D 版本 11 DDI 语义。

在驱动程序[ **RecycleCreateDeferredContext** ](https://msdn.microsoft.com/library/windows/hardware/ff569239)清除延迟的上下文中，管道状态类似于如何将驱动程序的函数必须[ **CreateDeferredContext** ](https://msdn.microsoft.com/library/windows/hardware/ff540622)清除推迟的上下文的管道状态。 运行时调用的驱动程序后[ **AbandonCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff538199)， [ **CreateCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff540602)，或[ **RecycleCreateCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff569238)，在运行时可以使用驱动程序使用推迟的上下文句柄[ **DestroyDevice(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff552768)或**RecycleCreateDeferredContext**函数。 有关详细信息**RecycleCreateDeferredContext**，请参阅[优化的小命令列表](supporting-command-lists.md)。

 

 





