---
title: 报告对可编程顶点着色器硬件的支持
description: DirectX 8.0 级别驱动程序的可编程顶点着色器硬件报表技术支持，它必须将 D3DCAPS8 结构 VertexShaderVersion 字段设置为有效的、 非零的顶点着色器版本数。
ms.assetid: c77dae52-ed7c-4385-b085-df3e16e53c5e
keywords:
- 顶点着色器 WDK DirectX 8.0，可编程硬件
- 处理硬件 WDK DirectX 8.0 的可编程顶点
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: fb39770b2db051e885ff52ba41be1b5149f45fd3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524669"
---
# <a name="reporting-support-for-programmable-vertex-shader-hardware"></a>报告对可编程顶点着色器硬件的支持

它必须设置为可编程顶点着色器硬件报表支持的 DirectX 8.0 级别驱动程序**VertexShaderVersion** D3DCAPS8 结构为有效的、 非零的顶点着色器版本数的字段。 **VertexShaderVersion**是一个 dword 值，其中最重要的词必须具有值 0xFFFE 和最不重要的 word 保存的实际版本数量。 该单词的最低有效字节持有的次版本号，最高有效字节包含主版本号。 由于此 DWORD 的格式很复杂，该驱动程序必须设置的值**VertexShaderVersion**使用宏 D3DVS\_版本中定义*d3d8types.h*。 例如，以下代码段集**VertexShaderVersion**以指示对 1.0 级别功能的支持。

```cpp
myD3DCaps8.VertexShaderVersion = D3DVS_VERSION(1, 0);
```

若要报告不可编程的顶点着色器的支持，将使用下面的代码段：

```cpp
myD3DCaps8.VertexShaderVersion = D3DVS_VERSION(0, 0);
```

不支持可编程顶点处理的驱动程序应设置**VertexShaderVersion**为零。

除了设置顶点着色器版本，该驱动程序应报告它具有的顶点着色常量寄存器的数量。 为了支持 1.0 顶点明暗度规范，设备必须具有至少 96 常量寄存器。 驱动程序报告的中的常量寄存器的数量**MaxVertexShaderConst** D3DCAPS8 结构的字段。 例如，下面的代码段报告所需的版本 1.0 顶点着色器常量寄存器的最小数目。

```cpp
myD3DCaps8.MaxVertexShaderConst = 96;
```

*d3d8types.h*定义的符号常量寄存器顶点着色器规范的版本 1.0 所需的最小数目。 此符号是 D3DVS\_CONSTREG\_最大\_V1\_0，它建议驱动程序使用此符号，除非它支持多个 96 常量寄存器。

 

 





