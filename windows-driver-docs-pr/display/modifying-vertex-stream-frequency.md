---
title: 修改顶点流频率
description: 修改顶点流频率
ms.assetid: 81bbced4-7331-4e54-9617-1ef29b02f162
keywords:
- 顶点流 9.0 frequency
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9cbd8e7ebbe455ca971559246bc4d839d6da50c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840561"
---
# <a name="modifying-vertex-stream-frequency"></a>修改顶点流频率


## <span id="ddk_modifying_vertex_stream_frequency_gg"></span><span id="DDK_MODIFYING_VERTEX_STREAM_FREQUENCY_GG"></span>


支持顶点着色器版本3.0 及更高版本的设备的 DirectX 9.0 版本驱动程序必须实现顶点流频率除法。 对于2.0 版和更早型号的顶点着色器（包括 fixed 函数），将每个顶点调用一次顶点着色器;对于每个调用，将用顶点流中的唯一顶点元素初始化输入顶点寄存器。 但是，使用顶点流的频率除法，可以调用顶点着色器（3.0 和更高版本）来以较低的频率初始化适用的输入寄存器。

当应用程序调用**IDirect3DDevice9：： SetStreamSourceFreq**方法来设置给定流的频率时，DirectX 9.0 运行时转而使用 D3DDP2OP 调用驱动程序的[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数\_SETSTREAMSOURCEFREQ 操作代码。

设置流的 frequency 约数后（例如，转换为2），驱动程序必须从流中提取数据，并将此数据传递到适用的输入顶点每2顶点注册一次。 此约数会影响流中的每个元素。

驱动程序使用此约数根据以下公式将顶点偏移量计算到顶点缓冲区：

```cpp
VertexOffset = VertexIndex / Divider * StreamStride + StreamOffset 
```

对于使用的每个顶点流，如果在使用 D3DDP2OP\_DRAWPRIMITIVE 操作代码调用驱动程序的*D3dDrawPrimitives2*函数时，驱动程序收到一个起始顶点值，则驱动程序还会将此起始顶点值除以frequency 除数和因素是公式中的结果。 此起始顶点值在[**D3DHAL\_DP2DRAWPRIMITIVE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2drawprimitive)结构的**VStart**成员中提供。 起始顶点值中的以下公式系数：

```cpp
VertexOffset = StartVertex / Divider + 
               VertexIndex / Divider * StreamStride + StreamOffset 
```

请注意，前面的公式使用整数除法。

应用程序通过对**IDirect3DDevice9：： CreateStateBlock**方法的调用传递 D3DSBT\_VERTEXSTATE 状态类型来捕获当前顶点状态。

对于索引基元，或如果驱动程序仅支持早于版本3.0 （包括 fixed 函数）的顶点着色器模型，则驱动程序将忽略流的 frequency 因数设置。

有关**IDirect3DDevice*xxx*：： SetStreamSourceFreq**和**IDirect3DDevice*Xxx*：： CreateStateBlock**的详细信息，请参阅最新的 DirectX SDK 文档。

 

 





