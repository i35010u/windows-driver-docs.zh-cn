---
title: Windows 2000 的显示器体系结构
description: Windows 2000 的显示器体系结构
ms.assetid: c18e1464-13b7-4e55-b3e1-77aaf9270f60
keywords:
- VGA WDK Windows 2000 显示
- 显示器驱动程序模型 WDK Windows 2000 中，体系结构
- Windows 2000 显示器驱动程序模型 WDK，体系结构
- 体系结构 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c9d1bb10a8645cb33cbdcc884d5d195ddd28f60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522981"
---
# <a name="windows-2000-display-architecture"></a>Windows 2000 的显示器体系结构


## <span id="ddk_display_architecture_gg"></span><span id="DDK_DISPLAY_ARCHITECTURE_GG"></span>


下图显示了所需显示在 Windows 2000 及更高版本的组件。

![说明 windows 2000 及更高版本的关系图显示子系统](images/dpy1.png)

在上图中的阴影的元素表示 Windows 2000 和更高版本提供的服务。 无阴影的元素指示一个第三方显示驱动程序和视频的微型端口驱动程序所需顺序显示在 Windows 2000 和更高版本系统的图形适配器。

对于每种类型的图形卡，可使用基于 NT 的操作系统的系统，必须显示驱动程序和相应的微型端口驱动程序。 微型端口驱动程序是专门针对一个图形适配器 （或系列的适配器） 编写的。 可以为任意数量的共享一个通用的图形界面; 适配器编写显示驱动程序例如，可以通过 VGA 或 ET4000 微型端口驱动程序使用 VGA 显示器驱动程序。 这是因为显示驱动程序绘制而微型端口驱动程序执行操作，如模式集，并提供有关向驱动程序硬件的信息。 还有可能用于多个显示器驱动程序以使用特定的微型端口驱动程序;例如，16 和 256 色 SVGA 显示器驱动程序可以使用相同的微型端口驱动程序。

以下各节介绍显示和视频的微型端口驱动程序的主要职责。 中的职责分解不是硬和快速;模块性和性能之间的平衡是关键。 例如，VGA 驱动程序的硬件指针代码驻留在微型端口驱动程序。 这促进了模块化，因此相同的显示驱动程序可以处理视频七个 vram 能够，它具有硬件指针，以及 ET4000，这不会执行。

[Windows 2000 显示驱动程序责任](windows-2000-display-driver-responsibilities.md)

[Windows 2000 视频微型端口驱动程序责任](windows-2000-video-miniport-driver-responsibilities.md)

 

 





