---
title: 显示内存
description: 显示内存
ms.assetid: 92092bf2-dc31-4781-82c6-3365df77af99
keywords:
- 显示内存 WDK DirectDraw 有关显示内存
- 有关显示内存的图形内存 WDK DirectDraw
- DirectDraw 内存 WDK Windows 2000 显示有关内存
- 有关内存的内存 WDK DirectDraw
- 绘制内存 WDK DirectDraw
- DirectDraw 内存 WDK Windows 2000 显示
- 内存 WDK DirectDraw
- 显示内存 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8540a92be9ef8a32bc98da934c9424fe07b3068f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327023"
---
# <a name="display-memory"></a>显示内存


## <span id="ddk_display_memory_gg"></span><span id="DDK_DISPLAY_MEMORY_GG"></span>


一般情况下，作为更以尽可能接近 DirectDraw 显示内存分配可以提高显示性能并允许游戏和其他 DirectDraw 应用程序运行得更快，更好的质量视觉对象图像。

通常情况下，显示卡具有设置为显示宽度，以便没有内存浪费右侧的间距 （从概念上讲） 的前台缓冲区。 这将使一个暂存区域在概念可用于其他表面的底部。 在这种情况下一个指针引用可访问的显示内存的整个区域因为内存访问是非常简单。

如果间距大于主表面的宽度，就会浪费内存右侧前台缓冲区的概念。 这必须回收为单独的矩形堆，而不管在卡上的内存是直线或矩形。 （即使内存是线性的某些显示驱动程序修补程序的音调 blitter 提高速度。 而是不是重写该驱动程序，可以只需回收内存为单独堆。）

 

 





