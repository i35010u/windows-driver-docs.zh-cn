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
ms.openlocfilehash: 0b87f8af3137ba97a96f2d95cbb8d08e978b0003
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533556"
---
# <a name="color-control-initialization"></a>颜色控制初始化


## <span id="ddk_color_control_initialization_gg"></span><span id="DDK_COLOR_CONTROL_INITIALIZATION_GG"></span>


驱动程序的[ *DdControlColor* ](https://msdn.microsoft.com/library/windows/hardware/ff549244)函数控制的覆盖层和/或主表面的亮度/亮度控件。 若要启用颜色的控件功能，Microsoft DirectDraw HAL 必须执行以下操作在初始化时：

-   如果覆盖和/或主表面包含颜色的控件，设置 DDCAPS2\_COLORCONTROLOVERLAY 和/或 DDCAPS2\_COLORCONTROLPRIMAY 标志中**dwCaps2**的成员[ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248)中嵌入的结构[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)结构。

-   该驱动程序必须 DD 中指定一个函数\_HALINFO 结构 DirectDraw 可以调用以获取其他信息。 这中所述[ **DdGetDriverInfo**](https://msdn.microsoft.com/library/windows/hardware/ff549404)。

-   [ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)回调必须调用具有 GUID\_ColorControlCallbacks GUID 指定。 该驱动程序必须填写[ **DD\_COLORCONTROLCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff550521)结构相应的驱动程序的回调和标志设置，然后将复制到此结构**lpvData**输入结构中的成员。

 

 





