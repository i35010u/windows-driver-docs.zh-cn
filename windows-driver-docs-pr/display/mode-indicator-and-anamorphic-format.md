---
title: 模式指示器和变形格式
description: 模式指示器和变形格式
keywords:
- DirectX VPE 支持 WDK DirectDraw，并显示隔行扫描视频
- 绘制 VPEs WDK DirectDraw 并显示交错视频
- DirectDraw VPEs WDK Windows 2000 显示，显示交错视频
- 视频端口扩展 WDK DirectDraw，显示交错视频
- VPEs WDK DirectDraw，显示交错视频
- 显示隔行扫描视频
- 交错视频显示 WDK 视频端口扩展
- anamorphic 格式 WDK DirectDraw
- bob WDK DirectDraw
- 编织 WDK DirectDraw
- 边缘-自适应筛选 WDK DirectDraw
- 模式指示器 WDK DirectDraw
- 不规则 3 2 模式 WDK DirectDraw
- REPEAT_FIELD
- 自动显示更改 WDK DirectDraw
- 取消隔行扫描 WDK 视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edce27a6e402ff424b8a860f1e73993d420b3d38
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821520"
---
# <a name="mode-indicator-and-anamorphic-format"></a>模式指示器和变形格式


## <span id="ddk_mode_indicator_and_anamorphic_format_gg"></span><span id="DDK_MODE_INDICATOR_AND_ANAMORPHIC_FORMAT_GG"></span>


良好的驱动程序设计要求使用 bob、编织和边缘自适应筛选的组合。 动作检测电路可以动态控制每种方法在每个像素上的使用程度。 遗憾的是，显示逻辑来实现这样做很难实现，除非有其他数据可用。 随着大型计算机级显示的不断提高的可用性，操作系统还需要此额外数据，以确保基本图形电路能可靠地提供最佳图片。

在 DVD 世界中，可能会有许多格式组合到一个磁盘上。 可能有每秒24帧的电影编辑为525/60 视频，然后编辑为每秒30帧。 每次进行此类编辑时，它可能会更改数据的最佳显示方式。 当前 DVD 规范不确保在显示系统中处理这种混合格式的良好性能。

另一种可能的情况是显示电影，其中重复 \_ 字段标志因错误而不规则或不存在。 当编码器尝试解释不规则的3:2 模式时，它会尝试重新获取同步，但这可能会杂乱。 完全可以使用重复 \_ 字段标志的显示从编织模式更改为 bob 模式，反之亦然，无论是在拍摄过程中，都是如此。 这会对查看器显示错误。

若要显示具有偶然3:2 模式 irregularity 的电影，一种很好的方法是从编织模式切换到 bob 模式，并返回到环绕 irregularity 的拍摄剪切。 在其他情况下，最好是特别标识新模式的第一个字段对并保持编织模式。

可以想象到许多内容方案。 某些自动显示方案的工作方式比其他方案更好，具体取决于所涉及的特定内容。 可能只有某些内容提供商才能保证最大范围的播放平台的最佳结果。 DirectShow 为这些内容作者提供了一个方法，用于判断显示模式对其标题的影响并传送其首选项。

 

 





