---
title: 支持线程、命令列表和 3-D 管道
description: 支持线程、命令列表和 3-D 管道
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
ms.openlocfilehash: b6759a41ba70d49cd4d61b31b062a4a981f02e42
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812485"
---
# <a name="supporting-threading-command-lists-and-3-d-pipeline"></a>支持线程、命令列表和 3-D 管道

本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

用户模式显示驱动程序指示支持的新 Direct3D 版本11功能 (例如，线程处理、命令列表和三维管道) 在 Direct3D 版本11运行时调用驱动程序的 [**GetCaps (D3D10_2)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getcaps) 函数。 *GetCaps (D3D10_2)* 是驱动程序提供的特定于驱动程序的特定函数之一，驱动程序在 [**D3D10_2DDI_ADAPTERFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)结构中提供 [**pAdapterFuncs_2**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)结构的 **D3D10DDIARG_OPENADAPTER** 成员所指向的函数。 有关在驱动程序初始化期间提供特定于适配器的函数的详细信息，请参阅 [初始化与 Direct3D 版本 11 DDI 的通信](initializing-communication-with-the-direct3d-version-11-ddi.md)。 调用 **GetCaps (D3D10_2)** 函数时，用户模式显示驱动程序将基于请求类型提供新的 Direct3D 版本11功能，该请求类型是在 [**D3D10_2DDIARG_GETCAPS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddiarg_getcaps)结构的 **type** 成员中指定的 (， *GetCaps (* D3D10_2 函数的 *pData* 参数指向) 。

## <a name="threading-and-command-lists"></a>线程和命令列表

Direct3D 版本 11 API 需要一种操作模式，在该模式下，它可以同步应用程序线程，以确保每次只有一个线程在 DDI 中运行。 Direct3D 版本 11 API 还需要一种操作模式，其中包含命令列表的软件模拟。 这种操作模式是必需的，并在以前版本的 DDIs (（例如，Direct3D 版本 10 DDI) ）上使用。 因此，作为驱动程序编写者的开发帮助，这些相同的操作模式将扩展到 Direct3D 版本 11 DDI 上。 驱动程序编写器可以决定它们要为 Direct3D 版本 11 DDI 支持的操作模式。

所有驱动程序都应最终完全支持所有类型的线程操作 (即，所有驱动程序最终都应支持 [**D3D11DDI_THREADING_CAPS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_threading_caps) 结构) 的所有线程功能。 但是，驱动程序可能要求 API 模拟命令列出或强制执行针对驱动程序的单线程操作模式。 API 在创建 API 设备期间，但在创建 DDI 设备之前，必须注意驱动程序的线程处理功能。 因此，当调用驱动程序的 (GetCaps 时，运行时将确定驱动程序的线程处理功能， [**D3D10_2)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getcaps)将 [**D3D10_2DDIARG_GETCAPS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddiarg_getcaps)设置为 D3D11DDICAPS_THREADING 的 **类型** 成员的特定于适配器的函数。 驱动程序将返回一个指针，该指针指向用于标识驱动程序线程功能的 D3D10_2DDIARG_GETCAPS 的 **pData** 成员中的 **D3D11DDI_THREADING_CAPS** 结构。 驱动程序必须支持自由线程模式 (D3D11DDICAPS_FREETHREADED) 如果驱动程序还支持 D3D11DDICAPS_COMMANDLISTS_BUILD_2) 中的命令 (列表，因为命令列出了在自由线程模式下生成。 驱动程序必须选择支持自由线程模式和命令列表。 应用程序可以通过使用应用程序级别的 **CheckFeatureSupport** 函数和 D3D11_FEATURE_THREADING 常数来确定驱动程序所指示的支持;但是，某些应用程序可能不会考虑 API 提供的支持。

## <a name="3-d-pipeline-level"></a>三维管道级别

支持 Direct3D 版本 11 DDI 的驱动程序无需支持 Direct3D 版本 11 DDI 的所有硬件功能。 驱动程序可以支持仅支持 Direct3D 版本 10 DDI 的基于硬件的 Direct3D 版本 11 DDI 的新线程模型。 当运行时调用驱动程序的 [**GetCaps (D3D10_2)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getcaps) 函数的 **类型** [**D3D10_2DDIARG_GETCAPS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddiarg_getcaps) 成员设置为 D3D11DDICAPS_3DPIPELINESUPPORT 时，Direct3D 版本11运行时将确定驱动程序的最高硬件支持级别。 驱动程序将返回一个指针，该指针指向用于标识支持的最高硬件级别的 **D3D10_2DDIARG_GETCAPS** 的 **pData** 成员中的 [**D3D11DDI_3DPIPELINESUPPORT_CAPS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_3dpipelinesupport_caps)结构。

API 不只使用 DDI 版本作为 API 功能级别支持的主要指标;该 API 允许驱动程序回送到此进程。 在设备创建期间，运行时将选择一个 [**D3D11DDI_3DPIPELINELEVEL**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11ddi_3dpipelinelevel)值并将该值回送到驱动程序，同时调用驱动程序的 [**CreateDevice (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数作为 [**D3D10DDIARG_CREATEDEVICE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)结构的 **Flags** 成员的一部分。

如果驱动程序在 Direct3D 版本 11 DDI 上支持的硬件级别低于 Direct3D 版本11，则驱动程序的操作将有很大的影响。 第一种情况是，Direct3D 版本11运行时根本不会调用许多新的 Direct3D 版本 11 DDI 函数。 例如，如果驱动程序支持的硬件功能级别低于 Direct3D 版本11，Direct3D 版本11运行时将不会调用任何新的着色器分段 DDI 函数 (例如 [**DsSetShader**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)) 。 其他 DDI 函数遵循功能级别的规则，并忽略 Direct3D 版本 11 DDI 可能与更高的功能关联的事实。 例如，尽管 Direct3D 版本 11 API 的 IAVertexInputSlots 是32，但 Direct3D 版本10功能级别仅允许16，这是驱动程序应该会出现的情况。

不推荐使用或已转换的功能提供另一个有趣的方面。 不能在 Direct3D 版本 11 DDI 级别上弃用，因为弃用必须支持能够表达早期版本 DDI 函数。 例如，PIPELINESTATS 的 Direct3D 11 API 版本始终是常量;但是，它会向 direct3d 10 功能级别请求不同的 [**D3D10_DDI_QUERY_DATA_PIPELINE_STATISTICS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_ddi_query_data_pipeline_statistics) ，并 [**D3D11_DDI_QUERY_DATA_PIPELINE_STATISTICS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_ddi_query_data_pipeline_statistics) direct3d 11 功能级别，等等。 即使 API 试图弃用文本筛选器大小，驱动程序也更容易弃用 DDI 函数表项，而不是尝试重复使用函数表项来执行其他操作。

即使支持 Direct3D 版本 11 DDI 的驱动程序不支持完整的 Direct3D 版本11功能级别，驱动程序也无法选择退出 "扩展格式识别"，如 [支持扩展格式识别](supporting-extended-format-awareness.md)中所述。 由于驱动程序支持 Direct3D 版本 11 DDI，驱动程序应处理以下任务：

* 支持 BGR 格式

* 正确响应对其 [**CheckFormatSupport**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkformatsupport) 函数的调用以检查 XR_BIAS 支持。 驱动程序应声明支持或拒绝支持。

* 允许强制转换完全类型的后台缓冲区

Direct3D 版本 11 API 还会通过 D3D11DDI_CREATEDEVICE_FLAG_SINGLETHREADED 标志通知驱动程序应用程序是否使用多个线程。 如果在通过调用驱动程序的 [**CREATEDEVICE (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数创建显示设备时，在 [**D3D10DDIARG_CREATEDEVICE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)结构的 **Flags** 成员中存在此标志，则驱动程序可以确定不创建延迟的上下文并且不需要驱动程序进行同步，因为并发创建不会出现。
