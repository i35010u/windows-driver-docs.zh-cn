---
title: 返回显示模式 DrvGetModes
description: 返回显示模式 DrvGetModes
ms.assetid: 1010235a-0609-4380-8b83-7d8c649c2404
keywords:
- 显示驱动程序 WDK Windows 2000 中，桌面管理
- 桌面管理 WDK Windows 2000 显示
- 返回 WDK Windows 2000 显示的显示模式
- DrvGetModes
- 显示模式 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20ffe555a994a8b2dd479190f5475db89751da78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523832"
---
# <a name="returning-display-modes-drvgetmodes"></a>返回显示模式：DrvGetModes


## <span id="ddk_returning_display_modes_drvgetmodes_gg"></span><span id="DDK_RETURNING_DISPLAY_MODES_DRVGETMODES_GG"></span>


显示驱动程序还必须支持[ **DrvGetModes**](https://msdn.microsoft.com/library/windows/hardware/ff556233)。 此函数为数组提供 GDI 指针[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)结构。 结构定义支持，其中包括维度 （以像素为单位和毫米为单位）、 平面数、 每个平面，颜色信息和等等的位的各种模式的显示的属性。

该驱动程序会写入内存的可用显示模式的顺序时[ **DrvGetModes** ](https://msdn.microsoft.com/library/windows/hardware/ff556233)调用函数可能会影响 Windows 选择的最后一个显示模式。 一般情况下，如果应用程序未指定默认模式，系统将提供的驱动程序列表中选择的第一个匹配模式。

例如，假设当前显示模式下是

800x600x32bpp@60Hz DMDO\_默认 DMDFO\_CENTER

和驱动程序指定的可用显示模式列表，如下所示：

**A.** 600x800x32bpp@60Hz DMDO\_270 DMDFO\_STRETCH

**B.** 600x800x32bpp@60Hz DMDO\_90 DMDFO\_STRETCH

**C.** 600x800x32bpp@60Hz DMDO\_90 DMDFO\_CENTER

**D.** 600x800x32bpp@60Hz DMDO\_270 DMDFO\_CENTER

**案例 1**

如果应用程序尝试将监视器设置为600x800x32bpp@60Hz，但 DM\_DISPLAYORIENTATION 和 DM\_DISPLAYFIXEDOUTPUT 标志未设置**dmFields**隶属[ **DEVMODEW**](https://msdn.microsoft.com/library/windows/hardware/ff552837)，系统必须选择方向和固定输出模式。 在这种情况下系统将选择显示模式 C，因为它与当前 DMDFO 相匹配的第一个列出的模式\_CENTER 设置。

**情况 2**

如果应用程序尝试将监视器设置为600x800x32bpp@60HzDMDFO\_STRETCH，系统会选择显示模式 a。

**案例 3**

如果应用程序尝试将监视器设置为600x800x32bpp@60HzDMDO\_270，系统会选择显示模式 d。

**用例 4**

如果应用程序尝试将监视器设置为600x800x32bpp@60HzDMDO\_默认情况下，系统将无法找到可接受匹配的项。

适用于这些规则的一个例外： 当系统查找匹配项的显示方向和未指定方向，当前的模式无法进行匹配，系统会使 DMDO\_默认的优先级高于其他显示方向。

例如，假设当前显示模式下是

600x800x32bpp@60Hz DMDO\_90 DMDFO\_STRETCH

和驱动程序指定的可用显示模式列表，如下所示：

**A.** 800x600x32bpp@60Hz DMDO\_180 DMDFO\_CENTER

**B.** 800x600x32bpp@60Hz DMDO\_180 DMDFO\_STRETCH

**C.** 800x600x32bpp@60Hz DMDO\_默认 DMDFO\_CENTER

**D.** 800x600x32bpp@60Hz DMDO\_默认 DMDFO\_STRETCH

在此情况下，如果应用程序尝试将监视器设置为800x600x32bpp@60Hz，系统会选择显示模式 d。

 

 





