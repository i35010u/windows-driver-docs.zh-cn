---
title: 处理压缩在 SysMem 中创建的纹理图面
description: 处理在系统内存中创建的压缩纹理图面
ms.assetid: 773962ce-f459-4dc5-8311-c43ae33cfb7c
keywords:
- 绘制压缩纹理 WDK DirectDraw，系统内存的注意事项
- DirectDraw 显示压缩的纹理 WDK Windows 2000，系统内存的注意事项
- 压缩的纹理图面 WDK DirectDraw，系统内存的注意事项
- WDK DirectDraw，压缩的纹理的图面
- 纹理 WDK DirectDraw 压缩
- 绘制压缩纹理 WDK DirectDraw，宽度
- DirectDraw 显示压缩的纹理 WDK Windows 2000 宽度
- 压缩的纹理图面 WDK DirectDraw，宽度
- 绘制压缩纹理 WDK DirectDraw，高度
- DirectDraw 显示压缩的纹理 WDK Windows 2000 高度
- 压缩的纹理图面 WDK DirectDraw，高度
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 31b84bfb1387bc43bb30f260a83a98e86aed126f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323792"
---
# <a name="handling-compressed-texture-surfaces-created-in-system-memory"></a>处理在系统内存中创建的压缩纹理图面

**本主题仅适用于基于 Windows NT 的操作系统。**

若要强制分配合适的内存数量的内核模式下运行时的用户模式下运行时更改的宽度和高度压缩纹理图面在系统内存中创建。 显示驱动程序必须撤消此更改，以防止此故障的图面执行的后续操作。 每当 DirectDraw 运行时调用的驱动程序[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)函数创建压缩纹理图面，该驱动程序必须还原的宽度和高度的面其未更改的状态。

在驱动程序*D3dCreateSurfaceEx*函数接收表面的宽度、 音调、 和高度更改，如下所示：

-   宽度和间距包含 4 × 4 中的块数乘以块大小的行数。

-   高则包含的列中的 4 × 4 块的数目。

下面的代码段显示了该驱动程序必须执行还原的宽度和高度的图面中的计算：

```cpp
RealWidth = (Width / Block size) * 4;
RealHeight = Height * 4;
```

该驱动程序应将已还原的宽度和高度值分配给在内核中的成员[ **DD\_面\_全局**](https://msdn.microsoft.com/library/windows/hardware/ff551726)呈现结构。 这样做会阻止 DirectDraw 内核模式下的运行时从拒绝 DXT 纹理下载 blts 因为宽度和高度值不匹配。 也就是说，如果驱动程序将在更改后的大小，则**wWidth**并**wHeight** DD 的成员\_图面\_全局、 DirectDraw 内核模式下运行时拒绝从 blt更改到视频内存面上的系统内存图面，因为的宽度和高度的源，即未更改的坐标，似乎是"外部"更改 DD\_面\_全局大小。

 

 





