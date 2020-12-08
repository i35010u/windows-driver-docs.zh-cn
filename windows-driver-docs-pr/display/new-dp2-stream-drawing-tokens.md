---
title: 新的 DP2 流绘图标记
description: 新的 DP2 流绘图标记
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，DP2 绘图标记
- DP2 绘制令牌 WDK DirectX 8。0
- 绘制令牌 WDK DirectX 8。0
- 令牌 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7535c09793fb67dd5025d6013a26815df35ee44e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840373"
---
# <a name="new-dp2-stream-drawing-tokens"></a>新的 DP2 流绘图标记


## <span id="ddk_new_dp2_stream_drawing_tokens_gg"></span><span id="DDK_NEW_DP2_STREAM_DRAWING_TOKENS_GG"></span>


DirectX 8.0 支持多个顶点数据流需要引入新的 DP2 绘图标记。 这些新标记是必需的，因为现有的绘图标记假设有一个指向特定绘图指令的顶点数据的指针。 如果有多个流，就不再出现这种情况。 绘图命令可通过流同时访问多个顶点数据缓冲区。

请注意，这些绘图标记会将现有的基元类型特定标记替换 (例如 D3DDP2OP \_ 点、D3DDP2OP \_ TRIANGLELIST、D3DDP2OP \_ TRIANGLESTRIP) ，以便仅通过新的 DirectX 8.0 接口调用。 通过 DX7 或更低版本的接口发出的调用仍将作为旧的样式绘制标记通过 DDI 传递。 因此，需要使用 DX8 驱动程序来支持新旧样式绘制标记。

索引和非索引的绘图标记有两个变体。 例如，非索引绘图由标记 D3DDP2OP \_ DRAWPRIMITIVE 和 D3DDP2OP \_ DRAWPRIMITIVE2 完成。 同样，索引绘制是通过标记 D3DDP2OP \_ DRAWINDEXEDPRIMITIVE 和 D3DDP2OP DRAWINDEXEDPRIMITIVE2 来完成的 \_ 。

这两个变体之间的主要区别是，在 \_ \_ 运行时转换顶点数据时，将使用 D3DDP2OP DRAWPRIMITIVE2 和 D3DDP2OP DRAWINDEXEDPRIMITIVE2。 这是因为驱动程序/硬件组合不支持硬件顶点处理，也可能是已明确选择了软件顶点处理。 对于这些标记，只使用流零，其中包含转换后的顶点。

\_使用 D3DDP2OP DRAWPRIMITIVE 和 D3DDP2OP \_ DRAWINDEXEDPRIMITIVE，则运行时尚未处理顶点数据。 因此，当应用程序将转换的数据直接提供给运行时时，这些标记可以提供未经转换顶点数据（当硬件支持硬件顶点处理或转换的顶点数据时）。 在这种情况下，任意数量的流 (多达 **MaxStreams**) 可以处于活动状态。 这些变体与其他新的绘图标记 (一起使用，D3DDP2OP \_ CLIPPEDTRIANGLEFAN) 在运行时中启用最佳代码路径，在此过程中所述的区别超出了此驱动程序。

 

 





