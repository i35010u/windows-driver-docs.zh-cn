---
title: 支持流中具有相同偏移量的顶点元素
description: 支持流中具有相同偏移量的顶点元素
ms.assetid: 52b2d891-15a1-4b82-aaf2-634f33202974
keywords:
- 顶点着色器声明 WDK DirectX 9.0 中，共享流中的偏移量
- 着色器声明 WDK DirectX 9.0 中，共享流中的偏移量
- 顶点流偏移量 WDK DirectX 9.0
- 顶点流偏移量 WDK DirectX 9.0 中，顶点着色器声明
- 流偏移量 WDK DirectX 9.0
- 流偏移量 WDK DirectX 9.0 中，顶点着色器声明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbe198f9fda0496b165a28b90df11fb4499feee9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350104"
---
# <a name="supporting-vertex-elements-sharing-offset-in-a-stream"></a>支持流中具有相同偏移量的顶点元素


## <span id="ddk_supporting_vertex_elements_sharing_offset_in_a_stream_gg"></span><span id="DDK_SUPPORTING_VERTEX_ELEMENTS_SHARING_OFFSET_IN_A_STREAM_GG"></span>


DirectX 9.0 版本驱动程序指示其设备，可以通过设置 D3DDEVCAPS2 共享相同的偏移量流中的多个顶点元素\_VERTEXELEMENTSCANSHARESTREAMOFFSET 功能位**DevCaps2**D3DCAPS9 结构的成员。 顶点着色器声明包含一个顶点元素的数组。 有关详细信息，请参阅[分隔的声明和顶点着色器代码](separating-declarations-and-code-for-vertex-shaders.md)。

如果用于早于 3.0 支持像素着色器 (PS) 版本的设备的 DirectX 9.0 驱动程序设置 D3DDEVCAPS2\_VERTEXELEMENTSCANSHARESTREAMOFFSET，该驱动程序可以处理大多数顶点声明具有的元素的指定 D3DDECLUSAGE\_POSITIONT (0) 的使用类型。 此预 PS 3.0 驱动程序将顶点声明与 D3DDECLUSAGE\_POSITIONT (0) 到有效灵活顶点格式 (FVF)。 但是，此预 PS 3.0 的驱动程序不能处理具有元素，用于指定 D3DDECLUSAGE 顶点声明\_POSITIONT (0) 使用类型，如果声明具有纹理坐标中的缺口。 例如，此预 PS 3.0 驱动程序无法处理以下顶点声明：

```cpp
{0,0,D3DDECLTYPE_FLOAT4, D3DDECLMETHOD_DEFAULT, D3DDECLUSAGE_POSITIONT, 0}
{0,16,D3DDECLTYPE_FLOAT2, D3DDECLMETHOD_DEFAULT, D3DDECLUSAGE_TEXCOORD, 0}
{0,24,D3DDECLTYPE_FLOAT2, D3DDECLMETHOD_DEFAULT, D3DDECLUSAGE_TEXCOORD, 5}
```

由于没有间隙纹理坐标中的，此预 PS 3.0 的驱动程序不能表达 D3DDECLUSAGE\_使用 FVF TEXCOORD 元素。

如果设备支持像素着色器 3.0 及更高版本的 DirectX 9.0 驱动程序设置 D3DDEVCAPS2\_VERTEXELEMENTSCANSHARESTREAMOFFSET，该驱动程序必须处理具有指定 D3DDECLUSAGE 的元素的所有顶点声明\_POSITIONT (0) 的使用类型。 此驱动程序必须允许多个顶点元素：

-   共享流中相同的偏移量。

-   为不同类型。 因此，它们可能具有不同的大小。

-   任意重叠。 例如，一个元素可以启动流当前正在进行另一个元素的位置。

 

 





