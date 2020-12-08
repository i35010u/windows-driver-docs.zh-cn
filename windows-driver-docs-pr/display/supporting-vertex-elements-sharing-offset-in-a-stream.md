---
title: 支持流中具有相同偏移量的顶点元素
description: 支持流中具有相同偏移量的顶点元素
keywords:
- 顶点着色器声明 WDK DirectX 9.0，共享流中的偏移量
- 着色器声明 WDK DirectX 9.0，共享流中的偏移量
- 顶点流偏移 WDK DirectX 9。0
- 顶点流偏移 WDK DirectX 9.0，顶点着色器声明
- 流偏移 WDK DirectX 9。0
- 流偏移 WDK DirectX 9.0，顶点着色器声明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d774ccdec02374590ec880f23effd586dbc5441
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838967"
---
# <a name="supporting-vertex-elements-sharing-offset-in-a-stream"></a>支持流中具有相同偏移量的顶点元素


## <span id="ddk_supporting_vertex_elements_sharing_offset_in_a_stream_gg"></span><span id="DDK_SUPPORTING_VERTEX_ELEMENTS_SHARING_OFFSET_IN_A_STREAM_GG"></span>


DirectX 9.0 版本驱动程序指示其设备允许多个顶点元素通过设置 \_ D3DCAPS9 结构的 **DevCaps2** 成员中的 D3DDEVCAPS2 VERTEXELEMENTSCANSHARESTREAMOFFSET 功能位，在流中共享同一偏移量。 顶点着色器声明包含一个顶点元素数组。 有关详细信息，请参阅 [分隔顶点着色器的声明和代码](separating-declarations-and-code-for-vertex-shaders.md)。

如果支持像素着色器 (PS) 版本低于3.0 的 DirectX 9.0 驱动程序将设置 D3DDEVCAPS2 \_ VERTEXELEMENTSCANSHARESTREAMOFFSET，则驱动程序可以使用指定 D3DDECLUSAGE \_ POSITIONT (0) 使用类型的元素处理大多数顶点声明。 此前 PS 3.0 驱动程序将 D3DDECLUSAGE \_ POSITIONT (0) 的顶点声明转换为有效的灵活顶点格式 (FVF) 。 但是，如果声明在纹理坐标中存在间隙，则此预 PS 3.0 驱动程序无法使用指定 D3DDECLUSAGE \_ POSITIONT (0) 用法类型的元素处理顶点声明。 例如，此预 PS 3.0 驱动程序无法处理以下顶点声明：

```cpp
{0,0,D3DDECLTYPE_FLOAT4, D3DDECLMETHOD_DEFAULT, D3DDECLUSAGE_POSITIONT, 0}
{0,16,D3DDECLTYPE_FLOAT2, D3DDECLMETHOD_DEFAULT, D3DDECLUSAGE_TEXCOORD, 0}
{0,24,D3DDECLTYPE_FLOAT2, D3DDECLMETHOD_DEFAULT, D3DDECLUSAGE_TEXCOORD, 5}
```

因为纹理坐标存在间隙，所以此预 PS 3.0 驱动程序无法 \_ 使用 FVF 表示 D3DDECLUSAGE TEXCOORD 元素。

如果支持像素着色器3.0 和更高版本的设备的 DirectX 9.0 驱动程序设置 D3DDEVCAPS2 \_ VERTEXELEMENTSCANSHARESTREAMOFFSET，则驱动程序必须使用指定 D3DDECLUSAGE \_ POSITIONT (0) 使用类型的元素处理所有顶点声明。 此驱动程序必须允许多个顶点元素：

-   在流中共享相同的偏移量。

-   不同类型。 因此，它们可以有不同的大小。

-   任意重叠。 例如，一个元素可以从当前位于另一个元素中间的流的位置开始。

 

 





