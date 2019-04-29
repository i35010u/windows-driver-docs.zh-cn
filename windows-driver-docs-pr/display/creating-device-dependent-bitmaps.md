---
title: 创建设备相关的位图
description: 创建设备相关的位图
ms.assetid: da53a8bf-5991-4abb-81f1-2d3a7cb0ff90
keywords:
- GDI WDK Windows 2000 显示位图
- 图形驱动程序 WDK Windows 2000 显示位图
- 绘制 WDK GDI，位图
- WDK GDI 位图
- 特定于设备的位图 WDK GDI
- DDB WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42e2f6dec985d51533ef7e0bfe37698bcb4de7a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387250"
---
# <a name="creating-device-dependent-bitmaps"></a>创建设备相关的位图


## <span id="ddk_creating_device_dependent_bitmaps_gg"></span><span id="DDK_CREATING_DEVICE_DEPENDENT_BITMAPS_GG"></span>

驱动程序时应用程序请求的位图的创建，可以创建和管理[ *DDB* ](https://docs.microsoft.com/windows/desktop/gdi/device-dependent-bitmaps)通过支持[ **DrvCreateDeviceBitmap** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap)函数。 当此类驱动程序创建位图时，它可以采用任何格式存储位图。 驱动程序会检查所传递的参数，并为位图提供至少多少位每像素的请求。

> [!NOTE]
> 图形驱动程序可以通过支持中的位图来提高性能[*屏幕外内存*](video-present-network-terminology.md#off_screen_memory)和通过绘制位图使用硬件。 此示例，请参阅**Permedia**显示驱动程序示例。


> [!NOTE]
> Microsoft Windows Driver Kit (WDK) 不包含 3Dlabs Permedia2 (*3dlabs.htm*) 和 3Dlabs Permedia3 (*Perm3.htm*) 示例显示器驱动程序。 你可以获取这些示例驱动程序从 Windows Server 2003 SP1 驱动程序开发工具包 (DDK)，可以从 DDK-WDHC 网站的 Windows 驱动程序开发工具包页面下载。

内**DrvCreateDeviceBitmap**，该驱动程序调用 GDI 服务[ **EngCreateDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff564204)要具有 GDI 创建设备位图的句柄。

如果该驱动程序支持**DrvCreateDeviceBitmap**，它创建 DDB、 定义其格式，并返回的句柄。 该驱动程序控制存储位图，然后在何种格式。 该驱动程序应支持其设备图面最匹配的颜色格式。

创建后将不确定位图的内容。 如果驱动程序将返回**NULL**，它不创建和管理位图; 相反，GDI 执行这些任务。

如果该驱动程序创建位图，它还必须能够通过实现将其删除[ **DrvDeleteDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff556187)函数。

 

 





