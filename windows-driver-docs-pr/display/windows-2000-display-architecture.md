---
title: Windows 2000 显示体系结构
description: Windows 2000 显示体系结构
keywords:
- VGA WDK Windows 2000 显示器
- 显示驱动程序模型 WDK Windows 2000、体系结构
- Windows 2000 显示器驱动程序模型 WDK，体系结构
- 体系结构 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b8e4f2320af3a98facf21005fe680da040d804f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826019"
---
# <a name="windows-2000-display-architecture"></a>Windows 2000 显示体系结构


## <span id="ddk_display_architecture_gg"></span><span id="DDK_DISPLAY_ARCHITECTURE_GG"></span>


下图显示了在 Windows 2000 和更高版本上显示的组件。

![说明 windows 2000 和更高版本的显示子系统的关系图](images/dpy1.png)

上图中的阴影元素表示 Windows 2000 和更高版本中提供的服务。 Unshaded 元素指示需要第三方显示器驱动程序和视频微型端口驱动程序，以便在 Windows 2000 和更高版本的系统中显示图形适配器。

对于可用于基于 NT 的操作系统的每种类型的图形卡，都必须有显示驱动程序和相应的视频微型端口驱动程序。 小型端口驱动程序专用于一个图形适配器 (或适配器系列) 。 可以为共享公共绘图接口的任意数量的适配器编写显示驱动程序;例如，VGA 显示器驱动程序可用于 VGA 或 ET4000 微型端口驱动程序。 这是因为显示器驱动程序会绘制，而微型端口驱动程序执行操作（如模式集），并向驱动程序提供有关硬件的信息。 对于一个特定微型端口驱动程序，也可以使用多个显示驱动程序;例如，16和256色 SVGA 显示驱动程序可以使用相同的微型端口驱动程序。

以下部分描述了显示和视频微型端口驱动程序的主要职责。 责任的细分不是很难实现;模块化和性能之间的平衡是关键所在。 例如，VGA 驱动程序的硬件指针代码驻留在微型端口驱动程序中。 这会升级模块，因此，同一显示器驱动程序可以处理包含硬件指针的视频七个 VRAM 和 ET4000，而不是。

[Windows 2000 显示驱动程序的责任](windows-2000-display-driver-responsibilities.md)

[Windows 2000 视频微型端口驱动程序的责任](windows-2000-video-miniport-driver-responsibilities.md)

 

 





