---
title: 使用 Context-Local DDI 句柄
description: 使用 Context-Local DDI 句柄
ms.assetid: 1b3e5c29-9b9e-4c10-8fe0-706255c8fd91
keywords:
- Direct3D 版本显示 11 WDK Windows 7，延迟的上下文中，使用上下文本地 DDI 句柄
- Direct3D 11 版 WDK Windows Server 2008 R2 显示，延迟上下文中，使用上下文本地 DDI 句柄
- 显示延迟的上下文 WDK Windows 7，请使用上下文本地 DDI 句柄
- 显示延迟的上下文 WDK Windows Server 2008 R2，请使用上下文本地 DDI 句柄
- 上下文本地 DDI 处理 WDK Windows 7 显示
- 上下文本地 DDI 处理 WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9eba46348708bb01572e3f9aa2a0b153052d622d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562089"
---
# <a name="using-context-local-ddi-handles"></a>使用 Context-Local DDI 句柄


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

每个对象 （例如，资源、 着色器，等等） 都有上下文本地 DDI 句柄。

假设一个对象使用具有三个延迟的上下文。 在此情况下，四个句柄引用同一对象 （每个推迟的上下文的一个句柄） 和即时上下文的另一个句柄。 因为每个上下文可以同时操作的线程，则可确保本地上下文句柄，多个 CPU 线程不会争用通过类似的内存 （有意或无意）。 本地上下文句柄还有直观，因为驱动程序可能必须修改这种数据仍是逻辑上相关联的每个上下文 （例如，对象可能受在上下文中，依次类推）。

仍是即时上下文句柄与延迟的上下文句柄的区别。 具体而言，要分配的第一个句柄和销毁的最后一个句柄，保证进行即时上下文句柄。 在"打开"每个推迟的上下文句柄，以将它们链接在一起的过程提供相应的即时上下文句柄。 当前没有具有每个设备 DDI 句柄的对象的概念 (即，一个句柄，之前创建和销毁后即时上下文句柄，并且将仅按顺序由引用上下文句柄创建)。

某些句柄具有与其他句柄的依赖关系 （例如，对于视图有依赖关系及其相应的资源）。 创建和销毁顺序保证存在即时上下文扩展到延迟上下文句柄 （即，运行时创建上下文本地资源句柄之前，运行时创建的任何上下文-本地视图的句柄资源和运行时销毁上下文本地资源句柄后，运行时销毁该资源的所有上下文本地视图句柄）。 当运行时创建的本地上下文句柄时，则运行时提供相应的上下文本地依赖关系处理。

### <a name="span-iddriverdataorganizationspanspan-iddriverdataorganizationspandriver-data-organization"></a><span id="driver_data_organization"></span><span id="DRIVER_DATA_ORGANIZATION"></span>驱动程序的数据组织

有几个有关驱动程序数据所在组织的需要注意的问题。 类似于 Direct3D 版本 10，正确的数据区域可以降低缓存未命中数之间的 API 和驱动程序。 正确的数据区域也可以阻止缓存抖动，发生多个小的所有常访问的数据解析为相同的缓存索引和耗尽时按的缓存。 DDI 旨在之后的 Direct3D 版本 10 为了帮助避免此类问题从驱动程序通知 API 表现形式为满足句柄和句柄的值分配的 API 驱动程序需要的内存量。 但是，新线程相关的问题会影响在 Direct3D 11 版时间范围内的 DDI 设计。

正常情况下，本地上下文句柄提供一种方法将对象数据每个上下文，这样可以避免在线程之间的争用问题相关联。 但是，由于此类数据复制的每个推迟的上下文中，此类数据的大小是主要考虑因素。 它提供自然合理化共享之间的即时上下文句柄和推迟的上下文句柄的只读数据。 在创建期间的推迟的上下文句柄，提供即时上下文句柄是为了建立控点之间的连接。 但是，从推迟的上下文句柄所在的任何数据获得 API 数据局部性好处并且为只读数据的间接寻址的其他级别可防止局部性优势扩展到只读数据。 如果局部性好处产生重复数据，可以将一些只读数据复制到每个上下文句柄区域。 但是，支持每个推迟的上下文句柄的内存应考虑在此类，它可能值得重定位是从句柄不相邻，如果该数据是相对较大且不为其他数据为经常访问的数据。 理想情况下，该类型的与每个推迟的上下文句柄相关联的数据将所有高频率数据仍;因此，数据不会足够大，需要考虑重定位必要。 正常情况下，该驱动程序必须综合考虑这些冲突的动机。

若要使驱动程序的数据设计高效地兼容使用 Direct3D 版本 10，尚不在实现中，不同的只读数据应位于连续 （但仍隔离从和之后） 的即时上下文句柄数据。 如果驱动程序使用这种设计，该驱动程序必须了解缓存行填充，则需要即时上下文句柄数据之间的只读数据。 因为频繁地 （如果不同时），一个线程可能会处理每个上下文句柄数据，false 共享损失之间的即时上下文句柄数据和推迟的上下文句柄数据发生，如果未使用缓存行填充。 驱动程序设计必须确定的清单如果指针是建立和定期遍历上下文之间的 false 共享损失处理内存区域。

对本地推迟的上下文的句柄，Direct3D 运行时使用以下 Direct3D 11 DDI:

-   [ **CheckDeferredContextHandleSizes** ](https://msdn.microsoft.com/library/windows/hardware/ff539388)函数验证保存推迟的上下文句柄的句柄数据的驱动程序专用内存空间的大小。

-   [ **CalcDeferredContextHandleSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538272)函数确定的推迟的上下文的内存区域的大小。

对于以检索所需的驱动程序的延迟的上下文句柄大小 Direct3D 运行时，必须使用前面的 DDI 函数。 一个对象，用于即时上下文创建后立即, 运行时调用[ **CalcDeferredContextHandleSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538272)来查询该驱动程序要求的存储空间量的驱动程序满足此对象的延迟的上下文句柄。 但是，Direct3D API 必须通过确定多少唯一的句柄大小来调整其符合 CLS 的内存分配器并访问它们的值;运行时调用的驱动程序[ **CheckDeferredContextHandleSizes** ](https://msdn.microsoft.com/library/windows/hardware/ff539388)函数来获取此信息。 因此，在设备实例化期间 API 申请推迟的上下文句柄大小的数组的双精度轮询。 第一次轮询是请求返回多少大小，而第二个轮询传入要检索的每种大小的值的数组。 该驱动程序必须指示多少内存它为满足需要以及哪些句柄类型的句柄。 该驱动程序可以返回与特定的句柄类型相关联的多个大小。 但是，它是驱动程序来曾经返回的值未定义**CalcDeferredContextHandleSize**未也相应地返回在**CheckDeferredContextHandleSizes**数组。

与创建 DDI 句柄，使用推迟的上下文上的创建方法。 例如，检查[ **CreateBlendState (D3D10\_1)** ](https://msdn.microsoft.com/library/windows/hardware/ff540597)并[ **DestroyBlendState** ](https://msdn.microsoft.com/library/windows/hardware/ff552745)函数。 HDEVICE 自然地指向相应推迟的上下文 （而不是即时的上下文）;其他 CONST 结构指针**NULL** （假定该对象没有任何依赖项）; 和 D3D10DDI\_HRT\*句柄是 D3D10DDI\_H\*到相应的句柄即时上下文对象。

具有依赖项的对象 （例如，视图有依赖关系及其相应的资源），提供了依赖项句柄的结构指针不是**NULL**。 但是，结构中的唯一有效的成员是依赖项句柄;而其他成员都将用零填充。 例如， [ **D3D11DDIARG\_CREATESHADERRESOURCEVIEW** ](https://msdn.microsoft.com/library/windows/hardware/ff542073)驱动程序的调用中的指针[ **CreateShaderResourceView(D3D11)**](https://msdn.microsoft.com/library/windows/hardware/ff540708)函数不会**NULL**当运行时调用此函数上推迟的上下文。 在此 CreateShaderResourceView(D3D11) 调用中，运行时将分配到资源的相应本地上下文句柄**hDrvResource** D3D11DDIARG 成员\_CREATESHADERRESOURCEVIEW。 其余的 D3D11DDIARG 成员\_CREATESHADERRESOURCEVIEW，不过，补零。

下面的示例代码演示如何 Direct3D 运行时将转换应用程序的创建请求和首次使用推迟到对用户模式显示驱动程序调用，以创建即时与延迟上下文的上下文。 应用程序的调用**ID3D11Device::CreateTexture2D**启动以下"创建资源"部分中的运行时代码。 应用程序的调用**ID3D11Device::CopyResource**启动下面的"延迟的上下文资源使用情况"部分中的运行时代码。

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

### <a name="span-idissueswithpfnseterrorcbspanspan-idissueswithpfnseterrorcbspanissues-with-pfnseterrorcb"></a><span id="issues_with_pfnseterrorcb"></span><span id="ISSUES_WITH_PFNSETERRORCB"></span>PfnSetErrorCb 的问题

返回错误代码，可能适合使用 Direct3D 11 版线程模型的任何创建函数。 创建函数的所有使用[ **pfnSetErrorCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568929)检索错误代码将从驱动程序。 若要最大化与 Direct3D 版本 10 驱动程序模型的兼容性，新 DDI 创建返回错误代码被引入的函数。 相反，该驱动程序必须继续使用统一设备/即时上下文 D3D10DDI\_HRTCORELAYER 使用来处理**pfnSetErrorCb**期间创建函数。 该驱动程序支持命令列表，驱动程序应使用适当**pfnSetErrorCb**与对应的上下文相关联。 也就是说，推迟的上下文错误应转到特定推迟的上下文调用**pfnSetErrorCb**为相应的句柄，依此类推。

延迟的上下文可以返回电子\_通过调用 OUTOFMEMORY [ **pfnSetErrorCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568929)从以前仅允许 D3DDDIERR DDI 函数\_（如DEVICEREMOVED[**绘制**](https://msdn.microsoft.com/library/windows/hardware/ff556120)， [ **SetBlendState**](https://msdn.microsoft.com/library/windows/hardware/ff569527)，依此类推)，因为推迟的上下文内存需求永久增长 DDI 函数每次调用。 Direct3D API 将触发本地上下文删除，以帮助驱动程序和此类失败的情况，这有效地丢弃部分生成的命令列表。 应用程序以确定它正在记录的命令列表; 继续但是，当应用程序最终调用**FinishCommandList**函数， **FinishCommandList**返回 E 的失败代码\_发生内存不足。

 

 





