---
title: 处理在 SysMem 中创建的压缩纹理图面
description: 处理在系统内存中创建的压缩纹理图面
ms.assetid: 773962ce-f459-4dc5-8311-c43ae33cfb7c
keywords:
- 绘制压缩纹理 WDK DirectDraw，系统内存注意事项
- DirectDraw 压缩纹理 WDK Windows 2000 显示，系统内存注意事项
- 压缩的纹理面 WDK DirectDraw，系统内存注意事项
- 表面 WDK DirectDraw，压缩纹理
- 纹理 WDK DirectDraw，压缩
- 绘制压缩纹理 WDK DirectDraw，width
- DirectDraw 压缩纹理 WDK Windows 2000 显示，宽度
- 压缩的纹理面 WDK DirectDraw，width
- 绘制压缩纹理 WDK DirectDraw，高度
- DirectDraw 压缩纹理 WDK Windows 2000 显示，高度
- 压缩的纹理面 WDK DirectDraw，高度
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: e87b0a44d9a129e030fbbd0105c1871be344411a
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423856"
---
# <a name="handling-compressed-texture-surfaces-created-in-system-memory"></a>处理在系统内存中创建的压缩纹理图面

**本主题仅适用于基于 Windows NT 的操作系统。**

用户模式运行时将更改在系统内存中创建的压缩纹理表面的宽度和高度，以强制内核模式运行时分配适当的内存量。 显示驱动程序必须撤消此改变，以防止在此表面上执行的后续操作失败。 每当 DirectDraw 运行时调用驱动程序的 [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 函数来创建压缩纹理图面时，驱动程序必须将其宽度和高度恢复为未修改的状态。

驱动程序的 *D3dCreateSurfaceEx* 函数接收图面的宽度、间距和高度的更改，如下所示：

-   Width 和螺距包含行中4x4 块的数目乘以块大小。

-   Height 包含列中的4x4 块的数目。

下面的代码片段演示了驱动程序为还原图面的宽度和高度而必须执行的计算：

```cpp
RealWidth = (Width / Block size) * 4;
RealHeight = Height * 4;
```

驱动程序应将还原的宽度和高度值分配给内核的 [**DD \_ 表面 \_ 全局**](/windows/win32/api/ddrawint/ns-ddrawint-dd_surface_global) surface 结构中的成员。 这样做可以防止 DirectDraw 内核模式运行时拒绝 DXT 纹理下载 blts，因为宽度和高度值不匹配。 也就是说，如果驱动程序在 DD surface GLOBAL 的 **wWidth** 和 **wHeight** 成员中保留了修改后的大小 \_ \_ ，则 DirectDraw 内核模式运行时将拒绝从已更改的系统内存图面到视频内存图面的 blt，因为源的宽度和高度在改变的 DD \_ 表面全局大小看来为 "外部" \_ 。

 

