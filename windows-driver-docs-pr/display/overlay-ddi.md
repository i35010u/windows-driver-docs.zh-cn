---
title: 覆盖 DDI
description: 覆盖 DDI
keywords:
- 覆盖 DDI WDK Windows 7 显示
- 覆盖 DDI WDK Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61fdaa7ef675e99b4de895aa44a18e23d34ae87b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802605"
---
# <a name="overlay-ddi"></a>覆盖 DDI


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

覆盖 DDI 是 [Direct3D 版本 9 DDI](/windows-hardware/drivers/ddi/d3dumddi/index) 的扩展，用于验证覆盖支持。 覆盖 DDI 包含以下入口点：

-   \_Direct3D 运行时使用 [**D3DDDICAPS \_ 类型**](/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type)枚举中的 D3DDDICAPS CHECKOVERLAYSUPPORT 值来验证显示设备是否支持特定覆盖。 运行时在 \_ [**D3DDDIARG \_ GETCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的 **Type** 成员中设置 D3DDDICAPS CHECKOVERLAYSUPPORT，在运行时调用 **pData** 时，驱动程序的 [**GETCAPS**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数 *的 GETCAPS* 参数指向此结构。 运行时还将 D3DDDIARG GETCAPS 的 **pInfo** 成员设置 \_ 为指向描述覆盖的 [**DDICHECKOVERLAYSUPPORTINPUT**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_ddicheckoverlaysupportinput) 结构的指针。 如果驱动程序支持覆盖，则驱动程序将设置 D3DOVERLAYCAPS 结构的成员，并在 **D3DDDIARG \_ GETCAPS** 的 **pData** 成员中返回指向此结构的指针。 否则，如果驱动程序不支持覆盖，驱动程序将无法通过 D3DDDIERR UNSUPPORTEDOVERLAYFORMAT 或 D3DDDIERR UNSUPPORTEDOVERLAY 调用其 **GetCaps** 函数， \_ \_ 具体取决于是否缺少支持是基于覆盖格式。 DirectX SDK 文档中介绍了 D3DOVERLAYCAPS。

    该驱动程序将 D3DOVERLAYCAPS 的 **MaxOverlayDisplayWidth** 和 **MaxOverlayDisplayHeight** 成员设置为指示驱动程序和硬件可能具有的任何限制，这涉及到) 拉伸覆盖数据后 (的最终覆盖大小。

    驱动程序将 D3DOVERLAYCAPS \_ STRETCHX (0x00000040) 和 D3DOVERLAYCAPS \_ 伸缩 (0x00000080) 功能位设置为 D3DOVERLAYCAPS 的 **cap** 成员，以指示重叠硬件能够任意拉伸和收缩覆盖数据。 驱动程序不应尝试通过 GPU 模拟覆盖拉伸，只应在重叠硬件支持拉伸时设置这些上限。 通常，应用程序需要较少的开销，才能将 GPU 拉伸作为视频处理和组合阶段的一部分执行，而不是让驱动程序在最一端执行单独的传递来模拟覆盖拉伸。

-   驱动程序应处理 [**D3DDDI \_ OVERLAYINFOFLAGS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfoflags) 结构中的以下新的位域标志。 D3DDDI \_ OVERLAYINFOFLAGS 结构用于标识要执行的覆盖操作的类型。 \_在对驱动程序的 [**CreateOverlay**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createoverlay)或 [**UpdateOverlay**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updateoverlay)函数的调用中，在 [**D3DDDI \_ OVERLAYINFO**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfo)结构的 **Flags** 成员中指定 D3DDDI OVERLAYINFOFLAGS 结构。

    <span id="LimitedRGB"></span><span id="limitedrgb"></span><span id="LIMITEDRGB"></span>**LimitedRGB**  
    覆盖范围 RGB 有限，而不是全范围 RGB。 在 RGB 有限范围内，RGB 范围已压缩，因此16:16:16 为黑色，235:235:235 为白色。

    <span id="YCbCrBT709"></span><span id="ycbcrbt709"></span><span id="YCBCRBT709"></span>**YCbCrBT709**  
    覆盖为为709，表示高清晰电视 (HDTV) ，而不是 BT. 601。

    <span id="YCbCrxvYCC"></span><span id="ycbcrxvycc"></span><span id="YCBCRXVYCC"></span>**YCbCrxvYCC**  
    覆盖是扩展的 YCbCr (xvYCC) 而不是传统的 YCbCr。

-   如果显示格式为64位而不是32位 (例如，当桌面 Windows Manager (DWM) \_ 将 D3DFMT A16B16G16R16F 用于显示模式) 时，运行时将覆盖 colorkey 的32位置于 [**D3DDDI \_ OVERLAYINFO**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfo)结构的 **DstColorKeyLow** 成员32和 DstColorKeyHigh D3DDDI 的 **OVERLAYINFO** 成员中 \_ 。

 

