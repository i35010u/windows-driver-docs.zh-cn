---
title: 支持线程、命令列表和 3-D 管道
description: 支持线程、命令列表和 3-D 管道
ms.assetid: 2c5adc7d-b8ac-48d2-9777-b3d9fbba829a
keywords:
- Direct3D 版本 11 WDK Windows 7 显示，线程支持
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示，线程支持
- Direct3D 版本 11 WDK Windows 7 显示，命令列表支持
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示，命令列表支持
- Direct3D 版本 11 WDK Windows 7 显示，三维管道支持
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示，三维管道支持
- Direct3D 版本 11 WDK Windows 7 显示的线程支持
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示的线程支持
- 命令列表支持 Direct3D 版本 11 WDK Windows 7 显示
- tcommand 列表支持 Direct3D 版本 11 WDK Windows Server 2008 R2 显示器
- Direct3D 版本 11 WDK Windows 7 显示的管道支持
- 针对 Direct3D 版本 11 WDK Windows Server 2008 R2 显示的管道支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13e0bc87ad6814f46db8aeda1a3c003a28cbd71d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829373"
---
# <a name="supporting-threading-command-lists-and-3-d-pipeline"></a>支持线程、命令列表和 3-D 管道


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

当 Direct3D 版本11运行时调用驱动程序的[**GetCaps （D3D10\_2）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getcaps)函数时，用户模式显示驱动程序指示它支持的新 Direct3D 版本11功能（例如，线程处理、命令列表和三维管道）。 *GetCaps （D3D10\_2）* 是驱动程序在[**D3D10\_2DDI\_ADAPTERFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)结构中提供的驱动程序的特定于适配器的一种功能，pAdapterFuncs **\_2** [**成员 D3D10DDIARG\_OPENADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)结构指向。 有关在驱动程序初始化期间提供特定于适配器的函数的详细信息，请参阅[初始化与 Direct3D 版本 11 DDI 的通信](initializing-communication-with-the-direct3d-version-11-ddi.md)。 调用**GetCaps （D3D10\_2）** 函数时，用户模式显示驱动程序提供基于请求类型（在 D3D10\_2DDIARG 的**type**成员中指定）的新 Direct3D 版本11功能[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddiarg_getcaps) *GETCAPS （D3D10\_2）* 函数的*PDATA*参数指向的 GETCAPS 结构。

### <a name="span-idthreading_and_command_listsspanspan-idthreading_and_command_listsspan-threading-and-command-lists"></a><span id="threading_and_command_lists"></span><span id="THREADING_AND_COMMAND_LISTS"></span>线程和命令列表

Direct3D 版本 11 API 需要一种操作模式，在该模式下，它可以同步应用程序线程，以确保每次只有一个线程在 DDI 中运行。 Direct3D 版本 11 API 还需要一种操作模式，其中包含命令列表的软件模拟。 这种操作模式是必需的，并在以前版本的 DDIs （如[Direct3D 版本 10 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)）上利用。 因此，作为驱动程序编写者的开发帮助，这些相同的操作模式将扩展到 Direct3D 版本 11 DDI 上。 驱动程序编写器可以决定它们要为 Direct3D 版本 11 DDI 支持的操作模式。

所有驱动程序都应最终完全支持所有类型的线程操作（也就是说，所有驱动程序最终都应支持 D3D11DDI 的所有线程功能[ **\_线程\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_threading_caps)结构）。 但是，驱动程序可能要求 API 模拟命令列出或强制执行针对驱动程序的单线程操作模式。 API 在创建 API 设备期间，但在创建 DDI 设备之前，必须注意驱动程序的线程处理功能。 因此，当调用驱动程序的[**GetCaps （D3D10\_2）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getcaps)适配器特定函数时，运行时将确定驱动程序的线程功能，其中**Type**成员[**D3D10\_2DDIARG\_GetCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddiarg_getcaps)设置为D3D11DDICAPS\_线程。 驱动程序将返回一个指针，该指针指向用于标识驱动程序线程功能的 D3D10\_2DDIARG\_GETCAPS 的**pData**成员中的**D3D11DDI\_串接\_cap**结构。 如果驱动程序还支持命令列表（D3D11DDICAPS\_COMMANDLISTS\_BUILD\_2），则该驱动程序必须支持自由线程模式（D3D11DDICAPS\_FREETHREADED），因为命令会列出自由线程模式下的生成。 驱动程序必须选择支持自由线程模式和命令列表。 应用程序可以通过使用应用程序级**CheckFeatureSupport**函数和 D3D11\_功能\_线程常数来确定驱动程序的支持;但是，某些应用程序可能不会考虑 API 提供的支持。

### <a name="span-idthree_d_pipeline_levelspanspan-idthree_d_pipeline_levelspan3-d-pipeline-level"></a><span id="three_d_pipeline_level"></span><span id="THREE_D_PIPELINE_LEVEL"></span>三维管道级别

支持 Direct3D 版本 11 DDI 的驱动程序无需支持 Direct3D 版本 11 DDI 的所有硬件功能。 驱动程序可以支持仅支持[direct3d 版本 10 ddi](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)的基于硬件的 direct3d 版本 11 ddi 的新线程模型。 当运行时调用驱动程序的[**GetCaps （D3D10\_2）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getcaps)函数和[**D3D10\_2DDIARG\_GetCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddiarg_getcaps)集的**类型**成员时，Direct3D 版本11运行时将确定驱动程序的最高硬件级别支持\_3DPIPELINESUPPORT 的 D3D11DDICAPS。 驱动程序将返回一个指针，该指针指向用于标识支持的最高硬件级别的**D3D10\_2DDIARG\_GETCAPS**的**pData**成员中的[**D3D11DDI\_3DPIPELINESUPPORT\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_3dpipelinesupport_caps)结构。

API 不只使用 DDI 版本作为 API 功能级别支持的主要指标;该 API 允许驱动程序回送到此进程。 运行时在设备的[**CreateDevice （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数调用中选择[**D3D11DDI\_3DPIPELINELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11ddi_3dpipelinelevel)值并将该值回送到驱动程序，作为 D3D10DDIARG**标志**成员的一部分。 [ **\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)结构。

如果驱动程序在 Direct3D 版本 11 DDI 上支持的硬件级别低于 Direct3D 版本11，则驱动程序的操作将有很大的影响。 第一种情况是，Direct3D 版本11运行时根本不会调用许多新的 Direct3D 版本 11 DDI 函数。 例如，如果驱动程序支持的硬件功能级别低于 Direct3D 11 版，则 Direct3D 版本11运行时不会调用任何新的着色器-阶段 DDI 函数（如[**DsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)）。 其他 DDI 函数遵循功能级别的规则，并忽略 Direct3D 版本 11 DDI 可能与更高的功能关联的事实。 例如，尽管 Direct3D 版本 11 API 的 IAVertexInputSlots 是32，但 Direct3D 版本10功能级别仅允许16，这是驱动程序应该会出现的情况。

不推荐使用或已转换的功能提供另一个有趣的方面。 不能在 Direct3D 版本 11 DDI 级别上弃用，因为弃用必须支持能够表达早期版本 DDI 函数。 例如，PIPELINESTATS 的 Direct3D 11 API 版本始终是常量;但是，它会请求不同的[**D3D10\_DDI\_QUERY\_数据\_管道\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_ddi_query_data_pipeline_statistics)含 Direct3D 10 功能级别的统计信息，以及[**D3D11\_DDI\_查询\_数据\_管道\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_ddi_query_data_pipeline_statistics)带有 Direct3D 11 功能级别的统计信息，等等。 即使 API 试图弃用文本筛选器大小，驱动程序也更容易弃用 DDI 函数表项，而不是尝试重复使用函数表项来执行其他操作。

即使支持 Direct3D 版本 11 DDI 的驱动程序不支持完整的 Direct3D 版本11功能级别，驱动程序也无法选择退出 "扩展格式识别"，如[支持扩展格式识别](supporting-extended-format-awareness.md)中所述。 由于驱动程序支持 Direct3D 版本 11 DDI，驱动程序应处理以下任务：

-   支持 BGR 格式

-   正确响应对其[**CheckFormatSupport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkformatsupport)函数的调用，以检查是否有 XR\_偏向支持。 驱动程序应声明支持或拒绝支持。

-   允许强制转换完全类型的后台缓冲区

Direct3D 版本 11 API 还通知驱动程序应用程序是否通过 D3D11DDI\_CREATEDEVICE\_标志\_SINGLETHREADED 标志来使用多个线程。 如果在通过调用驱动程序的[**CREATEDEVICE （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数创建显示设备时， [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)结构的**Flags**成员中存在此标志，则驱动程序可以确定不延迟将创建上下文并且不需要驱动程序进行同步，因为不会出现并发创建。

 

 





