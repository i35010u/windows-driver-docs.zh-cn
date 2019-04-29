---
title: 覆盖 DDI
description: 覆盖 DDI
ms.assetid: c8f1cdd6-1beb-43bd-b96c-2eea3a51321e
keywords:
- 覆盖 DDI WDK Windows 7 显示
- 覆盖 DDI WDK Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ac22885f8e3375a72e7038eec2c6c37d96ca418
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352419"
---
# <a name="overlay-ddi"></a>覆盖 DDI


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

覆盖 DDI 是扩展[Direct3D 版本 9 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552927)验证覆盖的支持。 覆盖 DDI 包括以下入口点：

-   D3DDDICAPS\_CHECKOVERLAYSUPPORT 取值[ **D3DDDICAPS\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff544132)枚举由 Direct3D 运行时用来验证是否显示设备支持特定覆盖。 运行时设置 D3DDDICAPS\_中的 CHECKOVERLAYSUPPORT**类型**的成员[ **D3DDDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff543148)结构的*pData*驱动程序的参数[ **GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff566762)函数运行时调用的时点**GetCaps**。 运行时还会设置**pInfo** D3DDDIARG 成员\_GETCAPS 为指针[ **DDICHECKOVERLAYSUPPORTINPUT** ](https://msdn.microsoft.com/library/windows/hardware/ff549563)描述结构覆盖。 如果该驱动程序支持在覆盖区上，驱动程序设置 D3DOVERLAYCAPS 结构的成员，并返回指向此结构中的指针**pData**的成员**D3DDDIARG\_GETCAPS**。 否则，如果驱动程序不支持在覆盖区上，该驱动程序将失败调用其**GetCaps**函数与任一 D3DDDIERR\_UNSUPPORTEDOVERLAYFORMAT 或 D3DDDIERR\_UNSUPPORTEDOVERLAY 具体于上是否不支持基于覆盖格式。 D3DOVERLAYCAPS 是 DirectX SDK 文档中所述。

    驱动程序集**MaxOverlayDisplayWidth**并**MaxOverlayDisplayHeight** D3DOVERLAYCAPS 以指示驱动程序和硬件可能有，这涉及最终任何限制的成员覆盖 （后拉伸覆盖数据） 的大小。

    驱动程序设置 D3DOVERLAYCAPS\_STRETCHX (0x00000040) 和 D3DOVERLAYCAPS\_STRETCHY (0x00000080) 功能中的位**Caps** D3DOVERLAYCAPS 以指示是覆盖硬件的成员能够随意拉伸和收缩的覆盖数据。 驱动程序不应尝试模拟覆盖通过 GPU 拉伸和应仅设置这些上限，如果覆盖硬件支持拉伸。 更少的开销是通常所必需的应用程序执行 GPU 的视频处理一部分拉伸和组合阶段不是为要执行一个单独的驱动程序在最后，若要模拟传递覆盖拉伸。

-   该驱动程序应处理从以下新的位域标志[ **D3DDDI\_OVERLAYINFOFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff544626)结构。 D3DDDI\_OVERLAYINFOFLAGS 结构标识覆盖要执行的操作类型。 D3DDDI\_中指定 OVERLAYINFOFLAGS 结构**标志**的成员[ **D3DDDI\_OVERLAYINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff544621)对的调用中的结构驱动程序[ **CreateOverlay** ](https://msdn.microsoft.com/library/windows/hardware/ff540662)或[ **UpdateOverlay** ](https://msdn.microsoft.com/library/windows/hardware/ff570107)函数。

    <span id="LimitedRGB"></span><span id="limitedrgb"></span><span id="LIMITEDRGB"></span>**LimitedRGB**  
    在覆盖区上是有限的范围 RGB 而不是完整范围 RGB。 在有限范围内 RGB，RGB 范围进行压缩 16:16:16 为黑色并 235:235:235 为白色。

    <span id="YCbCrBT709"></span><span id="ycbcrbt709"></span><span id="YCBCRBT709"></span>**YCbCrBT709**  
    在覆盖区上是 BT.709，指示高清晰电视 (HDTV)，而不是 BT.601。

    <span id="YCbCrxvYCC"></span><span id="ycbcrxvycc"></span><span id="YCBCRXVYCC"></span>**YCbCrxvYCC**  
    在覆盖区上而不是传统 YCbCr 扩展 YCbCr (xvYCC)。

-   64 位而不是 32 位的显示格式时 (例如，当桌面 Windows 管理器 (DWM) 使用 D3DFMT\_A16B16G16R16F 的显示模式)，运行时将放置在覆盖 colorkey 低 32 位**DstColorKeyLow**的成员[ **D3DDDI\_OVERLAYINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff544621)结构和在高 32 位**DstColorKeyHigh**的成员D3DDDI\_OVERLAYINFO。

 

 





