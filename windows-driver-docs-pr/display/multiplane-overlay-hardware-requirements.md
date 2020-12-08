---
title: 多平面覆盖硬件要求
description: 支持 multiplane 覆盖所需的硬件要求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 827e184f9847b6a637dcfe632101491e90c9eefe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830635"
---
# <a name="multiplane-overlay-hardware-requirements"></a>多平面覆盖硬件要求


不需要显示驱动程序和硬件即可支持 multiplane 覆盖。 但是，若要提供 multiplane 覆盖支持，硬件必须满足以下要求：

-   硬件必须支持非重叠平面：
    -   一个平面可以覆盖屏幕的一部分，而另一个平面可以覆盖不同的、相互排斥的部分。
    -   如果某个平面未涵盖屏幕的任何部分，则该硬件必须在该区域的黑色范围内扫描。 硬件可以假设有一个虚拟平面，其最小 *z* 顺序为黑色。
-   硬件必须支持重叠的平面：
    -   硬件必须能够对每个平面启用或禁用 alpha 混合。  (Alpha 混合是一种技术，其中源位图中的颜色与目标位图中的颜色组合在一起以生成新的目标位图。 ) 
    -   必须支持使用预乘 alpha 的平面之间的混合。
-   当只有一个输出目标处于活动状态时，活动输出必须支持 multiplane 覆盖。 对于克隆模式，如果多个输出同时处于活动状态，则硬件不应报告它是否支持 multiplane 覆盖，除非所有活动输出都支持 multiplane 叠加。
-   桌面窗口管理器 (DWM) 的存在 (平面 0) 必须能够与其他覆盖面进行交互。
-   所有飞机都必须能够启用和禁用，包括平面 0 (DWM 的存在) 。
-   所有平面都必须支持源和目标剪辑，包括平面 0 (DWM 的存在) 。
-   至少一个平面必须支持收缩和拉伸，这与可能启用的其他平面无关。
-   支持缩放的平面必须支持双线性筛选和筛选质量，这两种质量比双线性更好。
-   至少一个平面必须支持这些 YUV 格式 (有关详细信息，请参阅 [Windows 8.1 中的 YUV 格式范围](yuv-format-ranges.md)) ：
    -   对于 YUV 格式，ITU BT. 601 和 BT 为 709 YUV 到 RGB 矩阵转换。
    -   正常 (或工作室)  (16-235) 和扩展范围 YUV 亮度 (0-255) 。
-   硬件必须处理以下寄存器闩锁方案：
    -   在垂直回描期间，所有按平面属性 (缓冲区地址、剪辑、缩放等) 必须以原子方式发布。 更新寄存器块时，它们必须以原子方式全部发布—例如，如果 VSync 在写入10个与覆盖平面相关的20个寄存器后发生，则不会将任何内容发布到下一个 VSync，因为它们不能在当前 Vsync) 上全部发布。
    -   每个平面都可以独立于其他平面进行更新。 例如，如果在 VSync 和更高版本之前更新了飞机0注册，则在 VSync 发生时，平面1寄存器会更新，而平面1更新可能会等待下一 VSync，但平面0更新应在时间发生。
    -   如果在单个现场调用期间更新多个平面，则更新应以原子方式执行。 例如，如果单个现有调用正在更新平面0并启用平面1，则 "平面 0" 寄存器不应在 VSync 上发布，除非平面1的收银机还在同一 VSync 上发布。
-   转换、缩放和混合应按以下顺序进行：
    1.  根据指定的源矩形对源分配进行剪辑。 保证源矩形在源分配大小范围内进行限定。
    2.  应用水平图像翻转，然后在请求时垂直图像翻转。
    3.  根据目标矩形应用缩放，根据剪辑矩形应用剪辑，并在缩放时应用相应的筛选。
    4.  与其他层的分配混合。 应从上到下 (执行混合，或在按 *z* 顺序) 不透明层的情况下执行混合。 如果请求了 alpha 混合，则硬件必须遵循每像素的 alpha 值，颜色值将按 alpha 的值进行预处理。 下面的伪代码从上到下重复执行目标操作的源， ( # A1 # B2 层 0 over 第1层) 上第 \[ \] 2 层 \[ \] \[ \]) 通过¦第 \[ n \]) 。 在目标矩形以外，每一层都必须被视为透明 (0，0，0，0) 。

        ``` syntax
        Color = Color[0]; // Layer 0 is topmost.
        Alpha = Color[0].Alpha;
        for (i = 1; Alpha < 1 && i < LayersToBlend; i++)
        {
            Color += ((1 - Alpha) * Color[i]);
            Alpha += ((1 - Alpha) * Color[i].Alpha);
        }
        Output Color;
        ```

        只要输出结果相同，硬件就可以从下到上混合。 在这种情况下，应使用以下 blend 算法：

        ``` syntax
        Color = Color[LayersToBlend-1];  // Bottom-most layer
        Alpha = Color[LayersToBlend-1].Alpha;
        if (LayersToBlend > 1)
        {
            for (i = LayersToBlend - 2; Alpha < 1 && i >= 0; i--)
            {
                Color = Color[i] + ((1 - Color[i].Alpha) * Color;
                Alpha = Color[i].Alpha + (1 - Color[i].Alpha) * Alpha;
            }
        }
        Output Color;
        ```

    5.  黑色颜色必须显示在任何层的任何目标矩形均未涵盖的区域。 硬件可能会假设存在一个表示屏幕大小的概念性虚拟最底部黑色层。

 

 





