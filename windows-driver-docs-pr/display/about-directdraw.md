---
title: 关于 DirectDraw
description: 关于 DirectDraw
ms.assetid: f2ab4863-8ec8-4eaf-b59f-635570aef470
keywords:
- 绘制 WDK DirectDraw，有关 DirectDraw
- DirectDraw WDK Windows 2000 显示，相关 DirectDraw 信息
- 消除 WDK DirectDraw
- 屏幕闪烁 WDK DirectDraw
- GDI WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e390ecaad27c60aac89329c271eb9cc3b7f20615
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562279"
---
# <a name="about-directdraw"></a>关于 DirectDraw


## <span id="ddk_about_directdraw_gg"></span><span id="DDK_ABOUT_DIRECTDRAW_GG"></span>


Microsoft DirectDraw 是显示组件的 Microsoft DirectX，软件设计人员可以直接操作显示内存、 硬件 blitters、 硬件叠加和翻转的图面。 DirectDraw 为游戏和三维图形数据包和数字视频编解码器，若要访问的特定显示设备功能等 Windows 子系统软件提供的独立于设备的方法。

DirectDraw 提供直接的 32 位路径中的特定于设备的显示功能的独立于设备的访问。 DirectDraw 调用中的驱动程序，而无需干预的 Windows 图形设备接口 (GDI) 或与设备无关位图 (DIB) 引擎直接访问显示卡的重要功能。

通过利用此直接的路径，游戏和其他显示密集型应用程序运行得更快，并避免撕裂现象。 一个*消除*是图像显示，并且在同一时间写入到由导致屏幕闪烁。 直接访问通常允许游戏性能会显示卡性能只受限于。 DirectDraw 还使用页翻转提供流畅的动画。

快速动作和不断变化的许多游戏和多媒体应用程序的屏幕上显示进程中放置一个沉重的负担并往往会加剧撕裂现象。 尽管 GDI 绘制电子表格、 图形、 TrueType 字体呈现等在非常快，但它不是应为实时图形 API。 DirectDraw 来处理依赖于设备的硬件加速功能中的 32 位驱动程序扩充 GDI。

 

 





