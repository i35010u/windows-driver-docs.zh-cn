---
title: 关于 DirectDraw
description: 关于 DirectDraw
keywords:
- 绘制 WDK DirectDraw，关于 DirectDraw
- DirectDraw WDK Windows 2000 显示，大约 DirectDraw
- 泪水 WDK DirectDraw
- 屏幕闪烁 WDK DirectDraw
- GDI WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 933c2f7bf197e22f44bca24a4803045769f50b1d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810583"
---
# <a name="about-directdraw"></a>关于 DirectDraw


## <span id="ddk_about_directdraw_gg"></span><span id="DDK_ABOUT_DIRECTDRAW_GG"></span>


Microsoft DirectDraw 是 Microsoft DirectX 的显示组件，使软件设计人员能够直接处理显示内存、硬件 blitters、硬件重叠和翻转表面。 DirectDraw 为游戏和 Windows 子系统软件（如3D 图形包和数字视频编解码器）提供与设备无关的方式，以获得对特定显示设备功能的访问权限。

DirectDraw 为直接32位路径中的设备特定显示功能提供与设备无关的访问。 DirectDraw 调用直接访问显示卡的驱动程序中的重要函数，而不会干预 Windows 图形设备接口 (GDI) 或与设备无关的位图 (DIB) 引擎。

通过利用此直接路径，游戏和其他显示密集型应用程序的运行速度更快，并避免了撕裂。 " *撕* " 是一种屏幕闪烁，这是由同时显示并写入图像的。 直接访问通常允许游戏性能仅受到显示卡性能的限制。 DirectDraw 还使用页面翻转来提供平滑动画。

许多游戏和多媒体应用程序的快速运动和不断变化的屏幕对显示过程产生了沉重的负担，并且往往恶化撕裂。 尽管 GDI 在绘图电子表格、图形、TrueType 字体呈现等操作上速度非常快，但并不是一种实时图形 API。 DirectDraw 通过在32位驱动程序中处理与设备相关的硬件加速器功能来增强 GDI。

 

 





