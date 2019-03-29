---
title: 在 DP2 流中复制顶点和索引缓冲区
description: 在 DP2 流中复制顶点和索引缓冲区
ms.assetid: 5181e299-4beb-448c-bf11-be9bb5575af1
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，DP2 绘制令牌
- DP2 绘图令牌 WDK DirectX 8.0
- 绘制令牌 WDK DirectX 8.0
- 令牌 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 825138c82c713f1f8b661aa7bb77513a0e15642e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567478"
---
# <a name="copying-vertex-and-index-buffers-in-the-dp2-stream"></a>在 DP2 流中复制顶点和索引缓冲区


## <span id="ddk_copying_vertex_and_index_buffers_in_the_dp2_stream_gg"></span><span id="DDK_COPYING_VERTEX_AND_INDEX_BUFFERS_IN_THE_DP2_STREAM_GG"></span>


新的 DP2 令牌 D3DDP2OP\_添加了 BUFFERBLT，以获得最佳的复制和更新的索引和顶点缓冲区。 此令牌是非常类似于现有 D3DDP2OP\_TEXBLT 的复制和更新纹理但已被修改以支持 subbuffer 复制而不简单的矩形。

 

 





