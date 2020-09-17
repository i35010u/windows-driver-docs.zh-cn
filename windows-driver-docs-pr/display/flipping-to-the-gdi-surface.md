---
title: 交替到 GDI 图面
description: 交替到 GDI 图面
ms.assetid: e74e108d-f88c-4e42-9136-ef087378807a
keywords:
- 绘图页反向 WDK DirectDraw，GDI surface
- DirectDraw 翻转 WDK Windows 2000 显示，GDI 图面
- 页面翻转 WDK DirectDraw，GDI surface
- 翻转 WDK DirectDraw，GDI surface
- GDI 图面翻转 WDK DirectDraw
- surface DirectDraw，翻转
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7aa860b3883fdb193822c63bc13c0a3b4f5d79ab
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716036"
---
# <a name="flipping-to-the-gdi-surface"></a>交替到 GDI 图面


## <span id="ddk_flipping_to_the_gdi_surface_gg"></span><span id="DDK_FLIPPING_TO_THE_GDI_SURFACE_GG"></span>


应该实现显示驱动程序，使 GDI (桌面) 图面成为主要表面。 这样做可以让应用程序显示 GDI 呈现的内容，如对话框。 驱动程序可以使用以下方法之一，使 GDI 图面成为主要表面：

-   驱动程序可以将 GDI 图面包含为驱动程序的翻转链中的一个缓冲区。 建议将此方法用于使应用程序切换到 GDI 图面。 默认情况下，当应用程序发出翻转请求时，DirectDraw 会对驱动程序的 [*DdFlip*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_flip) 函数进行调用，以便按照它们附加到链中彼此的顺序循环遍历缓冲区。 应用程序可以通过确定 GDI 图面的位置，然后通过发出适当的翻转请求数来翻转到 GDI 面。

-   该驱动程序可以实现 [*DdFlipToGDISurface*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_fliptogdisurface) 函数，以在 DirectDraw 翻转到或从 GDI 图面翻转时接收通知。 如果驱动程序可以访问 GDI 图面，驱动程序可以在收到此通知后翻转到 GDI 图面。 使用此方法时，无需将 GDI 表面作为驱动程序的翻转链的一部分。

 

