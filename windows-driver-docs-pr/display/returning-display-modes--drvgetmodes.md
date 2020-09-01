---
title: 返回显示模式 DrvGetModes
description: 返回显示模式 DrvGetModes
ms.assetid: 1010235a-0609-4380-8b83-7d8c649c2404
keywords:
- 显示驱动程序 WDK Windows 2000，桌面管理
- 桌面管理 WDK Windows 2000 显示器
- 返回显示模式 WDK Windows 2000 显示
- DrvGetModes
- 显示模式 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8029c83260543009b42bbdaaac7afff5de262f90
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064610"
---
# <a name="returning-display-modes-drvgetmodes"></a>返回显示模式：DrvGetModes


## <span id="ddk_returning_display_modes_drvgetmodes_gg"></span><span id="DDK_RETURNING_DISPLAY_MODES_DRVGETMODES_GG"></span>


显示驱动程序还必须支持 [**DrvGetModes**](/windows/desktop/api/winddi/nf-winddi-drvgetmodes)。 此函数为 GDI 提供指向 [**DEVMODEW**](/windows/desktop/api/wingdi/ns-wingdi-_devicemodew) 结构数组的指针。 结构为其支持的各种模式定义显示的属性，包括) 的维度 (、像素数、平面数、每个平面的位数、颜色信息等。

在调用 [**DrvGetModes**](/windows/desktop/api/winddi/nf-winddi-drvgetmodes) 函数时，驱动程序将可用显示模式写入内存的顺序可能会影响 Windows 选择的最终显示模式。 通常情况下，如果应用程序未指定默认模式，则系统将在驱动程序提供的列表中选择第一个匹配模式。

例如，假设当前显示模式为

800x600x32bpp@60Hz DMDO \_ 默认 DMDFO \_ 中心

驱动程序指定可用显示模式的列表，如下所示：

**A.** 600x800x32bpp@60Hz DMDO \_ 270 DMDFO \_ STRETCH

**B.** 600x800x32bpp@60Hz DMDO \_ 90 DMDFO \_ STRETCH

**Ansi-c.** 600x800x32bpp@60Hz DMDO \_ 90 DMDFO \_ CENTER

**D.** 600x800x32bpp@60Hz DMDO \_ 270 DMDFO \_ CENTER

**Case 1**

如果应用程序尝试将监视器设置为 600x800x32bpp@60Hz ，但 \_ \_ 没有在[**DEVMODEW**](/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)的**dmFields**成员中设置 dm DISPLAYORIENTATION 和 dm DISPLAYFIXEDOUTPUT 标志，则系统必须选择方向和固定输出模式。 在这种情况下，系统会选择显示模式 C，因为它是与当前 DMDFO CENTER 设置匹配的第一个列出的模式 \_ 。

**Case 2**

如果应用程序尝试将监视器设置为 600x800x32bpp@60Hz DMDFO \_ STRETCH，系统会选择显示模式 A。

**情况3**

如果应用程序尝试将监视器设置为 600x800x32bpp@60Hz DMDO \_ 270，系统会选择 "显示模式 D"。

**情况4**

如果应用程序尝试将监视器设置为 600x800x32bpp@60Hz DMDO \_ 默认值，系统将无法找到可接受的匹配项。

以下规则有一个例外：当系统寻找显示方向的匹配项，并且未指定方向且当前模式无法匹配时，系统将 \_ 对其他显示方向提供 DMDO 的默认优先级。

例如，假设当前显示模式为

600x800x32bpp@60Hz DMDO \_ 90 DMDFO \_ STRETCH

驱动程序指定可用显示模式的列表，如下所示：

**A.** 800x600x32bpp@60Hz DMDO \_ 180 DMDFO \_ CENTER

**B.** 800x600x32bpp@60Hz DMDO \_ 180 DMDFO \_ STRETCH

**Ansi-c.** 800x600x32bpp@60Hz DMDO \_ 默认 DMDFO \_ 中心

**D.** 800x600x32bpp@60Hz DMDO \_ 默认 DMDFO \_ STRETCH

在这种情况下，如果应用程序尝试将监视器设置为 800x600x32bpp@60Hz ，系统会选择 "显示模式 D"。

 

