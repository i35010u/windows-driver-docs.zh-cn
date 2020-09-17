---
title: 显示驱动程序中的透明度
description: 显示驱动程序中的透明度
ms.assetid: 566706fb-66bd-44f5-b98c-23ed60e27970
keywords:
- 显示驱动程序 WDK Windows 2000，透明度
- 透明 WDK Windows 2000 显示器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcdc513d3d8ddd8015c58558240e33cfdb7fd0a9
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717586"
---
# <a name="transparency-in-display-drivers"></a>显示驱动程序中的透明度


## <span id="ddk_transparency_in_display_drivers_gg"></span><span id="DDK_TRANSPARENCY_IN_DISPLAY_DRIVERS_GG"></span>


如果显示硬件支持透明度，则显示驱动程序应实现 [**DrvTransparentBlt**](/windows/win32/api/winddi/nf-winddi-drvtransparentblt)。

为了降低从视频内存进行读取的成本，当源和目标面都在视频内存中时，驱动程序应该实现此功能。 驱动程序应该允许 GDI 处理透明位块从系统内存传输到视频内存，并允许 GDI 处理扩展的位块传输。

 

