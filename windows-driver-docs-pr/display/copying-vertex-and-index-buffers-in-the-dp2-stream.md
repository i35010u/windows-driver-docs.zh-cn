---
title: 在 DP2 流中复制顶点和索引缓冲区
description: 在 DP2 流中复制顶点和索引缓冲区
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，DP2 绘图标记
- DP2 绘制令牌 WDK DirectX 8。0
- 绘制令牌 WDK DirectX 8。0
- 令牌 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79e783e259af1f5f8a02a572b3f4d1de31cf22f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832803"
---
# <a name="copying-vertex-and-index-buffers-in-the-dp2-stream"></a>在 DP2 流中复制顶点和索引缓冲区


## <span id="ddk_copying_vertex_and_index_buffers_in_the_dp2_stream_gg"></span><span id="DDK_COPYING_VERTEX_AND_INDEX_BUFFERS_IN_THE_DP2_STREAM_GG"></span>


添加了新的 DP2 令牌 D3DDP2OP \_ BUFFERBLT，以支持索引和顶点缓冲区的最佳复制和更新。 此令牌非常类似于现有的 D3DDP2OP \_ TEXBLT，它复制和更新纹理，但已修改为支持 subbuffer 复制，而不是简单的矩形。

 

 





