---
title: Direct3D 顶点缓冲区
description: Direct3D 顶点缓冲区
ms.assetid: b93278fc-c05f-40d4-aec1-7a90aed18ff4
keywords:
- 顶点缓冲 WDK Direct3D
- 缓冲 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f0846ca8304feda23b70a383ae88af52c8f4574
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065900"
---
# <a name="direct3d-vertex-buffers"></a>Direct3D 顶点缓冲区


## <span id="ddk_direct3d_vertex_buffers_gg"></span><span id="DDK_DIRECT3D_VERTEX_BUFFERS_GG"></span>


在对 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)的调用中，顶点缓冲区包含与命令缓冲区的基元关联的顶点数据。 顶点使用灵活的顶点格式 ([FVF](fvf--flexible-vertex-format-.md)) ，其中每个顶点都可以有与之关联的以下数据：

-    (*x、y、z 和可选 w*)  (必需的位置) 

-   漫射色 (可选) 

-   镜面颜色 (可选) 

-   纹理坐标 (可选) 。 Direct3D 最多可以发送8个 (*u，v*) 值集。

驱动程序必须提供 FVF 支持。

实际顶点和处理顺序的顺序取决于 \_ 刚从命令缓冲区分析的 D3DDP2OP*Xxx*基元命令。 有关详细信息，请参阅单独的 D3DHAL \_ DP2*Xxx* 结构参考页。

 

