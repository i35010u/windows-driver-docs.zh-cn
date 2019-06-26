---
title: 在标准与非标准模式之间切换
description: 在标准与非标准模式之间切换
ms.assetid: 15939910-b325-47ff-b4ed-bbaeec4149bd
keywords:
- 使用了非标准的显示模式 WDK DirectX 9.0，标准和非标准模式之间切换
- 标准和非标准模式 WDK DirectX 9.0 之间切换
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e67f4986a584530d1e6eb7176e0cf69b6824d910
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361192"
---
# <a name="switching-between-standard-and-nonstandard-modes"></a>在标准与非标准模式之间切换


## <span id="ddk_switching_between_standard_and_nonstandard_modes_gg"></span><span id="DDK_SWITCHING_BETWEEN_STANDARD_AND_NONSTANDARD_MODES_GG"></span>


DirectX 9.0 驱动程序创建为标准显示模式的标准主面和用于使用了非标准模式下的虚拟主面，以便在运行时可以在必要时的模式之间切换。 这两个图面表示相同的视频内存，除非在中显示不同的格式。 标准和非标准模式时翻页之间的驱动程序开关被请求的顺序如下所示：

1.  应用程序请求模式切换。

    应用程序调用**ChangeDisplaySettings**视频模式更改为匹配的位深度的函数。 对于 10:10:10:2 模式中，位深度为每像素 32 位。 有关详细信息**ChangeDisplaySettings**，请参阅 Microsoft Windows SDK 文档。

2.  驱动程序创建标准主图面。

    运行时调用的驱动程序[ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))函数来请求主表面的创建。 此主面使用标准的显示格式 (例如，D3DFMT\_A8B8G8R8) 和有无后的缓冲区。

3.  该驱动程序创建虚拟主图面上链。

    运行时调用的驱动程序*DdCreateSurface*函数来请求虚拟主表面的创建。 在运行时指定 DDSCAPS2\_EXTENDEDFORMATPRIMARY (0x40000000) 功能位**dwCaps2**的成员[ **DDSCAPS2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))结构此图面，以指示在图面，使用非标准的显示模式 (例如，D3DFMT\_A2R10G10B10)。 在运行时还指定 DDSCAPS\_OFFSCREENPLAIN 功能位**dwCaps** DDSCAPS2 以指示面具有显式的像素格式的成员。

    因为此图面用于现有的主面的只是另一个名称，该驱动程序不应分配更多视频内存到图面。

    对于此面上，运行时也指定 DDSCAPS\_FLIP 和 DDSCAPS\_复杂功能中的位**dwCaps**和一组附加的运行时设置了标准主数据库的方式类似于后台缓冲区翻转链图面。 驱动程序应分配视频内存，因为这些后台缓冲区的驱动程序的任何进一步调用*DdCreateSurface*函数对这些后缓冲; 也就是说，则运行时会创建多个仅对的图面上对象标准主要区域。

4.  驱动程序才切换到使用了非标准格式图面。

    显示设备输出的标准格式，而该应用程序组合在一个这些后台缓冲区的非标准映像。 此图像显示为准备就绪后，运行时指定的一种使用了非标准的图面作为驱动程序的调用中的目标[ *DdFlip* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)函数。 该驱动程序然后 reprograms 输出使用了非标准格式的显示设备。

5.  在应用程序运行。

    应用程序生成的驱动程序的进一步调用*DdFlip*函数之间使用了非标准的缓冲区和驱动程序将继续显示使用了非标准格式。 应用程序还可以生成对驱动程序的调用[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数使用 D3DDP2OP\_BLT 操作代码，以将后台缓冲区复制到前台缓冲区，但这些调用始终是两个非标准的图面上对象之间。 驱动程序支持在窗口模式下使用了非标准格式，除非该驱动程序不会处理非标准和标准的图面上格式之间 blts。 有关窗口模式用例的详细信息，请参阅[支持 Two-Dimensional 操作](supporting-two-dimensional-operations.md)。

6.  该驱动程序翻转图面上的后为标准格式。

    运行时时关闭或最小化应用程序，作为对驱动程序的调用中的目标指定的标准格式主要面*DdFlip*函数。 该驱动程序然后 reprograms 显示设备输出的标准格式。

7.  该驱动程序销毁虚拟图面。

    当驱动程序破坏虚拟图面时，应确保标准格式重新编程后显示设备中。

 

 





