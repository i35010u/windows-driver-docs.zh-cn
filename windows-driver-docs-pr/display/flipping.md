---
title: 交替
description: 交替
keywords:
- 泪水 WDK DirectDraw
- 绘图页翻转 WDK DirectDraw，关于翻转
- DirectDraw 翻转 WDK Windows 2000 显示，关于翻转
- 翻转 WDK DirectDraw 页面，关于翻转
- 翻转 WDK DirectDraw，关于翻转
- 绘图页反向 WDK DirectDraw
- DirectDraw 翻转 WDK Windows 2000 显示器
- 页面翻转 WDK DirectDraw
- 翻转 WDK DirectDraw
- 主要面
- surface DirectDraw，翻转
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62aa80e6d040a26f16209e7fb75da6411489d2e8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817401"
---
# <a name="flipping"></a>交替


## <span id="ddk_flipping_gg"></span><span id="DDK_FLIPPING_GG"></span>


使用可通过前台缓冲区翻转的后台缓冲区是充分利用 DirectDraw 的最佳方式。 页面翻转对于游戏和视频播放中的平滑和自由自由动画非常重要。

*主要表面* 是要从中进行读取的内存区域，以绘制当前显示的屏幕。 如果主要表面有一个或多个附加缓冲区，则它是一个 *flippable* 图面。

翻转结构用于 DirectDraw 中的翻页。 从概念上讲，可以将它们视为表面的链接列表。 前台缓冲区为 "visible" 缓冲区。 后台缓冲区和所有附加的 flippable 表面必须与前台缓冲区大小和像素深度相同。 大多数新式显卡都有足够的内存，可用于在高分辨率模式下 flippable 前端和后台缓冲区。

所有类型的图面可以在 DirectDraw 中翻转;页面翻转是常见的特殊情况。 例如，翻转并不局限于支持叠加的卡片上的主表面，或具有纹理内存的支持3D 的显示卡。 在这些情况下，可以用相同的驱动程序入口点按照与主表面相同的方式翻转叠加和纹理。

不用于翻转的图面可以有任何尺寸，并可存储 nonflippable 对象（如图像数据）。 图像数据还可以存储在系统内存中，但在这种情况下，DirectDraw 可能会使用硬件仿真层 (HEL) ，因为硬件 blitters 通常无法访问系统内存来 array.blit 映像数据。 某些卡允许硬件 blitters 将 DMA)  (DMA 到系统内存，因此 DirectDraw 会检查 DMA。

下图说明两个 flippable 图面之间的关系。

![说明翻转的关系图](images/ddfig7.png)

如果前台缓冲区附加了一个或多个后台缓冲区，则它是一个 flippable 图面，如上图中所示。 后台缓冲区和所有附加的 flippable 表面必须与前台缓冲区大小和像素深度相同。 后台缓冲区表面使用翻转成为主要表面。 翻转只是更改指针，使其指向不同的 flippable 图面，从而显示新表面。 前台缓冲区 (不再是主表面) 随后可访问，并可向其写入新数据。

翻转解决了大多数屏幕闪烁问题。 呈现到未显示的表面的功能，这种功能可用于玩游戏和视频播放。

 

 





