---
title: 创建设备相关的位图
description: 创建设备相关的位图
ms.assetid: da53a8bf-5991-4abb-81f1-2d3a7cb0ff90
keywords:
- GDI WDK Windows 2000 显示，位图
- 图形驱动程序 WDK Windows 2000 显示，位图
- 绘制 WDK GDI，位图
- 位图 WDK GDI
- 特定于设备的位图 WDK GDI
- DDB WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7204e710372ac1411a955a512c4038c66e50015
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715348"
---
# <a name="creating-device-dependent-bitmaps"></a>创建设备相关的位图


## <span id="ddk_creating_device_dependent_bitmaps_gg"></span><span id="DDK_CREATING_DEVICE_DEPENDENT_BITMAPS_GG"></span>

当应用程序请求创建位图时，驱动程序可以通过支持[**DrvCreateDeviceBitmap**](/windows/win32/api/winddi/nf-winddi-drvcreatedevicebitmap)函数来创建和管理[*DDB*](/windows/desktop/gdi/device-dependent-bitmaps) 。 此类驱动程序创建位图后，可以将位图存储为任何格式。 驱动程序将检查传递的参数，并为所请求的每像素位数提供至少位数。

> [!NOTE]
> 图形驱动程序可以通过在 [*屏幕内存*](video-present-network-terminology.md#off_screen_memory) 中支持位图并使用硬件绘制位图来提高性能。 有关此示例的示例，请参阅 **Permedia** 显示驱动程序示例。


> [!NOTE]
> Microsoft Windows 驱动程序工具包 (WDK) 不包含 3Dlabs Permedia2 (*3dlabs.htm*) 和 3Dlabs * Permedia3 (Perm3.htm) 示例 * 显示驱动程序。 你可以从 Windows Server 2003 SP1 驱动程序开发工具包中获取这些示例驱动程序 (DDK) ，你可以从 WDHC 网站的 "Windows 驱动程序开发工具包" 页下载。

在 **DrvCreateDeviceBitmap**中，驱动程序调用 Gdi 服务 [**ENGCREATEDEVICEBITMAP**](/windows/win32/api/winddi/nf-winddi-engcreatedevicebitmap) ，使 gdi 为设备位图创建句柄。

如果驱动程序支持 **DrvCreateDeviceBitmap**，它将创建一个 DDB，定义其格式，并向其返回一个句柄。 驱动程序控制位图的存储位置和格式。 驱动程序应支持与设备表面最接近的颜色格式。

创建后，位图的内容是不确定的。 如果驱动程序返回 **NULL**，则它不会创建并管理位图;GDI 将执行这些任务。

如果驱动程序创建位图，它还必须能够通过实现 [**DrvDeleteDeviceBitmap**](/windows/win32/api/winddi/nf-winddi-drvdeletedevicebitmap) 函数来删除它们。

 

