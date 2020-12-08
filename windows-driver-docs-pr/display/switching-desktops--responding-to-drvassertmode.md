---
title: 切换桌面响应 DrvAssertMode
description: 切换桌面响应 DrvAssertMode
keywords:
- 显示驱动程序 WDK Windows 2000，桌面管理
- 桌面管理 WDK Windows 2000 显示器
- 切换桌面 WDK Windows 2000 显示器
- DrvAssertMode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de2aa173f04045418c639ed2b23d0ef1fde838ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838951"
---
# <a name="switching-desktops-responding-to-drvassertmode"></a>切换桌面：响应 DrvAssertMode


## <span id="ddk_switching_desktops_responding_to_drvassertmode_gg"></span><span id="DDK_SWITCHING_DESKTOPS_RESPONDING_TO_DRVASSERTMODE_GG"></span>


当在显示器上切换桌面时，窗口管理器将确保正确重绘桌面并在正确位置启用并显示鼠标指针。 仅当存在桌面开关时，显示驱动程序才会接收对 [**DrvAssertMode**](/windows/win32/api/winddi/nf-winddi-drvassertmode) 的调用。

调用此函数时，驱动程序将确保指示的 *PDEV* 是在创建 PDEV 时指定的模式下，还是在文本模式下。 然后，窗口管理器会选择正确的指针形状，并将其移动到当前位置。 GDI （而不是驱动程序）负责维护鼠标指针状态。

GDI 调用 *DrvAssertMode* 来设置指定硬件设备的模式。 此函数选择在创建显示驱动程序定义的 PDEV 结构或硬件的默认模式时指定的模式。 驱动程序应保留 PDEV 当前模式的记录。

GDI 还会调用 [**DrvAssertMode**](/windows/win32/api/winddi/nf-winddi-drvassertmode)，并将 enable 参数设置为 **FALSE**，当用户从有窗口的应用程序切换到 *x* 86 应用程序中的全屏应用程序时，或者当用户切换) 的所有平台上的桌面 (时。 显示驱动程序必须通过将 [**IOCTL \_ 视频 \_ 重置 \_ 设备**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_reset_device) 发送到视频微型端口驱动程序的 [**EngDeviceIoControl**](/windows/win32/api/winddi/nf-winddi-engdeviceiocontrol) 调用，将视频硬件还原到默认模式。

 

