---
title: 显示驱动程序中的位图
description: 显示驱动程序中的位图
ms.assetid: 3f0ed208-1cfb-4583-beaf-894cd210b459
keywords:
- 显示驱动程序 WDK Windows 2000 中，位图
- 显示位图 WDK Windows 2000
- 位块传输 WDK Windows 2000 显示
- 屏幕外内存 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96308f6cc29df62fbbdc013f815d70385d5e81c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384622"
---
# <a name="bitmaps-in-display-drivers"></a>显示驱动程序中的位图


## <span id="ddk_bitmaps_in_display_drivers_gg"></span><span id="DDK_BITMAPS_IN_DISPLAY_DRIVERS_GG"></span>


某些设备，如 16 色 VGA 显示，更快地可以从使用了非标准位图执行位块传输。 若要支持此功能，驱动程序可挂接**DrvCreateDeviceBitmap**。

**DrvSaveScreenBits**。 这些驱动程序可挂接**DrvSaveScreenBits**，它可让驱动程序调用保存或还原指定的矩形的多个快速时菜单显示的图像或对话框随即出现。

**请注意**  位块传输调用 GDI （而不是驱动程序） 处理*指针排除*并*剪辑区域锁定*。

 


实现设备位图中的驱动程序[*屏幕外内存*](video-present-network-terminology.md#off_screen_memory)可以显著提高系统性能。 设备屏幕外位图提高系统性能的方式是：

-   使用 accelerator 硬件来代替 GDI 绘制。

-   提高位图屏幕位块传输的速度。

-   减少了对主内存的要求 （在屏幕外内存中存储的位图不占用主内存中的空间）。

-   利用硬件执行支持 OpenGL，如掩码位块传输和双缓冲的操作。


驱动程序应通过屏幕外内存中实现设备位图[ **DrvCreateDeviceBitmap**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap)。

 

 





