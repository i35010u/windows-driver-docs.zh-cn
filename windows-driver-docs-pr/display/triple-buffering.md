---
title: 三重缓冲
description: 三重缓冲
keywords:
- 绘图页反向 WDK DirectDraw，三缓冲
- DirectDraw 翻转 WDK Windows 2000 显示，三缓冲
- 页面翻转 WDK DirectDraw，三缓冲
- 翻转 WDK DirectDraw，三缓冲
- 三倍缓冲 WDK DirectDraw
- 缓冲 WDK DirectDraw
- surface DirectDraw，翻转
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe7d0ac3d9865f83ca25580c352451f9b81e59b9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802581"
---
# <a name="triple-buffering"></a>三重缓冲


## <span id="ddk_triple_buffering_gg"></span><span id="DDK_TRIPLE_BUFFERING_GG"></span>


增加可容纳主图面的缓冲区数量会增加显示性能。 最好至少有三个 flippable 图面 (一些游戏使用5个或更多) 。 如果只有两个面并发生页面翻转，则显示将延迟，直到监视器的垂直回描完成。 需要延迟以确保后台缓冲区在完成显示之前不会写入。 使用三次缓冲时，第三个图面始终是可写的，因为它是一个后台缓冲区，可立即在 (上绘制，如下图所示) 。 在不使用 sprite 内存的游戏中，使用三次缓冲的三维渲染比双缓冲快20% 到30%。

![阐释三次缓冲的图示](images/ddfig9.png)

上图中的翻转结构与 [撕裂](tearing.md)的结构相同，只使用了三个缓冲区。 一个缓冲区几乎始终是可写的 (因为它不涉及到反向) ，因此，驱动程序不必等待显示扫描完成，就允许再次写入后台缓冲区。

下面是使用上图中的标签在三缓冲系统中翻转和 blitting 的简短说明。 该示例从显示的图面像素内存11开始。 这是由 Microsoft Windows 驱动程序开发工具包（DDK）) 提供的示例代码中的前台缓冲区 (**fpVidMem** 的主要 \[ 表面 \] 。 在某些时候，需要在像素内存22中 blt 图面。 由于 **fpVidMem** 指向从 11 (不是 22) 的图面，翻转状态为 false (请求的表面) 上不发生翻转，blt 可以继续。 驱动程序会锁定图面、向其中写入数据，然后将其解除锁定。 若要显示该表面，必须进行翻转。

DirectDraw 前台缓冲区对象现在可以将 **fpVidMem** 更改 (显示内存指针) ，使图面的22成为主要表面。 由于没有挂起的翻转，将交换显示指针 (查看上图) 的下半部分，并将翻转状态设置为 **TRUE**。 前台缓冲区现在指向 surface 象素内存22，后台缓冲区指向 surface 象素 memory 33，而第三个缓冲区对象指向曲面像素内存 11 (旧的主表面) 。 与双缓冲不同，DirectDraw 此时可随意写入后台缓冲区。 换句话说，DirectDraw 可以写入 surface 像素内存33，因为没有任何翻转处于挂起状态。 此循环过程会不断地持续下去，为使用 DirectDraw 的应用程序提供平滑动画和更快的游戏播放和视频播放。

 

 





