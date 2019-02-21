---
title: 显示的颜色管理
description: 显示的颜色管理
ms.assetid: a0c3f35f-3741-4d5a-b7ae-dd177c719508
keywords:
- 显示驱动程序 WDK Windows 2000 中，颜色管理
- 显示颜色管理 WDK Windows 2000
- 显示图像颜色管理 WDK Windows 2000
- ICM WDK Windows 2000 显示
- gamma 斜坡 WDK Windows 2000 显示
- 颜色精确度 WDK Windows 2000 显示
- 显示实际颜色 WDK Windows 2000
- 校准颜色 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a9395da8b7007a77225667c99b8d9dbfbd5aa53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523234"
---
# <a name="color-management-for-displays"></a>显示的颜色管理


## <span id="ddk_color_management_for_displays_gg"></span><span id="DDK_COLOR_MANAGEMENT_FOR_DISPLAYS_GG"></span>


GDI 支持图像颜色管理 (ICM) 2.0 版。 显示器驱动程序可以使用 ICM，而无需实现任何特殊代码。

如果显示硬件支持*伽马*，显示驱动程序应实现[ **DrvIcmSetDeviceGammaRamp**](https://msdn.microsoft.com/library/windows/hardware/ff556243)。 需要颜色精确度颜色校准应用程序使用此功能。 DirectDraw 还使用此函数可将 DirectX 应用程序-如在 RGB 模式下执行调色板动画游戏-控制 gamma 负载增加。 有关示例代码，请参阅*Permedia*示例显示器驱动程序。

**请注意**   Microsoft Windows Driver Kit (WDK) 不包含 3Dlabs Permedia2 (*3dlabs.htm*) 和 3Dlabs Permedia3 (*Perm3.htm*) 示例显示器驱动程序。 你可以获取这些示例驱动程序从 Windows Server 2003 SP1 驱动程序开发工具包 (DDK)，可以从 DDK-WDHC 网站的 Windows 驱动程序开发工具包页面下载。

 

 

 





