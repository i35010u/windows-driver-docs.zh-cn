---
title: 报告可编程顶点着色器硬件的支持
description: 要使 DirectX 8.0 级别驱动程序报告对可编程顶点着色器硬件的支持，它必须将 D3DCAPS8 结构的 VertexShaderVersion 字段设置为有效的非零顶点着色器版本号。
keywords:
- 顶点着色器 WDK DirectX 8.0，可编程硬件
- 可编程顶点处理硬件 WDK DirectX 8。0
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: e45e39c534b161c875c3cc94634d702c472224ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841139"
---
# <a name="reporting-support-for-programmable-vertex-shader-hardware"></a>报告可编程顶点着色器硬件的支持

要使 DirectX 8.0 级别驱动程序报告对可编程顶点着色器硬件的支持，它必须将 D3DCAPS8 结构的 **VertexShaderVersion** 字段设置为有效的非零顶点着色器版本号。 **VertexShaderVersion** 是一个 DWORD，其中最重要的单词的值必须为0xFFFE，并且最不重要的单词包含实际版本号。 此字的最小有效字节包含次版本号，最高有效字节保留主版本号。 由于此 DWORD 的格式很复杂，因此驱动程序必须使用 **VertexShaderVersion** \_ *d3d8types* 中定义的宏 D3DVS 版本来设置 VertexShaderVersion 的值。 例如，下面的代码段设置 **VertexShaderVersion** 以指示支持1.0 级别功能。

```cpp
myD3DCaps8.VertexShaderVersion = D3DVS_VERSION(1, 0);
```

若要报告不支持可编程顶点着色器，请使用以下代码片段：

```cpp
myD3DCaps8.VertexShaderVersion = D3DVS_VERSION(0, 0);
```

不支持可编程顶点处理的驱动程序应将 **VertexShaderVersion** 设置为零。

除了设置顶点着色器版本之外，驱动程序还应报告其对顶点底纹的常量寄存器的数目。 为了支持1.0 顶点底纹规范，设备必须至少具有96个常量寄存器。 驱动程序报告 D3DCAPS8 结构的 **MaxVertexShaderConst** 字段中的常量寄存器的数目。 例如，下面的代码段报告版本1.0 顶点着色器所需的最小常量寄存器数。

```cpp
myD3DCaps8.MaxVertexShaderConst = 96;
```

*d3d8types* 定义顶点着色器规范1.0 版所需的最小常量寄存器的符号。 此符号为 D3DVS \_ CONSTREG \_ MAX \_ V1 \_ 0，建议使用此符号，除非它支持96个以上的常量寄存器。

 

 





