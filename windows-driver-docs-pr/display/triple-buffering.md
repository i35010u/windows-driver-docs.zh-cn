---
title: 三重缓冲
description: 三重缓冲
ms.assetid: 4651f9d2-09fb-4006-8243-403f564414f5
keywords:
- 绘图页上翻转 WDK DirectDraw、 三重缓冲
- DirectDraw 翻转 WDK Windows 2000 显示三重缓冲
- 页翻转 WDK DirectDraw、 三重缓冲
- 翻转 WDK DirectDraw，三重缓冲
- 三重缓冲 WDK DirectDraw
- 缓冲区 WDK DirectDraw
- 显示 WDK DirectDraw 翻转
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 408b3f6aeeca0dda36486f526dcb6ce56c83bf15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545835"
---
# <a name="triple-buffering"></a>三重缓冲


## <span id="ddk_triple_buffering_gg"></span><span id="DDK_TRIPLE_BUFFERING_GG"></span>


增加缓冲区可以容纳主面数会增加显示性能。 最好具有至少三个 flippable 应用层协议 （某些游戏使用五个或多个）。 当有只有两个图面并翻页时，显示延迟，直到监视器的垂直回退操作已完成。 延迟是必须以确保在完成之前，后台缓冲区未编写上显示。 使用三重缓冲，第三个面始终是可写，因为它是后台缓冲区，并可用于立即 （如在下图中所示） 上绘制。 在不使用子画面内存游戏中，使用三重缓冲的 3D 渲染为 20 到 30%快于双缓冲。

![说明三重缓冲的关系图](images/ddfig9.png)

在上图中的翻转结构将与中的相同[Tearing](tearing.md)、 唯一现在都在使用三个缓冲区。 一个缓冲区几乎始终是可写 （因为它不涉及翻转） 使该驱动程序无需等待显示扫描，以允许后台缓冲区，以再次写入之前完成。

下面是在三重缓冲系统中，使用前图所示的标签中翻转和平面闪的简要说明。 该示例首先图面上的像素内存显示 11。 这是主表面指向前台缓冲区 (**fpVidMem**示例代码中提供与 Microsoft Windows 驱动程序开发工具包\[DDK\])。 在某些时候，它将成为到像素内存 22 面 blt 希望。 因为**fpVidMem**指向 11 (而不是 22) 和 flip 状态开始的图面上为 false （不翻转发生请求的图面上），blt 可以继续执行。 驱动程序锁定在图面，向其中写入，然后将其解锁。 若要显示该图面，必须进行翻转。

DirectDraw 前台缓冲区对象现在可以更改**fpVidMem** （显示内存指针） 进行 22 面主图面。 没有翻转处于挂起状态，因为交换显示指针 （参见底部上图的下半部分），和翻转的状态设置为 **，则返回 TRUE**。 前台缓冲区现在指向图面上的像素内存 22、 后台缓冲区指向图面上的像素内存 33 和图面上的像素内存 11 （旧的主面） 的第三个缓冲区对象点。 与使用双缓冲 DirectDraw 是免费的这一次写入到后台缓冲区。 换而言之，DirectDraw 可以写入图面上的像素内存 33，因为没有翻转处于挂起状态。 此循环的翻转过程将无休止地继续提供流畅的动画和更快地玩游戏和视频播放的应用程序都使用 DirectDraw。

 

 





