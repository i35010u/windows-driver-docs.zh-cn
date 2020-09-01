---
title: 桌面管理
description: 桌面管理
ms.assetid: 68ae302b-a39e-4aff-8be7-52081c318c9e
keywords:
- 显示驱动程序 WDK Windows 2000，桌面管理
- 桌面管理 WDK Windows 2000 显示器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b91da4ed9cf74d49ee118b3c5fa346bbff2fecb9
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065922"
---
# <a name="desktop-management"></a>桌面管理


## <span id="ddk_desktop_management_gg"></span><span id="DDK_DESKTOP_MANAGEMENT_GG"></span>


显示驱动程序必须实现 [**DrvAssertMode**](/windows/desktop/api/winddi/nf-winddi-drvassertmode) 和 [**DrvGetModes**](/windows/desktop/api/winddi/nf-winddi-drvgetmodes) 来管理桌面。

如果显示驱动程序由面板管理，则它还会接收到 [**DrvSetPalette**](/windows/desktop/api/winddi/nf-winddi-drvsetpalette) 的调用，以将其调色板重置为正确的状态。

在 Windows 2000 和更高版本的操作系统版本中，GDI 用于处理动态模式更改的机制已发生显著变化。 在初始化期间分配给驱动程序的 GDI HDEV 可能不同于在模式更改完成后分配的 HDEV。 显示驱动程序通常不受此更改的影响，原因如下：

-   驱动程序在其[**DrvCompletePDEV**](/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)实现中始终分配了*ppdev- &gt; hdevEng = hdev* 。

-   在需要 HDEV 的任何回调中，驱动程序始终引用 *ppdev- &gt; hdevEng* 。

 

