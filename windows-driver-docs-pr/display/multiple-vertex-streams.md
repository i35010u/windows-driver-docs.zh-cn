---
title: 多个顶点流
description: 多个顶点流
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多个顶点流
- 多个顶点流 WDK DirectX 8。0
- 顶点多流 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 688da9b597c5f90c29bdf84260b28de1d1b38e97
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840383"
---
# <a name="multiple-vertex-streams"></a>多个顶点流


## <span id="ddk_multiple_vertex_streams_gg"></span><span id="DDK_MULTIPLE_VERTEX_STREAMS_GG"></span>


DirectX 8.0 添加了对多个顶点流的支持。 即使驱动程序和硬件组合不支持多个顶点数据流，驱动程序仍必须处理流绑定 DP2 标记 (D3DDP2OP \_ SETSTREAMSOURCE 和 D3DDP2OP \_ SETSTREAMSOURCEUM) ，以及基于新的顶点流 DP2 绘图标记 (请参阅) 的 [新 DP2 流绘图标记](new-dp2-stream-drawing-tokens.md) 。 这些是将顶点数据传递到用于 DirectX 8.0 级别驱动程序的绘图中的驱动程序的机制。

 

 





