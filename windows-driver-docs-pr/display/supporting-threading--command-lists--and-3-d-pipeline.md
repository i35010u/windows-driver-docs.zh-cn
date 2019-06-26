---
title: 支持线程、命令列表和 3-D 管道
description: 支持线程、命令列表和 3-D 管道
ms.assetid: 2c5adc7d-b8ac-48d2-9777-b3d9fbba829a
keywords:
- Direct3D 11 版 WDK Windows 7 显示的线程支持
- Direct3D 11 版 WDK Windows Server 2008 R2 显示的线程支持
- Direct3D 11 版 WDK Windows 7 显示，命令将列出支持
- Direct3D 11 版 WDK Windows Server 2008 R2 显示，命令将列出支持
- Direct3D 11 版 WDK Windows 7 显示三维管道支持
- Direct3D 11 版 WDK Windows Server 2008 R2 显示三维管道支持
- 线程处理对 Direct3D 11 版 WDK Windows 7 显示的支持
- 线程处理 Direct3D 版本 11 WDK Windows Server 2008 R2 显示的支持
- 命令将列出对 Direct3D 11 版 WDK Windows 7 显示的支持
- tcommand 列出了支持的 Direct3D 版本 11 WDK Windows Server 2008 R2 显示
- 管道 Direct3D 11 版 WDK Windows 7 显示的支持
- 管道 Direct3D 11 版 WDK Windows Server 2008 R2 显示的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73f3a919030c34a3c2ba53807b1b1c57b25a291d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361214"
---
# <a name="supporting-threading-command-lists-and-3-d-pipeline"></a>支持线程、命令列表和 3-D 管道


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

用户模式显示驱动程序指示它支持的新 Direct3D 11 版功能 （例如，线程处理，命令列表和三维管道） 在 Direct3D 11 版运行时调用的驱动程序[ **GetCaps(D3D10\_2)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getcaps)函数。 *GetCaps (D3D10\_2)* 是驱动程序中提供的驱动程序的特定于适配器的功能之一[ **D3D10\_2DDI\_ADAPTERFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)结构的**pAdapterFuncs\_2**的成员[ **D3D10DDIARG\_OPENADAPTER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)结构指向。 在驱动程序初始化过程中提供特定于适配器的函数的详细信息，请参阅[与 Direct3D 版本 11 DDI 初始化通信](initializing-communication-with-the-direct3d-version-11-ddi.md)。 当其**GetCaps (D3D10\_2)** 调用函数，用户模式显示驱动程序提供了新的请求类型的 Direct3D 版本 11 功能 (中指定**类型**成员[ **D3D10\_2DDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10_2ddiarg_getcaps)结构*GetCaps (D3D10\_2)* 函数的*pData*参数指向)。

### <a name="span-idthreadingandcommandlistsspanspan-idthreadingandcommandlistsspan-threading-and-command-lists"></a><span id="threading_and_command_lists"></span><span id="THREADING_AND_COMMAND_LISTS"></span> 线程处理和命令列表

Direct3D 11 版 API 要求它可以在其中同步应用程序线程以确保只有一个线程运行 DDI 中一次操作的模式。 Direct3D 11 版 API 还需要使用命令列出的软件模拟操作的模式。 这些操作模式是必需的情况并利用在之前版本 DDIs (例如， [Direct3D 版本 10 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index))。 因此，作为驱动程序编写人员，帮助开发一种操作的这些相同的模式进行了扩展，存在于 Direct3D 版本 11 DDI。 驱动程序编写人员可以决定哪些三种操作模式在这个时候其驱动程序以支持 Direct3D 版本 11 DDI。

所有驱动程序应最终完全支持所有类型的线程处理操作 (即，所有驱动程序最终应都支持的所有线程的功能[ **D3D11DDI\_线程处理\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddi_threading_caps)结构)。 但是，该驱动程序可能需要的 API 模拟命令列表，或强制实施的驱动程序的操作的单线程模式。 API 必须创建一款 API 的设备，但在之前创建 DDI 设备期间注意驱动程序的线程处理功能。 因此，运行时确定调用的驱动程序时，该驱动程序的线程处理功能[ **GetCaps (D3D10\_2)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getcaps)特定于适配器的函数和**类型**的成员[ **D3D10\_2DDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10_2ddiarg_getcaps)设置为 D3D11DDICAPS\_线程处理。 驱动程序将返回一个指向**D3D11DDI\_线程处理\_CAP**结构**pData** D3D10 成员\_2DDIARG\_GETCAPS，标识驱动程序的线程处理功能。 该驱动程序必须支持自由线程模式 (D3D11DDICAPS\_FREETHREADED) 如果该驱动程序还支持命令列表 (D3D11DDICAPS\_COMMANDLISTS\_生成\_2) 因为命令将列出生成上自由线程模式。 该驱动程序必须参加支持自由线程模式和命令列表。 应用程序可以确定驱动程序指示通过使用应用程序级别的支持**CheckFeatureSupport**函数和 D3D11\_功能\_线程处理常量; 但是，某些应用程序可能由于该 API 提供的支持并不关心。

### <a name="span-idthreedpipelinelevelspanspan-idthreedpipelinelevelspan3-d-pipeline-level"></a><span id="three_d_pipeline_level"></span><span id="THREE_D_PIPELINE_LEVEL"></span>三维管道级别

支持 11 DDI 不支持所需的 Direct3D 版本 11 的所有硬件功能的 Direct3D 版本的驱动程序 DDI。 驱动程序可以支持 Direct3D 版本 11 的新线程模型仅支持的硬件上 DDI [Direct3D 版本 10 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。 Direct3D 11 版运行时确定驱动程序的最大硬件级别的支持，当运行时调用的驱动程序[ **GetCaps (D3D10\_2)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getcaps)函数和**类型**的成员[ **D3D10\_2DDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10_2ddiarg_getcaps)设置为 D3D11DDICAPS\_3DPIPELINESUPPORT。 驱动程序将返回一个指向[ **D3D11DDI\_3DPIPELINESUPPORT\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddi_3dpipelinesupport_caps)结构**pData**隶属**D3D10\_2DDIARG\_GETCAPS**标识支持的最大硬件级别。

该 API 不使用 DDI 版本作为 API 的功能级别支持; 的主要指示器该 API 允许驱动程序会反馈到此过程。 运行时选择[ **D3D11DDI\_3DPIPELINELEVEL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ne-d3d10umddi-d3d11ddi_3dpipelinelevel)值和源回值驱动程序在驱动程序的调用中的设备创建期间[ **CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数，作为的一部分**标志**的成员[ **D3D10DDIARG\_CREATEDEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)结构。

如果该驱动程序支持硬件级别上的 Direct3D 版本的 Direct3D 版本 11 小于 11 DDI，都有一些对驱动程序的操作的细微差异。 第一个是 Direct3D 版本 11 运行时可能永远不会调用许多新 Direct3D 版本 11 DDI 函数根本。 例如，Direct3D 11 版运行时不调用任何新的着色器阶段 DDI 函数 (如[ **DsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)) 如果该驱动程序支持小于 Direct3D 的硬件功能级别版本 11。 其他 DDI 函数按照功能级别的规则，并忽略这一事实，Direct3D 版本 11 DDI 可能与更高版本的功能相关联。 例如，即使 IAVertexInputSlots Direct3D 11 版 api 为 32，Direct3D 版本 10 个功能级别仅允许 16 和这就是驱动程序应该会。

已弃用或转换后的功能存在另一个有趣方面。 不推荐使用不能在 Direct3D 版本 11 DDI 级别，因为不推荐使用必须支持的功能来表达早期版本 DDI 函数。 例如，PIPELINESTATS Direct3D 11 API 版本始终是常量;但是，它会请求不同[ **D3D10\_DDI\_查询\_数据\_管道\_统计信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10_ddi_query_data_pipeline_statistics)与 Direct3D 10 功能级别和[ **D3D11\_DDI\_查询\_数据\_管道\_统计信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11_ddi_query_data_pipeline_statistics)使用 Direct3D 11 功能级别等等。 即使 API 尝试不推荐使用的文本筛选器大小，也是如此容易不推荐使用 DDI 函数的表项，其无法全部展示，而不是要尝试重新用于其他用途使用函数表条目中的驱动程序。

即使支持 11 DDI 不支持完整的 Direct3D 版本 11 功能级别的 Direct3D 版本的驱动程序，该驱动程序不能选择退出的"扩展的格式感知"，如中所述[支持扩展格式感知](supporting-extended-format-awareness.md)。 因为该驱动程序支持的 Direct3D 版本 11 DDI，该驱动程序应处理以下任务：

-   支持 BGR 格式

-   正确响应对的调用其[ **CheckFormatSupport** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkformatsupport)函数以检查 XR\_偏差的支持。 该驱动程序应声明支持或拒绝支持。

-   允许完全类型化的后台缓冲区的强制转换

Direct3D 11 版 API 还会通知驱动程序应用程序是否使用多个线程通过 D3D11DDI\_CREATEDEVICE\_标志\_SINGLETHREADED 标志。 如果此标志处在**标志**的成员[ **D3D10DDIARG\_CREATEDEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)结构时通过调用创建显示设备驱动程序的[ **CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数，该驱动程序可以确定是否会创建没有延迟的上下文，并驱动程序不需要同步，请为并发创建不这样做会出现。

 

 





