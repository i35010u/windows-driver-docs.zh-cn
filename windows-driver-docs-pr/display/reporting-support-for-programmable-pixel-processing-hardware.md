---
title: 报告可编程像素着色器硬件的支持
description: 要使 DirectX 8.0 级别驱动程序报告对可编程像素着色器硬件的支持，它必须将 D3DCAPS8 结构的 PixelShaderVersion 字段设置为有效的非零像素着色器版本号。
keywords:
- 象素着色器 WDK DirectX 8.0，可编程硬件
- 可编程像素处理硬件 WDK DirectX 8。0
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: e47a354d85355401780a0c71191884e05e2efc29
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786859"
---
# <a name="reporting-support-for-programmable-pixel-shader-hardware"></a>报告可编程像素着色器硬件的支持

要使 DirectX 8.0 级别驱动程序报告对可编程像素着色器硬件的支持，它必须将 D3DCAPS8 结构的 **PixelShaderVersion** 字段设置为有效的非零像素着色器版本号。 **PixelShaderVersion** 是一个 DWORD，其中最重要的词必须具有值0xffff，而最不重要的单词则包含实际版本号。 此词的此最小有效字节包含次版本号，最高有效字节保留主版本号。 由于此 DWORD 的格式很复杂，因此驱动程序必须使用 **PixelShaderVersion** \_ *d3d8types* 中定义的宏 D3DPS 版本来设置 PixelShaderVersion 的值。 例如，下面的代码段设置 **PixelShaderVersion** 以指示支持1.0 级别功能。

```cpp
myD3DCaps8.PixelShaderVersion = D3DPS_VERSION(1, 0);
```

不支持可编程像素处理的驱动程序应将 **PixelShaderVersion** 设置为零。

与报告设备对顶点着色器的常量寄存器数量不同，设备不能公开比它指定的像素着色器版本定义的更多的常量寄存器。 例如，实现1.0 像素着色器规范的设备必须仅公开8个常量像素着色器寄存器。 但是，驱动程序应设置其他像素着色器相关功能， **MaxPixelShaderValue**。 此字段提供像素颜色混合操作支持的内部值范围。

实现必须允许其报告范围内的数据通过未修改的像素处理 (例如 unclamped) 。 此值通常定义签名范围的限制，即绝对值。 例如，1表示范围为 \[ -1.0 到 1.0 \] ，8表示范围为 \[ -8.0 到 8.0 \] 。 对于像素着色器版本1.0 到1.3，驱动程序必须将 **MaxPixelShaderValue** 中的值设置为至少1。 对于1.4，驱动程序必须将 **MaxPixelShaderValue** 中的值设置为最小值8。

 

 





