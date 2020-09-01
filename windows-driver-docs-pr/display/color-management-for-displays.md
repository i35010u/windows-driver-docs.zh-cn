---
title: 显示颜色管理
description: 显示颜色管理
ms.assetid: a0c3f35f-3741-4d5a-b7ae-dd177c719508
keywords:
- 显示驱动程序 WDK Windows 2000，颜色管理
- 颜色管理 WDK Windows 2000 显示
- 图像颜色管理 WDK Windows 2000 显示
- ICM WDK Windows 2000 显示
- 伽玛斜坡 WDK Windows 2000 显示器
- color exactness WDK Windows 2000 显示器
- 完全颜色 WDK Windows 2000 显示
- 校准颜色 WDK Windows 2000 显示器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94ec429ce1d02bf8226950844155979354b42791
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065266"
---
# <a name="color-management-for-displays"></a>显示颜色管理


## <span id="ddk_color_management_for_displays_gg"></span><span id="DDK_COLOR_MANAGEMENT_FOR_DISPLAYS_GG"></span>


GDI 支持 (ICM) 版本2.0 的图像颜色管理。 显示驱动程序可以使用 ICM，无需实现任何特殊代码。

如果显示硬件支持 *伽玛斜坡*，则显示驱动程序应实现 [**DrvIcmSetDeviceGammaRamp**](/windows/desktop/api/winddi/nf-winddi-drvicmsetdevicegammaramp)。 需要颜色 exactness 的颜色校准应用程序使用此功能。 DirectDraw 还使用此函数允许 DirectX 应用程序（例如在 RGB 模式下执行调色板动画的游戏）控制伽玛斜坡。 有关代码示例，请参阅 *Permedia* 示例显示驱动程序。

**注意**   Microsoft Windows 驱动程序工具包 (WDK) 不包含 3Dlabs Permedia2 (*3dlabs.htm*) 和 3Dlabs *Permedia3 (Perm3.htm) 示例*显示驱动程序。 你可以从 Windows Server 2003 SP1 驱动程序开发工具包中获取这些示例驱动程序 (DDK) ，你可以从 WDHC 网站的 "Windows 驱动程序开发工具包" 页下载。

 

 

