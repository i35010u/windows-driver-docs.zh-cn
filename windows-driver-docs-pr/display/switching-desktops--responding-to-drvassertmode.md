---
title: 切换到 DrvAssertMode 响应的桌面
description: 切换到 DrvAssertMode 响应的桌面
ms.assetid: 0e37050f-63db-4e85-840b-c8f817a7f0e8
keywords:
- 显示驱动程序 WDK Windows 2000 中，桌面管理
- 桌面管理 WDK Windows 2000 显示
- WDK Windows 2000 的切换桌面显示
- DrvAssertMode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c2135a1787f055ac9ddda708fd080544fffa153
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562287"
---
# <a name="switching-desktops-responding-to-drvassertmode"></a>切换桌面：响应 DrvAssertMode


## <span id="ddk_switching_desktops_responding_to_drvassertmode_gg"></span><span id="DDK_SWITCHING_DESKTOPS_RESPONDING_TO_DRVASSERTMODE_GG"></span>


在显示器上的桌面之间切换时，窗口管理器可确保桌面正确重绘并且鼠标指针为启用，显示在正确位置。 显示驱动程序接收到调用[ **DrvAssertMode** ](https://msdn.microsoft.com/library/windows/hardware/ff556178)只有在没有桌面开关时。

当调用此函数时，该驱动程序可确保所指示*PDEV*创建 PDEV 时, 指定的模式中或在文本模式下。 然后，窗口管理器选择正确的指针形状，并将其移动到当前的位置。 GDI，不是驱动程序，负责维护鼠标指针状态。

GDI 调用*DrvAssertMode*将指定的硬件设备模式设置。 此函数可选择创建显示驱动程序定义 PDEV 结构时指定的模式或硬件的默认模式。 该驱动程序应记录 PDEV 的当前模式。

此外调用 GDI [ **DrvAssertMode**](https://msdn.microsoft.com/library/windows/hardware/ff556178)，并启用参数设置为**FALSE**，当用户切换窗口的应用程序中，对中的全屏应用程序*x*86 应用程序，或当用户切换台式计算机 （在所有平台）。 显示驱动程序必须通过发送到默认模式下还原视频硬件[ **IOCTL\_视频\_重置\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff567834)中[ **EngDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff564838)调用到微型端口驱动程序。

 

 





