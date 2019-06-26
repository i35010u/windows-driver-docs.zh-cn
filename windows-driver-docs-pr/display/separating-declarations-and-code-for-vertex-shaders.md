---
title: 隔离顶点着色器的声明和代码
description: 隔离顶点着色器的声明和代码
ms.assetid: 6da26a8f-553b-4995-9dda-66a7fd6d478b
keywords:
- 顶点着色器声明 WDK DirectX 9.0 中，分隔声明和代码
- 着色器声明 WDK DirectX 9.0 中，分隔声明和代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cab90b544ddc22027cbe093749e5fa52f6cf4d5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365583"
---
# <a name="separating-declarations-and-code-for-vertex-shaders"></a>隔离顶点着色器的声明和代码


## <span id="ddk_separating_declarations_and_code_for_vertex_shaders_gg"></span><span id="DDK_SEPARATING_DECLARATIONS_AND_CODE_FOR_VERTEX_SHADERS_GG"></span>


在 DirectX 9.0 中声明和顶点着色器代码不能再绑定在一起时创建顶点着色器。 支持顶点着色器的设备的 DirectX 9.0 版本驱动程序必须处理单独创建和管理声明和代码的对象。 但是，此 DirectX 9.0 驱动程序必须仍将能够管理结合了声明和代码，因为 DirectX 8.0 运行时可能会请求来创建此类顶点着色器对象的顶点着色器对象。 有关详细信息，请参阅[顶点着色器](vertex-shaders.md)。

DirectX 9.0 运行时将从单独的句柄池句柄分配给声明和代码对象。 DirectX 9.0 驱动程序必须将这些句柄存储在单独的数组中。 顶点着色器处理 DirectX 8.0 中的空间，如 DirectX 9.0 与灵活顶点格式 (FVF) 代码共享顶点着色器声明句柄空间。 设置句柄的位零指示顶点着色器声明，否则 FVF 代码。 有关详细信息，请参阅参考光栅器 (*refrast.cpp*示例代码)。

DirectX 9.0 驱动程序收到的顶点着色器声明时它可以处理 D3DDP2OP\_CREATEVERTEXSHADERDECL 操作代码中其[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数。 一个[ **D3DHAL\_DP2CREATEVERTEXSHADERDECL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2createvertexshaderdecl)结构和数组用于定义构成着色器声明的顶点元素 D3DVERTEXELEMENT9 结构遵循该操作中的代码[命令流](command-stream.md)。 如果在执行 DirectX 9.0 驱动程序来处理顶点着色器声明的元素，它必须支持所有可能的顶点数据使用。 也就是说，它必须为这些类型支持所有 D3DDECLUSAGE 类型，以及多个含义 （使用索引值）。 有关 D3DVERTEXELEMENT9 和 D3DDECLUSAGE 的详细信息，请参阅最新的 DirectX SDK 文档。

DirectX 9.0 驱动程序收到的顶点着色器代码时它可以处理 D3DDP2OP\_CREATEVERTEXSHADERFUNC 操作代码。 一个[ **D3DHAL\_DP2CREATEVERTEXSHADERFUNC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2createvertexshaderfunc)结构和顶点着色器代码遵循命令流中的操作代码。 单个着色器代码和构成每个着色器代码的令牌的格式的详细信息，请参阅[Direct3D 驱动程序着色器代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

DirectX 9.0 驱动程序处理 D3DDP2OP\_SETVERTEXSHADERDECL 和 D3DDP2OP\_SETVERTEXSHADERFUNC 操作代码，以使特定顶点着色器声明和代码当前顶点着色器组装器中。 该驱动程序处理 D3DDP2OP\_DELETEVERTEXSHADERDECL 和 D3DDP2OP\_DELETEVERTEXSHADERFUNC 操作代码从顶点着色器组装器中删除这些顶点着色器声明和代码。 为每个这些操作代码， [ **D3DHAL\_DP2VERTEXSHADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2vertexshader)结构后面的命令流。 此结构包含一个用于标识的句柄的声明或代码来设置或删除的成员。

 

 





