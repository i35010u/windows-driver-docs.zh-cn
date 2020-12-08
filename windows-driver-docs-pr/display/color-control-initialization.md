---
title: 颜色控制初始化
description: 颜色控制初始化
keywords:
- 绘制 WDK DirectDraw，颜色控件初始化
- DirectDraw WDK Windows 2000 显示，颜色控件初始化
- 颜色控制初始化 WDK DirectDraw
- 初始化 DirectDraw 颜色控制
- DdControlColor
- 亮度 WDK DirectDraw
- 亮度 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 989c47c700dde803ec060682e09ccb4e8f3e0090
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810291"
---
# <a name="color-control-initialization"></a>颜色控制初始化


## <span id="ddk_color_control_initialization_gg"></span><span id="DDK_COLOR_CONTROL_INITIALIZATION_GG"></span>


驱动程序的 [*DdControlColor*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_colorcb_colorcontrol) 函数控制叠加和/或主图面的亮度/亮度控件。 若要启用颜色控制功能，Microsoft DirectDraw HAL 必须在初始化时执行以下操作：

-   如果覆盖面和/或主表面包含颜色控件，请 \_ \_ 在嵌入在 [**DD \_ DwCaps2**](/windows/win32/api/ddrawint/ns-ddrawint-dd_halinfo)结构中的 [**DDCORECAPS**](/windows/win32/api/ddrawi/ns-ddrawi-ddcorecaps)结构的 **HALINFO** 成员中设置 DDCAPS2 COLORCONTROLOVERLAY 和/或 DDCAPS2 COLORCONTROLPRIMAY 标志。

-   驱动程序必须在 DD HALINFO 结构中指定一个函数 \_ ，该函数用于获取其他信息。 [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)中对此进行了介绍。

-   必须用指定的 GUID ColorControlCallbacks GUID 调用 [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) 回调 \_ 。 驱动程序必须使用适当的驱动程序回调和 flags 集填充 [**DD \_ COLORCONTROLCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_colorcontrolcallbacks) 结构，然后将该结构复制到输入结构的 **lpvData** 成员。

 

