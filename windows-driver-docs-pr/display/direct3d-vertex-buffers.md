---
title: Direct3D 顶点缓冲区
description: Direct3D 顶点缓冲区
keywords:
- 顶点缓冲 WDK Direct3D
- 缓冲 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8a9beebd801bf901866c23e03dac4fb1df0ce5b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809415"
---
# <a name="direct3d-vertex-buffers"></a>Direct3D 顶点缓冲区


## <span id="ddk_direct3d_vertex_buffers_gg"></span><span id="DDK_DIRECT3D_VERTEX_BUFFERS_GG"></span>


在对 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)的调用中，顶点缓冲区包含与命令缓冲区的基元关联的顶点数据。 顶点使用灵活的顶点格式 ([FVF](fvf--flexible-vertex-format-.md)) ，其中每个顶点都可以有与之关联的以下数据：

-    (*x、y、z 和可选 w*)  (必需的位置) 

-   漫射色 (可选) 

-   镜面颜色 (可选) 

-   纹理坐标 (可选) 。 Direct3D 最多可以发送8个 (*u，v*) 值集。

驱动程序必须提供 FVF 支持。

实际顶点和处理顺序的顺序取决于 \_ 刚从命令缓冲区分析的 D3DDP2OP *Xxx* 基元命令。 有关详细信息，请参阅单独的 D3DHAL \_ DP2 *Xxx* 结构参考页。

 

