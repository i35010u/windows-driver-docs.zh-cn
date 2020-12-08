---
title: 计算点精灵的大小
description: 计算点精灵的大小
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，点子画面
- point sprite WDK DirectX 8。0
- 大小 WDK 点子画面
- 点大小 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f154c92170b2e6b5793f48e356ed4c951fb67ffa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810199"
---
# <a name="computing-the-size-of-point-sprites"></a>计算点精灵的大小


## <span id="ddk_computing_the_size_of_point_sprites_gg"></span><span id="DDK_COMPUTING_THE_SIZE_OF_POINT_SPRITES_GG"></span>


使用现有的 D3DPT 点基元类型呈现点子画面 \_ 。 可以通过新的呈现状态 D3DRS \_ POINTSIZE 或新的 FVF 组件 D3DFVF PSIZE 控制子画面的大小 \_ 。

对于没有 D3DFVF \_ PSIZE 顶点组件的顶点， \_ 应使用 D3DRS POINTSIZE 渲染状态的当前值。 否则，应使用顶点数据中指定的值。 在任一情况下，值都是一个浮点数，它是呈现的四个呈现目标像素 (宽度和高度) 的大小。 在初始化期间，点大小呈现状态 (1.0) 的默认值将发送给驱动程序。

两个呈现状态控制钳位的计算点动画大小，D3DRS \_ POINTSIZE \_ MIN 和 D3DRS \_ POINTSIZE \_ MAX。 应将该点的计算大小限制为小于 D3DRS POINTSIZE MIN 给定的大小 \_ \_ ，且不能大于 D3DRS POINTSIZE MAX 给出的大小 \_ \_ 。 驱动程序的责任是确保将点动画大小限制到渲染状态指定的最小大小和最大大小。

对于支持硬件顶点处理的驱动程序，点 sprite 的大小还可以根据) 中点与眼睛 (的距离进行缩放。 点 sprite 的缩放通过新的呈现状态 D3DRS \_ POINTSCALEENABLE 启用。 如果此呈现状态的值为 **TRUE** ，则根据以下参数、Ss 公式和最大/最小值决定缩放点。 请注意，在这种情况下，应用程序指定的点大小用相机空间单位表示。 此缩放由仅支持转换和照明的驱动程序执行。

<span id="Si"></span><span id="si"></span><span id="SI"></span>S<sub>i</sub>  
输入点大小 (为每个顶点或 D3DRS \_ POINTSIZE) 

<span id="A_B_C"></span><span id="a_b_c"></span>A、B、C  
点缩放系数 D3DRS \_ POINTSCALEA/B/C

<span id="Vh"></span><span id="vh"></span><span id="VH"></span>Vh  
 (D3D 视区中 **dwHeight** 字段的视区高度 \_) 

<span id="Pe____Xe__Ye__Ze_"></span><span id="pe____xe__ye__ze_"></span><span id="PE____XE__YE__ZE_"></span>P ₑ = (X ₑ，Y ₑ，Z ₑ)   
点的目视空间位置

<span id="De___sqrt__Xe2___Ye2___Ze2_"></span><span id="de___sqrt__xe2___ye2___ze2_"></span><span id="DE___SQRT__XE2___YE2___ZE2_"></span>De = sqrt (X ₑ² + Y ₑ² + Z ₑ²)   
从眼睛到位置 (眼的距离) 

<span id="Ss___Vh___Si___sqrt_1__A___B_De___C__De2___"></span><span id="ss___vh___si___sqrt_1__a___b_de___c__de2___"></span><span id="SS___VH___SI___SQRT_1__A___B_DE___C__DE2___"></span>Ss = Vh \* S<sub>i</sub> \* sqrt (1/ (A + B \* D ₑ + C \* (d ₑ²) # A4 # A5  
屏幕空间点大小

<span id="Smax"></span><span id="smax"></span><span id="SMAX"></span>Smax  
**MaxPointSize** (D3DCAPS8) 设备功能的成员

<span id="Smin"></span><span id="smin"></span><span id="SMIN"></span>Smin  
D3DRS \_ POINTSIZE \_ MIN

<span id="Final_screen-space_point_size_S__"></span><span id="final_screen-space_point_size_s__"></span><span id="FINAL_SCREEN-SPACE_POINT_SIZE_S__"></span>最终屏幕空间点大小 S =  
Smax if Ss &gt; Smax

Smin if Ss &lt; Smin

Ss，否则

请注意，对于要绘制单像素顶点的应用程序，不应使用点子画面，它必须设置以下渲染状态：

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

 

 





