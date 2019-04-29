---
title: 点、线条和三角形填充要求
description: 点、线条和三角形填充要求
ms.assetid: 1a0a8160-01e2-4fb7-b1a2-6b61f1021fb9
keywords:
- 点填充规则 WDK Direct3D
- 行填充规则 WDK Direct3D
- 三角形填充规则 WDK Direct3D
- 填充行 WDK Direct3D
- 填充点 WDK Direct3D
- 填充三角形 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21c812aa82f357bd87c4c185a4434947205bfad3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366303"
---
# <a name="point-line-and-triangle-filling-requirements"></a>点、线条和三角形填充要求


## <span id="ddk_point_line_and_triangle_filling_requirements_gg"></span><span id="DDK_POINT_LINE_AND_TRIANGLE_FILLING_REQUIREMENTS_GG"></span>


填充点、 线条和三角形的要求如下所示：

### <a name="span-idpointsspanspan-idpointsspan-points"></a><span id="points"></span><span id="POINTS"></span> 点

点填充和光栅化规则可确定一个点的呈现方式。 这些规则是相同的三角形填充规则。 所有标志和都适用于三角形的功能也都适用于点和进行相反转换。 引用实现扩展点在一个矩形和三角形填充规则应用于结果。

使用坐标 P₀(x,y) 给定一个点，生成四个新点 P₁、 P₂、 P₃ 和 P₄，如下所示：

```cpp
P1(x,y) = (x âˆ’ 0.5, y âˆ’ 0.5)
P2(x,y) = (x âˆ’ 0.5, y + 0.5)
P3(x,y) = (x + 0.5, y + 0.5)
P4(x,y) = (x + 0.5, y âˆ’ 0.5)
```

该矩形，您可以为两个三角形，如 (P₁，P₂，P₃) 和 (P₁，P₃，P₄)。 您还可以检查源代码文件中的呈现点参考光栅器实现*setup.cpp*并*scancnv.cpp*的 DirectX 驱动程序开发工具包 (DDK)。

### <a name="span-idlinesspanspan-idlinesspanlines"></a><span id="lines"></span><span id="LINES"></span>行

行填充规则 （即，确定一个行的呈现方式的规则） 遵循网格相交量化 (GIQ) 菱形约定。 有关 GIQ 菱形约定的详细信息，请参阅[修饰的行](cosmetic-lines.md)。 遵循以下规则的线条图形代码的示例可以参考光栅器源文件中找到在 DirectX DDK *setup.cpp*并*scancnv.cpp*。

### <a name="span-idtrianglesspanspan-idtrianglesspantriangles"></a><span id="triangles"></span><span id="TRIANGLES"></span>三角形

三角形填充规则可确定如何呈现一个三角形。 这些规则的相同点填充规则。 遵循三角形填充规则的三角形绘图代码的示例可在 DirectX DDK 中参考光栅器源文件*setup.cpp*并*scancnv.cpp*。

硬件应提供精选的上限和正确实现三种精选的模式。 下面的代码段确定是否选择数据中的当前三角形：

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

在前面的代码示例测试，以确定三角形面向哪种方法。 三角形是定义的 0,1,2 和测试的屏幕空间中正在开始沿逆时针方向。 如果不是，和沿顺时针方向消除，则会因为顶点顺时针顺序不绘制该三角形。

 

 





