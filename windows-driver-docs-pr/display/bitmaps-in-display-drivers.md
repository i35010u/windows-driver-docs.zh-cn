---
title: 显示驱动程序中的位图
description: 显示驱动程序中的位图
keywords:
- 显示驱动程序 WDK Windows 2000，位图
- 位图 WDK Windows 2000 显示
- 位块传输 WDK Windows 2000 显示器
- 离屏内存 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 445b273e049d2917d26fc6f4deda7f474d59420a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810451"
---
# <a name="bitmaps-in-display-drivers"></a>显示驱动程序中的位图


## <span id="ddk_bitmaps_in_display_drivers_gg"></span><span id="DDK_BITMAPS_IN_DISPLAY_DRIVERS_GG"></span>


某些设备（例如16色 VGA 显示器）可以更快地从非标准位图执行位块传输。 为支持此功能，驱动程序可以挂钩 [**DrvCreateDeviceBitmap**](/windows/win32/api/winddi/nf-winddi-drvcreatedevicebitmap) ，这允许驱动程序创建驱动程序完全管理的位图。 当驱动程序创建这样的位图时，驱动程序可以将其存储为任何格式。 驱动程序将检查传递的参数，并为所请求的每像素位数提供至少位数。 创建后，位图的内容是不确定的。 如果应用程序请求设备托管的位图，则在 **DrvCreateDeviceBitmap** 返回 control 后，GDI 将调用用于 [绘制函数](optional-display-driver-functions.md)的驱动程序。 如果驱动程序返回 **FALSE**，则不会创建驱动程序托管的位图，因此 GDI 可以处理 *引擎管理的图面* 上的绘图操作。

[**DrvSaveScreenBits**](/windows/win32/api/winddi/nf-winddi-drvsavescreenbits)函数还与显示驱动程序中的位块传输相关。 某些显示驱动程序可以将数据移入或移出屏幕外的设备内存，而不是可以从 *DIB* 重绘或复制区域。 这些驱动程序可以挂钩 **DrvSaveScreenBits**，这使得驱动程序可以在菜单或对话框出现时，调用该驱动程序，以便更快地保存或还原所显示图像的指定矩形。

**注意**   对于位块传输调用，GDI (不是驱动程序) 处理 *指针排除* 和 *剪辑区域锁定*。

 


在 [*屏幕内存*](video-present-network-terminology.md#off_screen_memory) 中实现设备位图的驱动程序可显著提高系统性能。 屏幕外设备位图通过以下方式提高系统性能：

-   使用加速器硬件替代要绘制的 GDI。

-   提高位图到屏幕位块传输的速度。

-   降低 (在屏幕内存中存储的位图对主内存的需求不会占用主内存) 中的空间。

-   利用硬件执行支持 OpenGL 的操作，例如掩码位块传输和双缓冲。


驱动程序应通过 [**DrvCreateDeviceBitmap**](/windows/win32/api/winddi/nf-winddi-drvcreatedevicebitmap)在屏幕内存中实现设备位图。

