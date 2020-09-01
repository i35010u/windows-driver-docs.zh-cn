---
title: 显示驱动程序中的位图
description: 显示驱动程序中的位图
ms.assetid: 3f0ed208-1cfb-4583-beaf-894cd210b459
keywords:
- 显示驱动程序 WDK Windows 2000，位图
- 位图 WDK Windows 2000 显示
- 位块传输 WDK Windows 2000 显示器
- 离屏内存 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f294745e06f796a4ac50d19cc0a6c449700813b
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067476"
---
# <a name="bitmaps-in-display-drivers"></a>显示驱动程序中的位图


## <span id="ddk_bitmaps_in_display_drivers_gg"></span><span id="DDK_BITMAPS_IN_DISPLAY_DRIVERS_GG"></span>


某些设备（例如16色 VGA 显示器）可以更快地从非标准位图执行位块传输。 为了支持这一点，驱动程序可以挂钩 **DrvCreateDeviceBitmap**。

**DrvSaveScreenBits**。 这些驱动程序可以挂钩 **DrvSaveScreenBits**，这使得驱动程序可以在菜单或对话框出现时，调用该驱动程序，以便更快地保存或还原所显示图像的指定矩形。

**注意**   对于位块传输调用，GDI (不是驱动程序) 处理*指针排除*和*剪辑区域锁定*。

 


在 [*屏幕内存*](video-present-network-terminology.md#off_screen_memory) 中实现设备位图的驱动程序可显著提高系统性能。 屏幕外设备位图通过以下方式提高系统性能：

-   使用加速器硬件替代要绘制的 GDI。

-   提高位图到屏幕位块传输的速度。

-   降低 (在屏幕内存中存储的位图对主内存的需求不会占用主内存) 中的空间。

-   利用硬件执行支持 OpenGL 的操作，例如掩码位块传输和双缓冲。


驱动程序应通过 [**DrvCreateDeviceBitmap**](/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap)在屏幕内存中实现设备位图。

 

