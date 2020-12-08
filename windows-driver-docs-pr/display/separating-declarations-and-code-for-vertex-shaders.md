---
title: 隔离顶点着色器的声明和代码
description: 隔离顶点着色器的声明和代码
keywords:
- 顶点着色器声明 WDK DirectX 9.0，分隔声明和代码
- 着色器声明 WDK DirectX 9.0，分隔声明和代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d418d8e0e6ac5ce00907b98e489f8f72055a9ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816811"
---
# <a name="separating-declarations-and-code-for-vertex-shaders"></a>隔离顶点着色器的声明和代码


## <span id="ddk_separating_declarations_and_code_for_vertex_shaders_gg"></span><span id="DDK_SEPARATING_DECLARATIONS_AND_CODE_FOR_VERTEX_SHADERS_GG"></span>


在 DirectX 9.0 中，创建顶点着色器后，顶点着色器的声明和代码将不再绑定在一起。 支持顶点着色器的设备的 DirectX 9.0 版本驱动程序必须处理声明和代码对象的单独创建和管理。 但是，此 DirectX 9.0 驱动程序仍必须能够管理同时组合声明和代码的顶点着色器对象，因为 DirectX 8.0 运行时可能会请求创建这种顶点着色器对象。 有关详细信息，请参阅 [顶点着色](vertex-shaders.md)器。

DirectX 9.0 运行时将句柄从单独的句柄池分配到声明和代码对象。 DirectX 9.0 驱动程序必须在单独的数组中存储这些句柄。 与顶点着色器一样，在 DirectX 8.0 中处理空间，DirectX 9.0 共享顶点着色器声明以灵活的顶点格式处理空间， (FVF) 代码。 设置句柄的位零指示顶点着色器声明，否则为 FVF 代码。 有关详细信息，请参阅参考光栅化 (*refrast* 示例代码) 。

DirectX 9.0 驱动程序在处理 \_ 其 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 函数中的 D3DDP2OP CREATEVERTEXSHADERDECL 操作代码时接收顶点着色器声明。 [**D3DHAL \_ DP2CREATEVERTEXSHADERDECL**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2createvertexshaderdecl)结构和 D3DVERTEXELEMENT9 结构的数组，这些结构定义组成着色器声明的顶点元素遵循 [命令流](command-stream.md)中的操作代码。 如果实现了 DirectX 9.0 驱动程序来处理着色器声明的顶点元素，则它必须支持顶点数据的所有可能用途。 也就是说，它必须支持所有 D3DDECLUSAGE 类型以及这些类型)  (用法索引值。 有关 D3DVERTEXELEMENT9 和 D3DDECLUSAGE 的详细信息，请参阅最新的 DirectX SDK 文档。

DirectX 9.0 驱动程序在处理 D3DDP2OP CREATEVERTEXSHADERFUNC 操作代码时接收顶点着色器代码 \_ 。 [**D3DHAL \_ DP2CREATEVERTEXSHADERFUNC**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2createvertexshaderfunc)结构和顶点着色器代码遵循命令流中的操作代码。 有关各个着色器代码的格式和组成每个着色器代码的标记的详细信息，请参阅 [Direct3D 驱动程序着色器代码](/windows-hardware/drivers/ddi/index)。

DirectX 9.0 驱动程序处理 D3DDP2OP \_ SETVERTEXSHADERDECL 和 D3DDP2OP \_ SETVERTEXSHADERFUNC 操作代码，以使顶点着色器组装器中的特定顶点着色器声明和代码成为最新的。 驱动程序处理 D3DDP2OP \_ DELETEVERTEXSHADERDECL 和 D3DDP2OP \_ DELETEVERTEXSHADERFUNC 操作代码，以从顶点着色器组装器中删除这些顶点着色器声明和代码。 对于这些操作代码中的每个，命令流中 [**D3DHAL 的 \_ DP2VERTEXSHADER**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2vertexshader) 结构。 此结构只包含一个成员，用于标识要设置或删除的声明或代码的句柄。

 

