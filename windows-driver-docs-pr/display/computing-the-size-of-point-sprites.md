---
title: 计算点精灵的大小
description: 计算点精灵的大小
ms.assetid: f92ea8c6-f330-4625-873f-70c773c86334
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，点 sprite
- 点 sprite WDK DirectX 8.0
- 大小 WDK 点 sprite
- 点大小 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86a96206888332e65105b63963a3bf69f17a2ede
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372944"
---
# <a name="computing-the-size-of-point-sprites"></a>计算点精灵的大小


## <span id="ddk_computing_the_size_of_point_sprites_gg"></span><span id="DDK_COMPUTING_THE_SIZE_OF_POINT_SPRITES_GG"></span>


通过使用现有 D3DPT 呈现点 sprite\_点基元类型。 点动画层的大小可以控制通过新呈现状态 D3DRS\_POINTSIZE 或由新 FVF 组件 D3DFVF\_PSIZE。

而无需 D3DFVF 顶点\_PSIZE 顶点组件，D3DRS 的当前值\_应使用 POINTSIZE 呈现状态。 否则，应使用的顶点数据中指定的值。 在任一情况下，值是浮点数，它是在呈现目标像素呈现的四核的大小 （宽度和高度）。 在初始化期间，如果向驱动程序发送的点大小呈现状态 (1.0) 的默认值。

两个呈现状态控制计算的点子画面大小，D3DRS 夹紧\_POINTSIZE\_最小值和 D3DRS\_POINTSIZE\_最大值。 点的计算的大小应被限制为不小于 D3DRS 所指定的大小\_POINTSIZE\_最小值，但不大于 D3DRS 所指定的大小\_POINTSIZE\_最大值。 它是驱动程序的责任，以确保点子画面大小被限制到指定的呈现状态的最小值和最大大小。

支持硬件顶点处理的驱动程序，请点 sprite 的大小可能还会按比例基于上为 （以关注空间） 关注点的距离。 通过新的呈现状态 D3DRS 启用缩放的点 sprite\_POINTSCALEENABLE。 如果此设置的值呈现状态是 **，则返回 TRUE**然后磅为单位进行缩放根据以下参数、 Sₛ 公式和最大/最小值确定。 请注意在此情况下，应用程序指定的点大小表示照相机中空间单位。 由驱动程序支持转换和仅反射的情况下，执行这种扩展。

<span id="Si"></span><span id="si"></span><span id="SI"></span>S<sub>i</sub>  
输入点大小 (每个顶点或 D3DRS\_POINTSIZE)

<span id="A_B_C"></span><span id="a_b_c"></span>A,B,C  
点规模因素 D3DRS\_POINTSCALEA/B/C

<span id="Vh"></span><span id="vh"></span><span id="VH"></span>Vₕ  
视区的高度 (**dwHeight**字段中 D3D\_视区)

<span id="Pe____Xe__Ye__Ze_"></span><span id="pe____xe__ye__ze_"></span><span id="PE____XE__YE__ZE_"></span>Pₑ = （Xₑ、 Yₑ、 Zₑ）  
关注点的空间位置

<span id="De___sqrt__Xe2___Ye2___Ze2_"></span><span id="de___sqrt__xe2___ye2___ze2_"></span><span id="DE___SQRT__XE2___YE2___ZE2_"></span>De = sqrt （Xₑ² + Yₑ² + Zₑ²）  
从监视到位置 （在原点的眼睛） 距离

<span id="Ss___Vh___Si___sqrt_1__A___B_De___C__De2___"></span><span id="ss___vh___si___sqrt_1__a___b_de___c__de2___"></span><span id="SS___VH___SI___SQRT_1__A___B_DE___C__DE2___"></span>Sₛ = Vₕ \* S<sub>i</sub> \* sqrt(1/(A + B\*Dₑ + C\*(Dₑ²)))  
屏幕空间点大小

<span id="Smax"></span><span id="smax"></span><span id="SMAX"></span>Smax  
**MaxPointSize** （D3DCAPS8 的成员） 的设备功能

<span id="Smin"></span><span id="smin"></span><span id="SMIN"></span>Smin  
D3DRS\_POINTSIZE\_最小值

<span id="Final_screen-space_point_size_S__"></span><span id="final_screen-space_point_size_s__"></span><span id="FINAL_SCREEN-SPACE_POINT_SIZE_S__"></span>最终的屏幕空间点大小为 S =  
Smax 如果 Sₛ &gt; Smax

Smin 如果 Sₛ &lt; Smin

否则为 Sₛ

请注意，若要进行绘制单个像素的顶点，而不是点 sprite 的应用程序，它必须具备以下条件呈现状态集：

```cpp
SetRenderState (D3DRS_POINTSCALEENABLE, FALSE)
// All textures must be turned off.
SetTexture (0, NULL); 
SetTextureStageState(1, D3DTSS_COLOROP,  D3DTOP_DISABLE);
// The point size render state must be set to any value between 0.0-1.0
SetRenderState(D3DRS_POINTSIZE, 1.0);
// D3DRS_POINTSIZE_MIN and D3DRS_POINTSIZE_MAX
// must be set appropriately to allow
// D3DRS_POINTSIZE to be set to a value between 0.0-1.0
```

 

 





