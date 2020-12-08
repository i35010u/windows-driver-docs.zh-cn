---
title: 在 8 位 YUV 色彩空间中进行处理
description: 在 8 位 YUV 色彩空间中进行处理
keywords:
- ProcAmp WDK DirectX VA，YUV 颜色空间
- YUV 格式化 WDK DirectX VA
- Y 处理 WDK DirectX VA
- UV 处理 WDK DirectX VA
- 颜色空间转换 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f00862b9fec4de31960aea25be74ddcf70bd9a6b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820369"
---
# <a name="processing-in-the-8-bit-yuv-color-space"></a>在 8 位 YUV 色彩空间中进行处理


## <span id="ddk_processing_in_the_8_bit_yuv_color_space_gg"></span><span id="DDK_PROCESSING_IN_THE_8_BIT_YUV_COLOR_SPACE_GG"></span>


在 YUV 颜色空间中工作可简化视频流的 ProcAmp 调整控制所涉及的计算。

### <a name="span-idy_processingspanspan-idy_processingspanspan-idy_processingspany-processing"></a><span id="Y_Processing"></span><span id="y_processing"></span><span id="Y_PROCESSING"></span>Y 处理

若要对 Y 组件执行 ProcAmp 调整，请从 Y 值减去16，将黑色级别置于零。 这会删除 DC 偏移，以便调整对比度不会改变黑色。 由于 Y 值可能小于16，此时应支持负 Y 值。 对比度是通过将 YUV 像素值乘以常量来调整的。 如果没有调整，则每当对比度发生变化时，都会产生颜色变换。 亮度属性值添加 (或减去对比度调整的 Y 值) 这样做是为了避免由于调整对比度而引入 DC 偏移量。 最后，添加值16以将黑色级别重定位为16。

以下公式汇总了上一段中所述的步骤。 C 是对比度值，B 是亮度值。

```cpp
Y' = ((Y - 16) x C) + B + 16
```

### <a name="span-iduv_processingspanspan-iduv_processingspanspan-iduv_processingspanuv-processing"></a><span id="UV_Processing"></span><span id="uv_processing"></span><span id="UV_PROCESSING"></span>UV 处理

若要为你的和 V 组件执行 ProcAmp 调整，请从你的和 V 值中减去128，以将范围绕零。 通过混合你和 V 值来实现色相属性，如以下公式所示。 H 是所需的色调角度：

```cpp
U' = (U-128) x Cos(H) + (V-128) x Sin(H)
V' = (V-128) x Cos(H) - (U-128) x Sin(H)
```

饱和度按 U "and V" 乘以一对常量，然后将128添加到每个常量。 以下公式显示了针对 UV 数据的色调和饱和度的组合处理。 H 是所需的色调角度，C 是对比度值，S 是饱和度值：

```cpp
U'' = (((U-128) x Cos(H) + (V-128) x Sin(H)) x C x S) + 128
V'' = (((V-128) x Cos(H) - (U-128) x Sin(H)) x C x S) + 128
```

 

 





