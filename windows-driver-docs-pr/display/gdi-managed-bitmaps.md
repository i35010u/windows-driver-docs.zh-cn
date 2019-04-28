---
title: GDI 管理的位图
description: GDI 管理的位图
ms.assetid: 4b575574-7090-4010-962b-80cac059bfa5
keywords:
- GDI WDK Windows 2000 显示，呈现引擎
- 图形驱动程序 WDK Windows 2000 显示，呈现引擎
- 绘制 WDK GDI，呈现引擎
- 呈现引擎 WDK GDI
- GDI WDK Windows 2000 显示位图
- 图形驱动程序 WDK Windows 2000 显示位图
- 绘制 WDK GDI，位图
- WDK GDI 位图
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce336f19ea9ecf5376ee974ede0b2963b149cff4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347591"
---
# <a name="gdi-managed-bitmaps"></a>GDI 管理的位图


## <span id="ddk_gdi_managed_bitmaps_gg"></span><span id="DDK_GDI_MANAGED_BITMAPS_GG"></span>


GDI 管理在所有位图*DIB*包括 1、 4、 8、 16、 24 和 32 位每像素的格式。 GDI 可以执行所有的行绘制填充，文本输出和位块传输 (bitblt) 操作这些位图上。 这使驱动程序具有执行所有图形呈现 GDI，或以实现其硬件为其提供特殊支持的函数。

如果该设备已*帧缓冲区*DIB 格式，GDI 可以执行任何或所有图形输出直接与帧缓冲区中，从而减少驱动程序的大小。 如果设备使用了非标准格式帧缓冲区中，则该驱动程序必须实现所需的所有[的绘图功能](optional-display-driver-functions.md)。 尽管产生性能开销，GDI 仍然可以模拟大多数绘图函数： 之前可以在运营的 GDI，然后复制回原格式绘制完成后，必须将像素复制到位图标准格式。

 

 





