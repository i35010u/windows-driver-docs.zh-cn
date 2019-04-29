---
title: 交替到 GDI 图面
description: 交替到 GDI 图面
ms.assetid: e74e108d-f88c-4e42-9136-ef087378807a
keywords:
- 翻转 WDK DirectDraw，GDI 面绘制页面
- DirectDraw 翻转 WDK Windows 2000 显示，GDI 图面
- 页翻转 WDK DirectDraw，GDI 图面
- 翻转 WDK DirectDraw，GDI 图面
- 翻转 WDK DirectDraw GDI 面
- 显示 WDK DirectDraw 翻转
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5287f565c499a1325bc7b7d049946bc57359f1d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359405"
---
# <a name="flipping-to-the-gdi-surface"></a>交替到 GDI 图面


## <span id="ddk_flipping_to_the_gdi_surface_gg"></span><span id="DDK_FLIPPING_TO_THE_GDI_SURFACE_GG"></span>


显示驱动程序应实现，以便在 GDI （桌面版） 面会变得主图面。 执行此操作允许显示 GDI 呈现的内容，例如，对话框的应用程序。 该驱动程序可以使用以下方法之一使主表面 GDI 图面：

-   该驱动程序可以包含 GDI 图面，因为一个驱动程序中的缓冲区的翻转链。 此方法是为了让应用程序到 GDI 面翻转的推荐的方式。 默认情况下，当应用程序进行翻转请求 DirectDraw 会调用驱动程序的[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)函数以在循环中的顺序与其所附加到中彼此的缓冲区链。 确定在链中的 GDI 面位置然后进行适当数量的翻转请求，应用程序可以切换到 GDI 图面。

-   该驱动程序可以实现[ *DdFlipToGDISurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549335)函数 DirectDraw 翻转到或从 GDI 图面时接收通知。 如果驱动程序可以访问的 GDI 图面，该驱动程序可以收到此通知后，切换到 GDI 图面。 使用此方法，GDI 面不是需要是驱动程序的翻转链的一部分。

 

 





