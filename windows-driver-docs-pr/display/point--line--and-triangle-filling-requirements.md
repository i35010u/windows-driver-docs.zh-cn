---
title: 点、线条和三角形填充要求
description: 点、线条和三角形填充要求
keywords:
- 点填充规则 WDK Direct3D
- 行填充规则 WDK Direct3D
- 三角形填充规则 WDK Direct3D
- 填充线条 WDK Direct3D
- 填充点 WDK Direct3D
- 填充三角 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09f8e703ccb95ebcad679d50e25e006be0d12073
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795593"
---
# <a name="point-line-and-triangle-filling-requirements"></a>点、线条和三角形填充要求


## <span id="ddk_point_line_and_triangle_filling_requirements_gg"></span><span id="DDK_POINT_LINE_AND_TRIANGLE_FILLING_REQUIREMENTS_GG"></span>


填充点、线条和三角形的要求如下：

### <a name="span-idpointsspanspan-idpointsspan-points"></a><span id="points"></span><span id="POINTS"></span> 热点

点填充和光栅化规则确定如何呈现一个点。 这些规则与三角形填充规则完全相同。 适用于三角形的所有标志和功能也适用于点，反之亦然。 参考实现将一个点展开为一个矩形，并将三角形填充规则应用到结果。

给定坐标为 P ₀ (x，y) 的点时，将生成四个新点，p ₁，P ₂，p ₃，p ₄，如下所示：

```cpp
P1(x,y) = (x âˆ’ 0.5, y âˆ’ 0.5)
P2(x,y) = (x âˆ’ 0.5, y + 0.5)
P3(x,y) = (x + 0.5, y + 0.5)
P4(x,y) = (x + 0.5, y âˆ’ 0.5)
```

然后，该矩形将生成为两个三角形，如 (P ₁，P ₂，P ₃) 和 (P ₁，P ₃，P ₄) 。 你还可以在 (的 DDK) 的 DirectX 驱动程序开发工具包的源文件 *设置 .cpp* 和 *scancnv* 中检查参考光栅化实现。

### <a name="span-idlinesspanspan-idlinesspanlines"></a><span id="lines"></span><span id="LINES"></span>行

行填充规则 (即，确定如何呈现线条的规则) 遵循网格交集量化 (GIQ) 菱形约定。 有关 GIQ 菱形约定的详细信息，请参阅 [修饰线](cosmetic-lines.md)。 遵循这些规则的行绘制代码示例可在参考光栅化源文件 *设置 .cpp* 和 *Scancnv* 中的 DirectX DDK 中找到。

### <a name="span-idtrianglesspanspan-idtrianglesspantriangles"></a><span id="triangles"></span><span id="TRIANGLES"></span>三角

三角形填充规则确定如何呈现三角形。 这些规则与点填充规则完全相同。 下面是一个三角形填充规则后面的三角形绘图代码的示例，可在参考光栅化源文件 *设置 .cpp* 和 *Scancnv* 中的 DirectX DDK 中找到。

硬件应提供剔除 cap 并正确实现三种精选模式。 下面的代码片段确定是否要剔除当前三角形：

```cpp
if (CurrentCullMode != D3DCULL_NONE) {
    int ccw = (((v[0]->sx - v[2]->sx) *
                (v[1]->sy - v[2]->sy)) <
               ((v[1]->sx - v[2]->sx) *
                (v[0]->sy - v[2]->sy)));
if ((CurrentCullMode == D3DCULL_CW && (ccw == 0)) ||
        (CurrentCullMode == D3DCULL_CCW && (ccw != 0))) {
        // Current triangle is culled, move onto
        // next triangle.
    }
}
// Current triangle is not culled, render it
```

前面的代码示例将测试，以确定三角形的方向。 三角形定义为0、1、2，并在屏幕空间中对其进行了测试。 如果不是，并且有顺时针剔除，则不绘制三角形，因为顶点以顺时针顺序排列。

 

 





