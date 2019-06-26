---
title: 颜色控制初始化
description: 颜色控制初始化
ms.assetid: dd3afcaa-3da0-4515-8b8d-e7429792be23
keywords:
- 绘制 WDK DirectDraw，颜色控件初始化
- DirectDraw WDK Windows 2000 显示，颜色控件初始化
- 颜色控制初始化 WDK DirectDraw
- 初始化 DirectDraw 颜色控件
- DdControlColor
- 亮度 WDK DirectDraw
- 亮度 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8aa72adef70158452deef271bcd4dcf9e442f44c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370692"
---
# <a name="color-control-initialization"></a>颜色控制初始化


## <span id="ddk_color_control_initialization_gg"></span><span id="DDK_COLOR_CONTROL_INITIALIZATION_GG"></span>


驱动程序的[ *DdControlColor* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_colorcb_colorcontrol)函数控制的覆盖层和/或主表面的亮度/亮度控件。 若要启用颜色的控件功能，Microsoft DirectDraw HAL 必须执行以下操作在初始化时：

-   如果覆盖和/或主表面包含颜色的控件，设置 DDCAPS2\_COLORCONTROLOVERLAY 和/或 DDCAPS2\_COLORCONTROLPRIMAY 标志中**dwCaps2**的成员[ **DDCORECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)中嵌入的结构[ **DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构。

-   该驱动程序必须 DD 中指定一个函数\_HALINFO 结构 DirectDraw 可以调用以获取其他信息。 这中所述[ **DdGetDriverInfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)。

-   [ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)回调必须调用具有 GUID\_ColorControlCallbacks GUID 指定。 该驱动程序必须填写[ **DD\_COLORCONTROLCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_colorcontrolcallbacks)结构相应的驱动程序的回调和标志设置，然后将复制到此结构**lpvData**输入结构中的成员。

 

 





