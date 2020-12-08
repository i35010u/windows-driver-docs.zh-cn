---
title: 命令和顶点缓冲区
description: 命令和顶点缓冲区
keywords:
- 命令缓冲区 WDK Direct3D
- 顶点缓冲 WDK Direct3D
- 缓冲 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f15ebdfc13e9fee257fff6da0652f63f47942d6f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810255"
---
# <a name="command-and-vertex-buffers"></a>命令和顶点缓冲区


## <span id="ddk_command_and_vertex_buffers_gg"></span><span id="DDK_COMMAND_AND_VERTEX_BUFFERS_GG"></span>


[**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) DDI 使用两种类型的缓冲区：命令缓冲区和顶点缓冲区。 命令缓冲区包含后跟与执行缓冲区类似的结构中数据的指令。 命令缓冲区可能包含索引和非索引基元，有时还包含内联顶点数据。 命令缓冲区可以是 API 级别的执行缓冲区，也可以是 Direct3D 内部命令缓冲区。 有关主输入结构的说明，请参阅 [**D3DHAL \_ DRAWPRIMITIVES2DATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)。

对于内部命令缓冲区，驱动程序会分配内存，并可能 multibuffering。 内部命令缓冲区是只写的。 可在 [**D3DHAL \_ DP2COMMAND**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command)中查看指令格式。

如果设置了 D3DHALDP2 \_ USERMEMVERTICES 标志，则由用户内存指针指定顶点缓冲区。 否则，顶点缓冲区为 DirectDrawSurface，可以是 API 级别的执行缓冲区、内部隐式顶点缓冲区或 API 级别的顶点缓冲区。

顶点缓冲区 API 可以创建、销毁、锁定和解锁顶点缓冲区，并且可以使用 **IDirect3DVertexBuffer7：:P rocessvertices** 方法处理从源到目标缓冲区的顶点。 **IDirect3DDevice7：:D rawprimitivevb** 和 **IDirect3DDevice7：:D rawindexedprimitivevb** 方法是主要的 API 级别调用。 还可以优化顶点缓冲区，但不能锁定优化的顶点缓冲区。 有关这三种方法的说明，请参阅 Direct3D SDK 文档。

 

