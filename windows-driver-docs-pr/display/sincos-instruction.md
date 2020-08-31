---
title: SINCOS 指令格式
description: SINCOS 指令格式
ms.assetid: df9b51ef-5a9f-4222-a0be-a40d5b577f9a
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ded4d0557cc3bd8816b893181ba87f8fd415137d
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066626"
---
# <a name="sincos-instruction-format"></a>SINCOS 指令格式


## <span id="ddk_sincos_instruction_gg"></span><span id="DDK_SINCOS_INSTRUCTION_GG"></span>


SINCOS 指令计算以弧度表示的正弦和余弦值。 结果的 X 分量包含 cos (X) ;Y 组件包含 sin (x) 。

### <a name="span-idformatspanspan-idformatspanformat"></a><span id="format"></span><span id="FORMAT"></span>形式

包含 D3DSIO SINCOS 的[指令标记](instruction-token.md) \_ 。 指令长度为4。

使用 D3DSPR TEMP 寄存器类型的[目标参数标记](destination-parameter-token.md) \_ [register type](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)。

第一个 [源参数标记](source-parameter-token.md)。 要求显式使用复制 swizzle，即 X、Y、Z 或 W swizzle 组件 (或 R、G、B 或等效) 必须指定。

**以下源标记适用于 3 0 之前的像素和顶点着色器版本 \_ 。也就是说，对于像素和顶点着色器版本 3 \_ 0 及更高版本，只使用第一个源形参标记。**

使用 D3DSPR 临时寄存器类型的第二个源参数标记 \_ 。

使用 D3DSPR TEMP 寄存器类型的第三个源参数标记 \_ 。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

第二个和第三个源可用作临时寄存器。

源寄存器规则：

-   src1. 所选 \_ 通道是-pi 和 + Pi 之间以弧度表示的角。

-   src2 = ([ (\* ˆ]128) ，ˆ/ (6！ \*64) ，1. f/ (4！ \*16) 、1. f/ (5！ \*32) ) 。

-   src3 = (ˆ "1. f/ (3！ \*8) ，ˆ/ (2！ \*8) ，1. f，0.5 f) 。

    Src2 和 src3 中最后两个数字的顺序是专门选择的，以容纳像素着色器2.0，这也包含 SINCOS 宏。 反转这些数字意味着宏展开可以使用几个可用于 ps 2 0 的自定义源 swizzles 中的一项， \_ \_ (顶点着色器具有常规 swizzle，因此没有) 问题。 这允许使用相同的自定义常量，而不考虑使用 sincos 的位置。

目标寄存器规则：

-   dest = cos (src1。所选 \_ 通道) ，dest = sin (src1 \_ 通道) ，目标 z 在指令后未定义。

-   dest 不应与 src1 相同。

-   仅允许 X 和 Y 位于目标写入掩码中。

SINCOS 指令是一个采用8个指令槽的宏指令。

仅允许 X 和 Y 位于目标写入掩码中。

最大绝对错误为0.002。

### <a name="span-idoperationspanspan-idoperationspanoperation"></a><span id="operation"></span><span id="OPERATION"></span>运作

下面显示了 sin (x) 和 cos (x) 的 Taylor 系列：


`(1) cos(x) = 1 - x2/2! + x4/4! - x6/6!
sin(x) = x - x3/3! + x5/5! - x7/7! = x*(1 - x2/3! + x4/5! - x6/7!)`

为了增加精度，我们使用 cos (x/2) 来计算 cos (x) ：

`(2) cos(x) = 1 - 2*sin(x/2)*sin(x/2)
sin(x) = 2*sin(x/2)*cos(x/2)`

 (1) 可以通过将 x 替换为 x/2 来重新编写，如下所示：

`(3) cos(x) = 1 - x2/(2!*4) + x4/(4!*16) - x6/(6!*64)
sin(x) = x/2 - x3/(3!*8) + x5/(5!*32) - x7/(7!*128) =
= x*(0.5f - x2/(3!*8) + x4/(5!*32) - x6/(7!*128))`

让我们以矢量形式编写 (3) 。 此处 a、b、c、d 是2D 常量向量：

`a + x2*b + x4*c + x6*d = a+x2*(b + x2*(c + x2*d)`


下面演示了 SINCOS 的实现：


SRC2 应为常量：

`(1.f/(7!*128), 1.f/(6!*64), 1.f/(4!*16), 1.f/(5!*32) )`

SRC3 应为常量：

```cpp
(1.f/(3!*8), 1.f/(2!*8), 1.f, 0.5f )
VECTOR v1 = EvalSource(SRC1);
VECTOR v2 = EvalSource(SRC2);
VECTOR v3 = EvalSource(SRC3);
VECTOR v;
MUL v.z, v1.w, v1.w ; x*x
MAD v.xy, v.z, v2.xy, v2.wz
MAD v.xy, v.xy, v.z, v3.xy
MAD v.xy, v.xy, v.z, v3.wz ; 
```

部分 sin (x/2) ，最终 cos (x/2) ：

```cpp
MUL v.x, v.x, v1.w ; sin(x/2)
MUL v.xy, v.xy, v.x ; compute sin(x/2)*sin(x/2) and sin(x/2)*cos(x/2)
ADD v.xy, v.xy, v.xy ; 2*sin(x/2)*sin(x/2) and 2*sin(x/2)*cos(x/2)
ADD v.x, -v.x, v3.z ; cos(x) and sin(x)
WriteResult(v, DST);
```

如果应用程序必须为任意角度计算 SINCOS，则可以使用以下 (宏将角度映射到范围-Pi ... + Pi：) 的原始角度：

```macro
def c0, Pi, 0.5f, 2*Pi, 1/(2*Pi)
mad r0.x, r.x, c0.w, c0.y
frc r0.x, r0.x
mad r0.x, r0.x, c0.z, -c0.x
```

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

