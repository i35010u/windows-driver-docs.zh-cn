---
title: 支持 DitherOnRealize 标志
description: 支持 DitherOnRealize 标志
ms.assetid: 2a480045-ed2e-4650-80a4-a374f0388591
keywords:
- 显示驱动程序 WDK Windows 2000，抖色
- DrvDitherColor
- 抖动 WDK Windows 2000 显示
- 抖动 WDK Windows 2000 显示的颜色
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f58ecc950acff5fe717fc9f544d42ea91dd6641b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361227"
---
# <a name="supporting-the-ditheronrealize-flag"></a>支持 DitherOnRealize 标志


## <span id="ddk_supporting_the_ditheronrealize_flag_gg"></span><span id="DDK_SUPPORTING_THE_DITHERONREALIZE_FLAG_GG"></span>


在 GDI 和图形 DDI 的早期版本中，通过 GDI 的两个调用，以显示驱动程序功能需要抖动指定的颜色，然后发现该颜色的画笔。 例如，当应用程序请求时，使用抖色填充矩形，GDI 通常会调用[ **DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)，传递的矩形和要使用的画笔对象的扩展盘区。 显示器驱动程序，然后检查画笔，发现它未实现，并回拨到使用的 GDI [ **BRUSHOBJ\_pvGetRbrush** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_pvgetrbrush) GDI 的画笔地实现。 由于显示器驱动程序不 GDI，执行抖色的画笔，GDI 将应用程序最初为抵色处理中提供的 RGB [ **DrvDitherColor** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdithercolor)显示器驱动程序的回调。

*DrvDitherColor*返回指向描述的抖动信息返回到 GDI 提供颜色的颜色索引的数组的指针。 GDI 立即将此抖动信息传递回调用中的显示驱动程序[ **DrvRealizeBrush**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvrealizebrush)。 与[ **BRUSHOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_brushobj)意识到，控件将返回到 GDI，并随后返回到原始*DrvBitBlt*函数。

若要为抵色处理使用上面的技术，GDI 必须调用*DrvDitherColor*，然后通过调用立即*DrvRealizeBrush* -两个单独的函数调用。 设置 GCAPS\_DITHERONREALIZE 标志[ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)结构和修改*DrvRealizeBrush*有效地组合这两个函数不需要单独调用*DrvDitherColor*还会节省一些内存分配。 在此方案中，如果显示驱动程序设置 GCAPS\_DITHERONREALIZE、 GDI 调用*DrvRealizeBrush*若要进行抖色处理的 RGB 和 RB\_中设置 DITHERCOLOR 标志*iHatch*. RB\_DITHERCOLOR 标志设置中的高字节*iHatch*，而在三个低位字节中包含的 RGB 颜色抖色。 需要调用*DrvDitherColor*将消除这种情况下，因为这两个调用的功能将放入其中一个。

有关示例代码，请参阅*Permedia*示例显示器驱动程序。

**请注意**   Microsoft Windows Driver Kit (WDK) 不包含 3Dlabs Permedia2 (*3dlabs.htm*) 和 3Dlabs Permedia3 (*Perm3.htm*) 示例显示器驱动程序。 你可以获取这些示例驱动程序从 Windows Server 2003 SP1 驱动程序开发工具包 (DDK)，可以从 DDK-WDHC 网站的 Windows 驱动程序开发工具包页面下载。

 

 

 





