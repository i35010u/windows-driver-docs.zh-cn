---
title: 修改顶点 Stream 频率
description: 修改顶点 Stream 频率
ms.assetid: 81bbced4-7331-4e54-9617-1ef29b02f162
keywords:
- 顶点流频率除法 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f4b47bde0db39b6f7f8384abe1e4f86daa644fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546448"
---
# <a name="modifying-vertex-stream-frequency"></a>修改顶点 Stream 频率


## <span id="ddk_modifying_vertex_stream_frequency_gg"></span><span id="DDK_MODIFYING_VERTEX_STREAM_FREQUENCY_GG"></span>


支持顶点着色器版本 3.0 及更高版本的设备的 DirectX 9.0 版本驱动程序必须实现顶点流频率除法。 对于版本 2.0 和顶点着色器 （包括固定的函数） 的较旧型号，顶点着色器调用一次每顶点;对于每个调用中，输入的顶点寄存器使用顶点流中的唯一顶点元素进行初始化。 但是，使用顶点流频率除法，顶点着色器 （3.0 版及更高版本） 可以调用以初始化频率较低的费率适用输入的寄存器。

当应用程序调用**IDirect3DDevice9::SetStreamSourceFreq**方法来设置用于给定的流，DirectX 9.0 运行时的频率反过来调用驱动程序的[ **D3dDrawPrimitives2**](https://msdn.microsoft.com/library/windows/hardware/ff544704)函数使用 D3DDP2OP\_SETSTREAMSOURCEFREQ 操作代码。

在流的频率后除数设置-例如，为 2，则驱动程序必须从流中提取数据并将此数据传递到适用的输入的顶点寄存器每 2 个顶点。 此除数影响流中的每个元素。

驱动程序使用此除数到顶点缓冲区根据以下公式计算的顶点偏移量：

```cpp
VertexOffset = VertexIndex / Divider * StreamStride + StreamOffset 
```

如果该驱动程序的驱动程序的调用过程中接收开始顶点值中使用的每个顶点流*D3dDrawPrimitives2*函数使用 D3DDP2OP\_DRAWPRIMITIVE 操作代码，该驱动程序还将这频率除数开始顶点值以及因素中公式的结果。 中提供该值开始顶点**VStart**的成员[ **D3DHAL\_DP2DRAWPRIMITIVE** ](https://msdn.microsoft.com/library/windows/hardware/ff545526)结构。 下面的公式中开始顶点值因素：

```cpp
VertexOffset = StartVertex / Divider + 
               VertexIndex / Divider * StreamStride + StreamOffset 
```

请注意上述公式使用整数除法。

应用程序传递 D3DSBT\_VERTEXSTATE 状态类型中调用**IDirect3DDevice9::CreateStateBlock**方法来捕获当前的顶点状态。

该驱动程序将忽略流的频率除数为索引的基元或如果该驱动程序仅支持早于版本 3.0 （包括固定函数） 的顶点着色器模型的设置。

有关详细信息**IDirect3DDevice*Xxx*:: SetStreamSourceFreq**并**IDirect3DDevice*Xxx*:: CreateStateBlock**，请参阅最新的 DirectX SDK 文档。

 

 





