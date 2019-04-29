---
title: Direct3D 顶点缓冲区
description: Direct3D 顶点缓冲区
ms.assetid: b93278fc-c05f-40d4-aec1-7a90aed18ff4
keywords:
- 顶点缓冲区 WDK Direct3D
- WDK Direct3D 缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e2d924a3bfcafabe0c15f9294a814012af08d8d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357961"
---
# <a name="direct3d-vertex-buffers"></a>Direct3D 顶点缓冲区


## <span id="ddk_direct3d_vertex_buffers_gg"></span><span id="DDK_DIRECT3D_VERTEX_BUFFERS_GG"></span>


顶点缓冲区中包含对的调用中的命令缓冲区的基元与关联的顶点数据[ **D3dDrawPrimitives2**](https://msdn.microsoft.com/library/windows/hardware/ff544704)。 使用灵活的顶点格式表示顶点 ([FVF](fvf--flexible-vertex-format-.md))，其中每个顶点可以具有与之关联的以下数据：

-   位置 (*x、 y、 z 和 w 可选*) （必需）

-   （可选） 的漫射颜色

-   （可选） 的反射颜色

-   （可选） 的纹理坐标。 Direct3D 可以向上发送到最大的八组 (*u、 v*) 值。

驱动程序必须提供 FVF 支持。

实际的顶点和应处理的顺序取决于 D3DDP2OP\_*Xxx*基元命令只是通过分析得到的命令缓冲区。 有关详细信息，请参阅各个 D3DHAL\_DP2*Xxx*结构参考页。

 

 





