---
title: 使用 Context-Local DDI 句柄
description: 使用 Context-Local DDI 句柄
keywords:
- Direct3D 版本 11 WDK Windows 7 显示，延迟上下文，使用上下文本地 DDI 句柄
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示，延迟上下文，使用上下文本地 DDI 句柄
- 延迟上下文 WDK Windows 7 显示，使用上下文本地 DDI 句柄
- 延迟的上下文 WDK Windows Server 2008 R2 显示，使用上下文本地 DDI 句柄
- 上下文本地 DDI 处理 WDK Windows 7 显示
- 上下文本地 DDI 处理 WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cedf9bfc6928c53dcf8e8efc3a88adeef2d9ec50
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818579"
---
# <a name="using-context-local-ddi-handles"></a>使用 Context-Local DDI 句柄


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

每个对象 (例如，资源、着色器等) 具有上下文本地 DDI 句柄。

假设对象与三个延迟的上下文一起使用。 在这种情况下，四个句柄指的是同一对象 (每个延迟上下文的一个句柄，另一个句柄用于即时上下文) 。 由于每个上下文都可由线程并发操作，因此上下文本地句柄可确保多个 CPU 线程不会争用类似的内存 (有意或无意地) 。 上下文本地句柄也是直观的，因为驱动程序可能必须修改每个上下文在逻辑上相关联的大部分数据 (例如，对象可能被上下文绑定，依此类推) 。

还有一个直接的上下文句柄与延迟的上下文句柄的区别。 具体而言，可保证直接上下文句柄是所分配的第一个句柄和最后一个已销毁的句柄。 在每个延迟的上下文句柄的 "正在打开" 过程中提供相应的即时上下文句柄，以将它们链接在一起。 当前没有具有每个设备 DDI 句柄的对象的概念 (即，在即时上下文句柄之后和销毁之前创建的句柄，只能通过上下文句柄创建) 进行引用。

某些句柄与其他句柄具有依赖关系 (例如，视图依赖于其相应的资源) 。 为即时上下文提供的创建和析构顺序保证也扩展到延迟的上下文句柄 (也就是说，运行时在运行时创建上下文本地资源句柄，然后运行时在运行时创建该资源的任何上下文本地视图句柄，并在运行时将所有上下文本地视图句柄销毁到该资源) 之后，运行时销毁该资源句柄。 当运行时创建上下文本地句柄时，运行时也提供相应的上下文本地依赖关系句柄。

### <a name="span-iddriver_data_organizationspanspan-iddriver_data_organizationspandriver-data-organization"></a><span id="driver_data_organization"></span><span id="DRIVER_DATA_ORGANIZATION"></span>驱动程序数据组织

需要注意的驱动程序数据组织有一些问题。 与 Direct3D 版本10一样，数据的适当位置可以减少 API 与驱动程序之间的缓存未命中。 适当位置的数据也会阻止缓存失效，这是因为经常访问的多个数据片段都解析为同一缓存索引，并耗尽缓存的表现。 自 Direct3D 版本10起，DDI 的设计目的是为了帮助避免驱动程序从 manifesting 中避免此类问题，告知 API 驱动程序需要多少内存来满足句柄，并使用 API 来分配句柄的值。 但是，新的与线程相关的问题会影响 Direct3D 版本11时间范围内的 DDI 设计。

当然，上下文本地句柄提供了一种将对象数据与每个上下文相关联的方法，从而避免了线程间的争用问题。 但是，由于此类数据是针对每个延迟的上下文进行复制的，因此这种数据的大小是一个主要考虑因素。 这使自然合理化可以在即时上下文句柄和延迟的上下文句柄之间共享只读数据。 在创建延迟的上下文句柄期间，将提供直接的上下文句柄以在句柄之间建立连接。 但是，位于延迟的上下文中的任何数据都将利用 API 数据获取地区权益，而对只读数据的额外级别的间接寻址可防止区域受益于扩展为只读数据。 某些只读数据可以复制到每个上下文句柄区域，前提是该区域的优势在于数据重复。 但是，在这种高级版上，应考虑支持每个延迟的上下文句柄的内存。如果数据相对较大且不能像其他数据一样频繁地进行访问，则可能需要重新定位与句柄无关的数据。 理想情况下，与每个延迟的上下文句柄关联的数据类型仍为所有高频数据;因此，数据不会足够大，因此不需要重定位。 当然，驱动程序必须与这些冲突动机进行平衡。

为了使驱动程序数据设计与 Direct3D 版本10（但不是实现中的共存）有效地兼容，只读数据应位于连续 (中，但仍会在) 即时上下文句柄数据之前和之后相互隔离。 如果驱动程序使用此设计，则驱动程序必须知道直接上下文句柄数据和只读数据之间需要缓存行填充。 由于线程可能会频繁地处理每个上下文句柄数据 (如果不同时) ，则在未使用缓存行填充时，直接上下文句柄数据和延迟的上下文句柄数据之间将发生错误的共享罚款。 如果在上下文句柄内存区域之间定期建立和遍历了指针，则驱动程序的设计必须是 cognizant 的错误共享罚款。

Direct3D 运行时对延迟的上下文本地句柄使用以下 Direct3D 11 DDI：

-   [**CheckDeferredContextHandleSizes**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_checkdeferredcontexthandlesizes)函数验证驱动程序的大小-专用内存空间，其中包含延迟的上下文句柄的句柄数据。

-   [**CalcDeferredContextHandleSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcdeferredcontexthandlesize)函数确定延迟上下文的内存区域大小。

为了使 Direct3D 运行时检索驱动程序所需的延迟上下文句柄大小，必须使用前面的 DDI 函数。 立即为直接上下文创建对象后，运行时将调用 [**CalcDeferredContextHandleSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcdeferredcontexthandlesize) 来查询驱动程序，以查找驱动程序为满足此对象延迟的上下文句柄而需要的存储空间量。 但是，Direct3D API 必须通过确定访问的唯一句柄大小及其值，来优化其 CLS 内存分配器;运行时调用驱动程序的 [**CheckDeferredContextHandleSizes**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_checkdeferredcontexthandlesizes) 函数来获取此信息。 因此，在设备实例化过程中，API 通过双重轮询请求延迟的上下文句柄大小的数组。 第一次轮询是请求返回多少大小，而第二次轮询传入数组以检索每个大小的值。 驱动程序必须指示满足一个句柄以及哪种句柄类型所需的内存量。 驱动程序可以返回与特定句柄类型相关联的多个大小。 但是，该驱动程序不确定该驱动程序从 **CalcDeferredContextHandleSize** 返回的值，这些值也不会在 **CheckDeferredContextHandleSizes** 数组中相应返回。

对于创建 DDI 句柄，使用延迟上下文的 create 方法。 例如，检查 [**CreateBlendState (D3D10 \_ 1)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_1ddi_createblendstate) 和 [**DestroyBlendState**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyblendstate) 函数。 HDEVICE 自然指向适当的延迟上下文 (与直接上下文) ;如果对象不具有依赖) 项，则其他常量结构指针为 **NULL** (;而且，D3D10DDI \_ HRT \* 句柄是 \_ \* 对应的即时上下文对象的 D3D10DDI H 句柄。

对于具有依赖关系的对象 (例如，视图在其对应的资源) 上具有依赖关系，提供依赖关系句柄的结构指针不是 **NULL**。 但是，该结构的唯一有效成员是依赖项句柄;而其余成员则用零填充。 例如，当运行时在延迟的上下文中调用此函数时，对驱动程序的 [**CREATESHADERRESOURCEVIEW (D3D11)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createshaderresourceview)函数的调用中的 [**D3D11DDIARG \_ CREATESHADERRESOURCEVIEW**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createshaderresourceview)指针将不会为 **NULL** 。 在此 CreateShaderResourceView (D3D11) 调用中，运行时将资源的适当上下文本地句柄分配给 D3D11DDIARG CreateShaderResourceView 的 **hDrvResource** 成员 \_ 。 但 D3D11DDIARG CREATESHADERRESOURCEVIEW 的其余成员将 \_ 用零填充。

下面的示例代码演示 Direct3D 运行时如何将应用程序的 create 请求和第一次使用延迟的上下文转换为对用户模式显示驱动程序的调用，以创建立即与延迟的上下文。 应用程序对 **ID3D11Device：： CreateTexture2D** 的调用将在以下 "资源创建" 部分启动运行时代码。 应用程序对 **ID3D11Device：： CopyResource** 的调用将在以下 "延迟的上下文资源使用情况" 部分启动运行时代码。

```cpp
// Device Create
 IC::pfnCheckDeferredContextHandleSizes( hIC, &u, NULL );
pArray = malloc( u * ... );
IC::pfnCheckDeferredContextHandleSizes( hIC, &u, pArray );

// Resource Create
 s = IC::pfnCalcPrivateResourceSize( hIC, &Args );
pICRHandle = malloc( s );
 IC::pfnCreateResource( hIC, &Args, pICRHandle, hRTResource );
 s2 = IC::pfnCalcDeferredContextHandleSize( hIC, D3D10DDI_HT_RESOURCE, pICRHandle );

// Deferred Context Resource Usage
pDCRHandle = malloc( s2 );
 DC::pfnCreateResource( hDC, NULL, pDCRHandle, pICRHandle );
```

### <a name="span-idissues_with_pfnseterrorcbspanspan-idissues_with_pfnseterrorcbspanissues-with-pfnseterrorcb"></a><span id="issues_with_pfnseterrorcb"></span><span id="ISSUES_WITH_PFNSETERRORCB"></span>PfnSetErrorCb 问题

任何 create 函数都不会返回错误代码，这非常适合于 Direct3D 版本11线程模型。 所有创建函数都使用 [**pfnSetErrorCb**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb) 从驱动程序检索错误代码。 若要最大程度地提高与 Direct3D 版本10驱动程序模型的兼容性，则不会引入返回错误代码的新 DDI create 函数。 相反，在创建功能期间，驱动程序必须继续使用统一设备/直接上下文 D3D10DDI \_ HRTCORELAYER 句柄和 **pfnSetErrorCb** 。 当驱动程序支持命令列表时，驱动程序应使用与相应上下文关联的相应 **pfnSetErrorCb** 。 也就是说，延迟上下文错误应发送到与相应句柄 **pfnSetErrorCb** 的特定延迟上下文调用。

延迟的上下文可以通过对 PfnSetErrorCb 的调用返回 E OUTOFMEMORY，这种情况 \_ 是以前仅允许 D3DDDIERR [**pfnSetErrorCb**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb) \_ DEVICEREMOVED (如 [**绘图**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_draw)、 [**SetBlendState**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setblendstate)等) ，因为每次调用 DDI 函数时，延迟的上下文内存需求永久会增长。 Direct3D API 会触发本地上下文删除，以帮助驱动程序解决此类故障情况，从而有效地丢弃部分生成的命令列表。 应用程序继续确定它正在记录命令列表;但是，当应用程序最终调用 **FinishCommandList** 函数时， **FinishCommandList** 将返回失败代码 E \_ OUTOFMEMORY。

 

