---
title: 桌面管理
description: 桌面管理
ms.assetid: 68ae302b-a39e-4aff-8be7-52081c318c9e
keywords:
- 显示驱动程序 WDK Windows 2000 中，桌面管理
- 桌面管理 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b9c1acb1bfc2933535941d60162c373e3a3801a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348891"
---
# <a name="desktop-management"></a>桌面管理


## <span id="ddk_desktop_management_gg"></span><span id="DDK_DESKTOP_MANAGEMENT_GG"></span>


显示驱动程序必须实现[ **DrvAssertMode** ](https://msdn.microsoft.com/library/windows/hardware/ff556178)并[ **DrvGetModes** ](https://msdn.microsoft.com/library/windows/hardware/ff556233)管理的桌面。

如果显示驱动程序是面板管理，它将接收到调用[ **DrvSetPalette** ](https://msdn.microsoft.com/library/windows/hardware/ff556282)重置其调色板到正确的状态。

在 Windows 2000 和更高版本的操作系统版本，GDI 的机制，用于处理动态模式下更改发生了显著变化。 在初始化期间分配给驱动程序 GDI HDEV 可能不同于分配模式下更改完成后 HDEV。 由于以下原因，显示器驱动程序通常将不受此更改：

-   驱动程序始终分配*ppdev-&gt;hdevEng = hdev*中其[ **DrvCompletePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556181)实现。

-   驱动程序始终引用*ppdev-&gt;hdevEng*需要 HDEV 任何回调中。

 

 





