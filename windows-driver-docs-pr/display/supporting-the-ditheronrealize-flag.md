---
title: 支持 DitherOnRealize 标志
description: 支持 DitherOnRealize 标志
keywords:
- 显示驱动程序 WDK Windows 2000，抖动
- DrvDitherColor
- 抖动 WDK Windows 2000 显示
- 颜色抖动 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 122b40aa38c7755f784431b644c2a833465e03f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838975"
---
# <a name="supporting-the-ditheronrealize-flag"></a>支持 DitherOnRealize 标志

在较早版本的 GDI 和图形 DDI 中，需要通过 GDI 执行两次调用以使指定颜色抖动，然后为该颜色实现画笔。 例如，当应用程序请求使用抖动颜色填充矩形时，GDI 通常会调用 [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt)，同时传递矩形的范围以及要使用的 brush 对象。 然后，显示驱动程序会检查画笔，发现尚未实现该画笔，并通过 [**BRUSHOBJ_pvGetRbrush**](/windows/win32/api/winddi/nf-winddi-brushobj_pvgetrbrush) 调用 gdi 来实现该画笔的 gdi。 由于显示驱动程序（而不是 GDI）执行画笔的抖动，GDI 会将最初提供的应用程序的 RGB 传递到显示驱动程序的 [**DrvDitherColor**](/windows/win32/api/winddi/nf-winddi-drvdithercolor) 回调中的抖动。

*DrvDitherColor* 返回一个指针，该指针指向一个颜色索引数组，用于描述提供的颜色的抖动信息返回到 GDI。 GDI 会立即将此仿色信息传递回 [**DrvRealizeBrush**](/windows/win32/api/winddi/nf-winddi-drvrealizebrush)的调用中的显示驱动程序。 实现 [**BRUSHOBJ**](/windows/win32/api/winddi/ns-winddi-brushobj) 后，控件会返回到 GDI，并随后返回到原始的 *DrvBitBlt* 函数。

若要使用上述方法完成仿色，GDI 必须先调用 *DrvDitherColor*，然后调用 *DrvRealizeBrush* ，这两个单独的函数调用。 在 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo) 结构中设置 GCAPS_DITHERONREALIZE 标志并将 *DrvRealizeBrush* 修改为有效组合这两个函数无需单独调用 *DrvDitherColor* ，还会保存一些内存分配。 在此方案中，如果显示驱动程序集 GCAPS_DITHERONREALIZE，则 GDI 将与 RGB 进行 *DrvRealizeBrush* ，并在 *iHatch* 中设置 RB_DITHERCOLOR 标志。 RB_DITHERCOLOR 标志设置为 *iHatch* 的高字节，而要抖动的 RGB 颜色包含在三个低序位字节中。 在这种情况下，需要调用 *DrvDitherColor* ，因为这两个调用的功能都放入其中。

有关代码示例，请参阅 *Permedia* 示例显示驱动程序。

> [!NOTE]
> Microsoft Windows 驱动程序工具包 (WDK) 不包含 3Dlabs Permedia2 (*3dlabs.htm*) 和 3Dlabs *Permedia3 (Perm3.htm) 示例* 显示驱动程序。 你可以从 Windows Server 2003 SP1 驱动程序开发工具包中获取这些示例驱动程序 (DDK) ，你可以从 WDHC 网站的 "Windows 驱动程序开发工具包" 页下载。
