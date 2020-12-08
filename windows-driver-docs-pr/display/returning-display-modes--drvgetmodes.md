---
title: 返回显示模式 DrvGetModes
description: 返回显示模式 DrvGetModes
keywords:
- 显示驱动程序 WDK Windows 2000，桌面管理
- 桌面管理 WDK Windows 2000 显示器
- 返回显示模式 WDK Windows 2000 显示
- DrvGetModes
- 显示模式 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c9d7e894b25bfee5b7e9dbd402b86e64bececdb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824175"
---
# <a name="returning-display-modes-drvgetmodes"></a>返回显示模式：DrvGetModes

显示驱动程序还必须支持 [**DrvGetModes**](/windows/win32/api/winddi/nf-winddi-drvgetmodes)。 此函数为 GDI 提供指向 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew) 结构数组的指针。 结构为其支持的各种模式定义显示的属性，包括) 的维度 (、像素数、平面数、每个平面的位数、颜色信息等。

在调用 [**DrvGetModes**](/windows/win32/api/winddi/nf-winddi-drvgetmodes) 函数时，驱动程序将可用显示模式写入内存的顺序可能会影响 Windows 选择的最终显示模式。 通常情况下，如果应用程序未指定默认模式，则系统将在驱动程序提供的列表中选择第一个匹配模式。

例如，假设当前显示模式为

800x600x32bpp@60Hz DMDO_DEFAULT DMDFO_CENTER

驱动程序指定可用显示模式的列表，如下所示：

| “模式” | 模式详细信息 |
| ---- | ------------ |
| **A** | 600x800x32bpp@60Hz DMDO_270 DMDFO_STRETCH |
| **B** | 600x800x32bpp@60Hz DMDO_90 DMDFO_STRETCH |
| **C** | 600x800x32bpp@60Hz DMDO_90 DMDFO_CENTER |
| **D** | 600x800x32bpp@60Hz DMDO_270 DMDFO_CENTER |

* **Case 1**

  如果应用程序尝试将监视器设置为 600x800x32bpp@60Hz ，但没有在 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew)的 **dmFields** 成员中设置 DM_DISPLAYORIENTATION 和 DM_DISPLAYFIXEDOUTPUT 标志，则系统必须选择方向和固定输出模式。 在这种情况下，系统会选择显示模式 **C** ，因为它是与当前 DMDFO_CENTER 设置匹配的第一个列出的模式。

* **Case 2**

  如果应用程序尝试将监视器设置为 " 600x800x32bpp@60Hz DMDFO_STRETCH"，系统会选择 "显示模式 **A**"。

* **情况3**

  如果应用程序尝试将监视器设置为 " 600x800x32bpp@60Hz DMDO_270"，系统会选择 "显示模式 **D**"。

* **情况4**

  如果应用程序尝试将监视器设置为 600x800x32bpp@60Hz DMDO_DEFAULT，系统将无法找到可接受的匹配项。

有一个例外情况适用于这些规则：当系统寻找显示方向的匹配项，并且未指定方向且当前模式无法匹配时，系统将提供与其他显示方向 DMDO_DEFAULT 优先级。

例如，假设当前显示模式为

600x800x32bpp@60Hz DMDO_90 DMDFO_STRETCH

驱动程序指定可用显示模式的列表，如下所示：

| “模式” | 模式详细信息 |
| ---- | ------------ |
| **A** | 800x600x32bpp@60Hz DMDO_180 DMDFO_CENTER |
| **B** | 800x600x32bpp@60Hz DMDO_180 DMDFO_STRETCH |
| **C** | 800x600x32bpp@60Hz DMDO_DEFAULT DMDFO_CENTER |
| **D** | 800x600x32bpp@60Hz DMDO_DEFAULT DMDFO_STRETCH |

在这种情况下，如果应用程序尝试将监视器设置为 800x600x32bpp@60Hz ，系统会选择 "显示模式 **D**"。
