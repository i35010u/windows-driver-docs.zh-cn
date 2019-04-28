---
title: 新的 DP2 流绘图标记
description: 新的 DP2 流绘图标记
ms.assetid: 09f3e5a4-60ed-4649-a30b-de4b320a54de
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，DP2 绘制令牌
- DP2 绘图令牌 WDK DirectX 8.0
- 绘制令牌 WDK DirectX 8.0
- 令牌 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79321adf0c18f6dafbc7fc7a252502bfe9fe32bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345542"
---
# <a name="new-dp2-stream-drawing-tokens"></a>新的 DP2 流绘图标记


## <span id="ddk_new_dp2_stream_drawing_tokens_gg"></span><span id="DDK_NEW_DP2_STREAM_DRAWING_TOKENS_GG"></span>


顶点数据的多个流的 DirectX 8.0 的支持需要引入新 DP2 绘制标记。 这些新的令牌是必需的因为现有绘制令牌假定没有指向特定的绘制指令的顶点数据的单个指针。 与多个流，这是不能再用例。 绘制命令可能也访问多个顶点数据缓冲区同时通过流。

请注意这些绘制令牌替换现有的基元类型特定的令牌 (例如，D3DDP2OP\_点、 D3DDP2OP\_TRIANGLELIST、 D3DDP2OP\_TRIANGLESTRIP) 的调用通过新的 DirectX 8.0 接口仅。 通过 DX7 或更早的接口进行的调用仍通过传递 DDI 作为旧样式绘制标记。 因此，DX8 驱动程序时需要支持旧的和新样式绘制的令牌。

索引和非索引绘制标记有两个不同版本。 例如，非索引绘图通过令牌 D3DDP2OP\_DRAWPRIMITIVE 和 D3DDP2OP\_DRAWPRIMITIVE2。 同样，索引的绘图通过令牌 D3DDP2OP\_DRAWINDEXEDPRIMITIVE 和 D3DDP2OP\_DRAWINDEXEDPRIMITIVE2。

两种变体之间的主要区别在于该 D3DDP2OP\_DRAWPRIMITIVE2 和 D3DDP2OP\_DRAWINDEXEDPRIMITIVE2 时已转换的顶点数据由运行时使用。 这是要么因为驱动程序/硬件组合不支持硬件顶点处理或软件顶点处理具有已明确选择。 有关这些令牌中，使用仅流零，其中包含已转换和亮起顶点。

D3DDP2OP\_DRAWPRIMITIVE 和 D3DDP2OP\_DRAWINDEXEDPRIMITIVE 使用，则运行时未处理的顶点数据。 因此，这些令牌可以提供未经转换的顶点数据，如果硬件支持硬件顶点处理或转换后的顶点数据时应用程序提供直接向运行时转换的数据。 在此情况下，任意数量的流 (最多**MaxStreams**) 可处于活动状态。 这些变体 (以及其他新绘图的令牌，D3DDP2OP\_CLIPPEDTRIANGLEFAN) 启用运行时中的最优性能的代码路径和此处所述的之外的差别不大向驱动程序。

 

 





