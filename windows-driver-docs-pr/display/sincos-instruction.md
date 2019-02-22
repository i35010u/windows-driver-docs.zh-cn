---
title: SINCOS 指令格式
description: SINCOS 指令格式
ms.assetid: df9b51ef-5a9f-4222-a0be-a40d5b577f9a
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2e21722699b161c6a5f365747e980fc5df4f0726
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526098"
---
# <a name="sincos-instruction-format"></a>SINCOS 指令格式


## <span id="ddk_sincos_instruction_gg"></span><span id="DDK_SINCOS_INSTRUCTION_GG"></span>


SINCOS 指令计算正弦和余弦值，以弧度为单位。 结果的 X 分量包含 cos(x);Y 分量包含 sin （x）。

### <a name="span-idformatspanspan-idformatspanformat"></a><span id="format"></span><span id="FORMAT"></span>格式

[指令令牌](instruction-token.md)，其中包含 D3DSIO\_SINCOS。 指令的长度为 4。

[目标参数标记](destination-parameter-token.md)使用 D3DSPR\_TEMP[注册类型](https://msdn.microsoft.com/library/windows/hardware/ff569707)。

第一个[源参数标记](source-parameter-token.md)。 要求必须指定显式使用复制 swizzle，也就是说，X、 Y、 Z 或 W swizzle 组件 （或等效的 R、 G、 B 或 A）。

**以下源标记是像素和顶点着色器版本早于 3\_0。也就是说，像素和顶点着色器版本 3\_0 和更高版本中，使用仅第一个源参数标记。**

第二个源参数标记使用 D3DSPR\_TEMP 注册类型。

第三个源参数标记使用 D3DSPR\_TEMP 注册类型。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

第二个和第三个源都用作临时寄存器。

源注册规则：

-   src1. 所选\_通道是角度以弧度为单位之间的 Pi 和 + Pi。

-   src2 = (âˆ’1.f/(7!\*128), âˆ’1.f/(6!\*64), 1.f/(4!\*16), 1.f/(5!\*32) ).

-   src3 = (âˆ’1.f/(3!\*8), âˆ’1.f/(2!\*8), 1.f, 0.5f).

    Src2 和 src3 中的最后两个数字的顺序是专门选择以适应像素着色器 2.0 中，它还具有 SINCOS 宏。 反转这些数字意味着将在宏扩展可以使用一个可供 ps 几个自定义源 swizzles\_2\_0 （顶点着色器具有常规 swizzle 这样没有问题）。 这样，相同的自定义常量使用，而不考虑 sincos 正在使用的位置。

目标注册规则：

-   dest.x = cos (src1.selected\_通道)，dest.y = sin (src1.selected\_通道)，dest.z 未定义的指令之后。

-   目标不应作为接管 src1 同一个寄存器。

-   仅 X 和 Y 可以是目标写掩码中。

SINCOS 指令是采用八个指令槽的宏指令。

仅 X 和 Y 可以是目标写掩码中。

最大绝对错误是 0.002。

### <a name="span-idoperationspanspan-idoperationspanoperation"></a><span id="operation"></span><span id="OPERATION"></span>操作

下面显示了 sin （x） 和 cos(x) Taylor 系列：


`(1) cos(x) = 1 - x2/2! + x4/4! - x6/6!
sin(x) = x - x3/3! + x5/5! - x7/7! = x*(1 - x2/3! + x4/5! - x6/7!)`

若要提高精度计算 cos(x) 使用 cos(x/2):

`(2) cos(x) = 1 - 2*sin(x/2)*sin(x/2)
sin(x) = 2*sin(x/2)*cos(x/2)`

（1） 可以重写替换为 x x / 2 一样：

`(3) cos(x) = 1 - x2/(2!*4) + x4/(4!*16) - x6/(6!*64)
sin(x) = x/2 - x3/(3!*8) + x5/(5!*32) - x7/(7!*128) =
= x*(0.5f - x2/(3!*8) + x4/(5!*32) - x6/(7!*128))`

允许以向量形式编写 (3)。 以下 a、 b、 c、 d 是 2D 常量向量：

`a + x2*b + x4*c + x6*d = a+x2*(b + x2*(c + x2*d)`


以下显示了 SINCOS 的实现：


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

部分 sin(x/2) 和最终 cos(x/2):

```cpp
MUL v.x, v.x, v1.w ; sin(x/2)
MUL v.xy, v.xy, v.x ; compute sin(x/2)*sin(x/2) and sin(x/2)*cos(x/2)
ADD v.xy, v.xy, v.xy ; 2*sin(x/2)*sin(x/2) and 2*sin(x/2)*cos(x/2)
ADD v.x, -v.x, v3.z ; cos(x) and sin(x)
WriteResult(v, DST);
```

如果任意角度的应用程序必须计算 SINCOS，角度可以映射到范围-Pi...+ Pi 通过使用以下宏 （r0.x 保留与原始角度）：

```macro
def c0, Pi, 0.5f, 2*Pi, 1/(2*Pi)
mad r0.x, r.x, c0.w, c0.y
frc r0.x, r0.x
mad r0.x, r0.x, c0.z, -c0.x
```

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

 





