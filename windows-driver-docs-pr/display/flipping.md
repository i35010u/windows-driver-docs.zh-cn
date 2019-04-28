---
title: 交替
description: 交替
ms.assetid: e577b73f-7664-4c87-8d43-c3cf04705081
keywords:
- 消除 WDK DirectDraw
- 绘图页上有关翻转翻转 WDK DirectDraw
- DirectDraw 翻转 WDK Windows 2000 显示，有关翻转
- 页翻转 WDK DirectDraw，有关翻转
- 有关翻转翻转 WDK DirectDraw
- 翻转 WDK DirectDraw 绘图页面
- DirectDraw 翻转 WDK Windows 2000 显示
- 页翻转 WDK DirectDraw
- 翻转 WDK DirectDraw
- 主图面 WDK DirectDraw
- 显示 WDK DirectDraw 翻转
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51eb8efb73a02b29987bab0afeed9b12b2234297
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338662"
---
# <a name="flipping"></a>交替


## <span id="ddk_flipping_gg"></span><span id="DDK_FLIPPING_GG"></span>


使用与前台缓冲区可以翻转的后台缓冲区是充分利用 DirectDraw 的最佳方式。 翻页，对于在游戏和视频播放平滑、 免拆解动画至关重要。

*主表面*是从硬盘读出绘制当前显示在屏幕的内存的区域。 如果主面有一个或多个附加的后台缓冲区，则*flippable*图面。

DirectDraw 中翻页用于翻转的结构。 从概念上讲，它们可以认为的链接列表的图面进行。 前台缓冲区是"可见"缓冲区。 后台缓冲区和所有附加 flippable 图面必须是前台缓冲区相同的大小和像素深度。 大多数新式图形卡高分辨率模式中有足够内存用于 flippable 前端和后台缓冲区。

可以在 DirectDraw; 翻转所有类型的图面页翻转是常见的特殊情况。 例如，翻转并不局限于支持覆盖，卡上的主图面或 3d 能够显示具有纹理内存卡。 在这些情况下，可以在主面，相同的驱动程序的入口点的方式相同翻转叠加和纹理。

不用于翻转的图面可以有任何维度，并且可存储 nonflippable 对象，例如图像数据。 此外可以将图像数据存储在系统内存中，但在这种情况下 DirectDraw 可能使用硬件仿真层 (HEL)，因为硬件 blitters 通常无法访问到位块的图像数据的系统内存。 某些卡允许硬件 blitters 个直接内存访问 (DMA) 到系统内存，因此 DirectDraw DMA 时进行检查。

下图说明了两个 flippable 图面之间的关系。

![阐释翻转关系图](images/ddfig7.png)

如果前台缓冲区有一个或多个附加的后台缓冲区，它是 flippable 的图面上，在上图中所示。 后台缓冲区和所有附加 flippable 图面必须是前台缓冲区相同的大小和像素深度。 后台缓冲区面将成为使用翻转在主图面。 翻转只需更改一个指针，使其指向不同的 flippable 图面，从而显示新的图面。 前台缓冲区 （这不再是主图面） 然后变得可以访问，并可以有新数据写入到它。

翻转解决了大多数屏幕闪烁问题。 不显示图面上呈现的能力使玩游戏和视频播放流畅、 无拆解的动画。

 

 





