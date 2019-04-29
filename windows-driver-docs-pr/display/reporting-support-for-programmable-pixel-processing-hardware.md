---
title: 报告可编程像素着色器硬件的支持
description: DirectX 8.0 级别驱动程序的可编程像素着色器硬件报表技术支持，它必须将 D3DCAPS8 结构 PixelShaderVersion 字段设置为有效的、 非零像素着色器版本数。
ms.assetid: e6456c2a-d40f-4082-9122-fab9299808f7
keywords:
- 像素着色器 WDK DirectX 8.0，可编程硬件
- 处理硬件 WDK DirectX 8.0 的可编程像素
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: e046280f8c72a05f3a5e153703b2079b38787326
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383245"
---
# <a name="reporting-support-for-programmable-pixel-shader-hardware"></a>报告可编程像素着色器硬件的支持

DirectX 8.0 级别驱动程序的可编程像素着色器硬件报表技术支持，它必须设置**PixelShaderVersion** D3DCAPS8 结构为有效的、 非零像素着色器版本数的字段。 **PixelShaderVersion**是一个 dword 值，其中最重要的词必须具有 0xFFFF 的值和最不重要的 word 保存的实际版本数量。 此 word 此最低有效字节持有的次版本号，最高有效字节包含主版本号。 由于此 DWORD 的格式很复杂，该驱动程序必须设置的值**PixelShaderVersion**使用宏 D3DPS\_版本中定义*d3d8types.h*。 例如，以下代码段集**PixelShaderVersion**以指示对 1.0 级别功能的支持。

```cpp
myD3DCaps8.PixelShaderVersion = D3DPS_VERSION(1, 0);
```

不支持可编程像素处理的驱动程序应设置**PixelShaderVersion**为零。

与不同的报告的设备具有顶点着色器的常量寄存器的数量，设备不能公开更常量寄存器不是由它指定像素着色器版本。 例如，实现 1.0 像素着色器规范的设备必须公开仅包括八种常量像素着色器寄存器。 但是，没有其他像素着色器相关的功能，应设置驱动程序，请**MaxPixelShaderValue**。 此字段用于提供支持的像素颜色混合操作值的内部范围。

实现必须允许它们报告通过像素处理以未修改形式 （例如，unclamped） 范围内的数据。 此值通常定义的已签名的范围，它是一个绝对值的限制。 因此，例如，1 表示的范围是\[-1.0 到 1.0\]，，8 表示该范围\[-8.0 到 8.0\]。 像素着色器版本 1.0 到 1.3，驱动程序必须设置的值**MaxPixelShaderValue**到最小为 1。 该驱动程序必须将该值设置为 1.4， **MaxPixelShaderValue**为 8 的最小值。

 

 





