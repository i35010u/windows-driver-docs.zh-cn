---
title: 多平面覆盖硬件要求
ms.assetid: 3BDA8F54-A0D8-4879-A828-89A2E4254179
description: 支持 multiplane 覆盖所需的硬件要求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bff654fda8156c47104c795d5aa410667ec12be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565136"
---
# <a name="multiplane-overlay-hardware-requirements"></a>多平面覆盖硬件要求


显示驱动程序和硬件不支持所需 multiplane 覆盖。 但是，若要提供 multiplane 覆盖的支持，硬件必须满足以下要求：

-   硬件必须支持非重叠平面：
    -   一个平面可以涵盖一个屏幕的一部分，而另一个平面可以涵盖不同，互斥的大部分屏幕。
    -   如果在平面未涵盖在屏幕的任何部分，硬件必须扫描出针对该区域的黑色。 硬件可以假定在最底层是虚拟的平面*z*填充有黑色的顺序。
-   硬件必须支持重叠平面：
    -   硬件必须能够启用或禁用 alpha 值混合处理每个平面基础上。 （alpha 值混合处理是一种技术中的源位图的颜色的合并目标位图，以生成新的目标位图中。）
    -   必须支持之间的平面使用预乘的 alpha 值混合处理。
-   当只有一个输出目标处于活动状态时，活动的输出必须支持 multiplane 覆盖。 克隆模式，其中多个输出是同时处于活动状态，对于硬件不应报告它支持 multiplane 覆盖，除非所有活动的输出支持 multiplane 覆盖。
-   桌面窗口管理器 (DWM) 的 swapchain （平面 0） 必须能够与其他覆盖平面进行交互。
-   所有平面都必须能够启用和禁用，包括平面 0 (DWM 的 swapchain)。
-   所有平面必须都支持源和目标剪辑，包括平面 0 (DWM 的 swapchain)。
-   收缩和拉伸，独立于可能启用其他平面，必须支持至少一个平面。
-   支持缩放的平面必须支持双线性筛选和筛选优于双线性的质量。
-   至少一个平面必须支持这些 YUV 格式 (有关详细信息，请参阅[YUV 格式范围在 Windows 8.1 中](yuv-format-ranges.md)):
    -   ITU BT.601 和 BT.709 YUV 到 RGB 矩阵转换，则为 YUV 格式。
    -   正常 （或 studio） 范围 YUV 亮度 (16 235) 和扩展范围 YUV 亮度 (0-255)。
-   硬件必须处理这些寄存器闩锁的方案：
    -   在垂直回描期间必须以原子方式发布所有平面每个属性 （缓冲区地址、 剪辑、 缩放和等等）。 在更新时的寄存器的块，它们必须所有 post 以原子方式 — 例如，如果写入 10 20 覆盖平面与相关的寄存器的后发生的垂直同步，其中任何一个将发布直到下一个 VSync 因为它们不能在当前垂直同步的所有 post)。
    -   可以从其他平面独立更新每个平面。 例如，如果已在垂直同步之前更新平面 0 寄存器和更高版本的平面 1 注册更新的垂直同步发生时，平面 1 更新可能会等到下一个垂直同步，但平面 0 更新应发生在时间上。
    -   当多个平面更新期间存在一次调用时，应以原子方式进行更新。 例如，如果单个 present 调用正在更新平面 0 并启用平面 1，平面 0 寄存器 VSync 不应进行发布，除非平面 1 还注册相同的 VSync 上的帖子。
-   转换、 缩放和混合应按以下顺序发生：
    1.  根据指定的源矩形被剪辑源分配。 确保源矩形边界内源分配的大小。
    2.  垂直图像翻转如果请求则应用水平图像翻转。
    3.  应用缩放根据目标矩形，将根据剪辑矩形的剪辑应用和应用适当的筛选，缩放时。
    4.  与其他层分配混合。 混合应执行从上到下 （或直到命中一个不透明的层） 中*z*的顺序。 如果 alpha 值混合处理请求，硬件必须接受每个-像素的 alpha、 和颜色值都预先乘以 alpha。 下面的伪代码对目标操作重复从上到下，执行源 (((层\[0\]通过层\[1\]) 通过层\[2\]) 通过...层\[n\])。 外部目标矩形中，必须将每个层视为透明 (0,0,0,0)。

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

        硬件可以混合从底部到顶部，前提是输出结果中时相同。 在这种情况下，应使用以下 blend 算法：

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

    5.  必须在区域中显示黑色位置不受任何来自任何层的目标矩形。 硬件可以假定没有概念虚拟最底部的黑色层是屏幕的大小。

 

 





