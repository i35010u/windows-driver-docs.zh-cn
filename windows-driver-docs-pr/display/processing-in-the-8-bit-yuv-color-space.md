---
title: 8 位 YUV 颜色空间中的处理
description: 8 位 YUV 颜色空间中的处理
ms.assetid: fbf62dc6-b5bf-43f6-baa8-c6d1cee80f9b
keywords:
- ProcAmp WDK DirectX VA , YUV color space
- YUV 格式 WDK DirectX VA
- Y 处理 WDK DirectX VA
- UV 处理 WDK DirectX VA
- 颜色空间转换 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b6b1094784003e6541d6569759c32f9c05ff419
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554549"
---
# <a name="processing-in-the-8-bit-yuv-color-space"></a>8 位 YUV 颜色空间中的处理


## <span id="ddk_processing_in_the_8_bit_yuv_color_space_gg"></span><span id="DDK_PROCESSING_IN_THE_8_BIT_YUV_COLOR_SPACE_GG"></span>


YUV 颜色空间中工作，简化了 ProcAmp 调整控件的视频流涉及到的计算。

### <a name="span-idyprocessingspanspan-idyprocessingspanspan-idyprocessingspany-processing"></a><span id="Y_Processing"></span><span id="y_processing"></span><span id="Y_PROCESSING"></span>Y 处理

若要执行的 Y 分量 ProcAmp 调整，减去从要放置在零处的黑色级别的 Y 值的 16。 这会删除 DC 偏移量，以便调整对比度不发生改变的黑色级别。 由于 Y 值可能小于 16，此时应支持负的 Y 值。 通过将乘以一个常量 YUV 像素值调整对比度。 如果不调整和 V，颜色变化会导致更改对比时。 亮度属性值添加 （或减去） 调整对比度 Y 值;这样做是为了避免引入由于调整对比度的 DC 偏移量。 最后，添加值 16 来重新定位的黑色 16 级别。

下面的公式总结了上一段中所述的步骤。 C 是对比度值，而 B 是亮度值。

```cpp
Y&#39; = ((Y - 16) x C) + B + 16
```

### <a name="span-iduvprocessingspanspan-iduvprocessingspanspan-iduvprocessingspanuv-processing"></a><span id="UV_Processing"></span><span id="uv_processing"></span><span id="UV_PROCESSING"></span>UV 处理

若要为你执行 ProcAmp 调整和 V 组件减去从你和 V 的值来定位范围大约零 128。 混合您实现 hue 属性和 V 值一起以下等式中所示。 H 是所需的 hue 角度：

```cpp
U&#39; = (U-128) x Cos(H) + (V-128) x Sin(H)
V&#39; = (V-128) x Cos(H) - (U-128) x Sin(H)
```

饱和度调整乘以 U 和 V 由一对常量，然后通过添加到每个 128。 组合的色调和饱和度 UV 数据处理所示的以下等式。 H 是所需的 hue 角度，C 是对比度值，S 是饱和度值：

```cpp
U&#39;&#39; = (((U-128) x Cos(H) + (V-128) x Sin(H)) x C x S) + 128
V&#39;&#39; = (((V-128) x Cos(H) - (U-128) x Sin(H)) x C x S) + 128
```

 

 





