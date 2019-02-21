---
title: 多个顶点流
description: 多个顶点流
ms.assetid: aaaea27b-79e0-4c48-9102-898b42a1487f
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多个顶点流
- 多个顶点流式传输 WDK DirectX 8.0
- 顶点多个流 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd942a1d9b9f154807319484fdd6f5bd16fdc3e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556218"
---
# <a name="multiple-vertex-streams"></a>多个顶点流


## <span id="ddk_multiple_vertex_streams_gg"></span><span id="DDK_MULTIPLE_VERTEX_STREAMS_GG"></span>


DirectX 8.0 添加了对多个顶点流支持。 即使驱动程序和硬件组合不支持多个流的顶点数据，该驱动程序仍必须处理绑定 DP2 令牌流 (D3DDP2OP\_SETSTREAMSOURCE 和 D3DDP2OP\_SETSTREAMSOURCEUM) 和新的基于 DP2 绘制令牌顶点流 (请参阅[新 DP2 Stream 绘制令牌](new-dp2-stream-drawing-tokens.md))。 这些是用于将顶点数据传递到绘制的 DirectX 8.0 级别驱动程序中的驱动程序的机制。

 

 





