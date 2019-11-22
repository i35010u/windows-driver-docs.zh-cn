---
title: 覆盖 DDI
description: 覆盖 DDI
ms.assetid: c8f1cdd6-1beb-43bd-b96c-2eea3a51321e
keywords:
- 覆盖 DDI WDK Windows 7 显示
- 覆盖 DDI WDK Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7276ccced91896f2dc537ec616955f38b148e128
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826067"
---
# <a name="overlay-ddi"></a>覆盖 DDI


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

覆盖 DDI 是[Direct3D 版本 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/index)的扩展，用于验证覆盖支持。 覆盖 DDI 包含以下入口点：

-   Direct3D 运行时使用[**D3DDDICAPS\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type)枚举中的 D3DDDICAPS\_CHECKOVERLAYSUPPORT 值来验证显示设备是否支持特定覆盖。 运行时在[**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的**类型**成员中设置 D3DDDICAPS\_CHECKOVERLAYSUPPORT，在运行时调用**pData**时，驱动程序的[**GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps) *函数的 GETCAPS 参数指向*此结构。 运行时还会将 D3DDDIARG\_GETCAPS 的**pInfo**成员设置为指向描述覆盖的[**DDICHECKOVERLAYSUPPORTINPUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_ddicheckoverlaysupportinput)结构的指针。 如果驱动程序支持覆盖，则驱动程序将设置 D3DOVERLAYCAPS 结构的成员，并在**D3DDDIARG\_GETCAPS**的**pData**成员中返回指向此结构的指针。 否则，如果驱动程序不支持覆盖，驱动程序将无法通过 D3DDDIERR\_UNSUPPORTEDOVERLAYFORMAT 或 D3DDDIERR\_UNSUPPORTEDOVERLAY 调用其**GetCaps**函数，具体取决于是否缺少支持基于覆盖格式。 DirectX SDK 文档中介绍了 D3DOVERLAYCAPS。

    驱动程序将 D3DOVERLAYCAPS 的**MaxOverlayDisplayWidth**和**MaxOverlayDisplayHeight**成员设置为指示驱动程序和硬件可能具有的任何限制，这涉及最终覆盖大小（延伸覆盖数据后）).

    驱动程序在伸缩的**cap**成员中设置 D3DOVERLAYCAPS\_STRETCHX （0x00000040）和 D3DOVERLAYCAPS\_0x00000080 （D3DOVERLAYCAPS）功能位，以指示覆盖硬件能够任意拉伸收缩覆盖数据。 驱动程序不应尝试通过 GPU 模拟覆盖拉伸，只应在重叠硬件支持拉伸时设置这些上限。 通常，应用程序需要较少的开销，才能将 GPU 拉伸作为视频处理和组合阶段的一部分执行，而不是让驱动程序在最一端执行单独的传递来模拟覆盖拉伸。

-   驱动程序应处理来自[**D3DDDI\_OVERLAYINFOFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfoflags)结构的以下新的位域标志。 D3DDDI\_OVERLAYINFOFLAGS 结构标识要执行的覆盖操作的类型。 在调用驱动程序的[**CreateOverlay**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createoverlay)或[**UpdateOverlay**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updateoverlay)函数的[**D3DDDI\_OVERLAYINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfo)结构的**FLAGS**成员中指定了 D3DDDI\_OVERLAYINFOFLAGS 结构。

    <span id="LimitedRGB"></span><span id="limitedrgb"></span><span id="LIMITEDRGB"></span>**LimitedRGB**  
    覆盖范围 RGB 有限，而不是全范围 RGB。 在 RGB 有限范围内，RGB 范围已压缩，因此16:16:16 为黑色，235:235:235 为白色。

    <span id="YCbCrBT709"></span><span id="ycbcrbt709"></span><span id="YCBCRBT709"></span>**YCbCrBT709**  
    覆盖为为709，表示高清晰电视（HDTV），而不是 BT. 601。

    <span id="YCbCrxvYCC"></span><span id="ycbcrxvycc"></span><span id="YCBCRXVYCC"></span>**YCbCrxvYCC**  
    覆盖是扩展 YCbCr （xvYCC），而不是传统的 YCbCr。

-   当显示格式为64位而不是32位时（例如，当桌面窗口管理器（DWM）使用 D3DFMT\_A16B16G16R16F 作为显示模式）时，运行时将覆盖 colorkey 中的较低32位置于**DstColorKeyLow**成员在 D3DDDI\_OVERLAYINFO 的**DstColorKeyHigh**成员中， [**D3DDDI\_OVERLAYINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfo)结构和上限32位。

 

 





