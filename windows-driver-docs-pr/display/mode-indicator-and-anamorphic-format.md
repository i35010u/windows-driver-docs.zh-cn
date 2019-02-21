---
title: 模式指示器和变形格式
description: 模式指示器和变形格式
ms.assetid: b297c62e-3b7e-47de-95a5-c25e8fc5ad56
keywords:
- DirectX VPE 支持 WDK DirectDraw，显示交错的视频
- 绘制 VPEs WDK DirectDraw，显示交错视频
- DirectDraw VPEs WDK Windows 2000 显示，显示交错的视频
- 视频端口扩展 WDK DirectDraw，显示交错的视频
- VPEs WDK DirectDraw，显示交错的视频
- 显示交错的视频
- 交错的视频显示 WDK 的视频端口扩展
- 变形格式 WDK DirectDraw
- bob WDK DirectDraw
- 将 WDK DirectDraw
- 边缘自适应筛选 WDK DirectDraw
- 模式指示器 WDK DirectDraw
- 不规则 3 2 模式 WDK DirectDraw
- REPEAT_FIELD
- 自动显示对 WDK DirectDraw 的更改
- 取消隔行扫描 WDK 的视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e9917246c79fa460fbbf7204e34dce5a93c8773
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534467"
---
# <a name="mode-indicator-and-anamorphic-format"></a>模式指示器和变形格式


## <span id="ddk_mode_indicator_and_anamorphic_format_gg"></span><span id="DDK_MODE_INDICATOR_AND_ANAMORPHIC_FORMAT_GG"></span>


很好的驱动程序设计调用 bob、 织物，和边缘自适应筛选的组合。 动作检测电路可以动态控制向其每种技术使用在逐像素的基础的程度。 遗憾的是，显示逻辑来实现此目的很难执行，除非使某些其他数据可用。 与可用性的提高大型计算机级显示，操作系统需要这些额外的数据，以确保该基本图形电路可以可靠地提供最佳的图片。

在 DVD 的世界中，它应该有多种格式，将组合在一个磁盘上。 可能有每第二个电影 525/60 视频编辑，然后编辑为每第二个电影胶片的 30 帧的 24 帧。 此类编辑发生，每次它可能会更改数据的最佳显示方式。 当前 DVD 规范不能确保用于显示系统中处理这种混合的格式良好的性能。

另一种情形是电影胶片的显示位置重复\_字段标志是不规则或不存在由于出现错误。 当编码器尝试解释不规则 3:2 模式时，它会尝试重新获取同步，但这可能比较混乱。 完全有可能遵循重复显示\_字段标志，用于从更改将模式设置为 bob 模式下，或者反之亦然，按原义中间截图。 这将查找到查看器错误。

显示具有偶尔 3:2 模式不一致情况是从切换电影胶片的好办法将模式将 bob 模式以及在快捷方式括住的不一致情况。 在其他情况下，它可能是最佳以特别标识新模式的第一个字段对和维护 weave 实现模式。

一个可以想象，许多内容的方案。 某些自动显示方案工作比其他具体取决于所涉及的特定内容更好。 很可能仅某些内容提供程序，将看到需要保证的播放平台上最广泛的最佳结果。 DirectShow 提供这些内容编写者参与评判： 在其标题的显示模式的影响的方法，并将传输其首选项。

 

 





