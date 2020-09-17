---
title: 在标准与非标准模式之间切换
description: 在标准与非标准模式之间切换
ms.assetid: 15939910-b325-47ff-b4ed-bbaeec4149bd
keywords:
- 非标准显示模式 WDK DirectX 9.0，在标准和非标准模式之间切换
- 切换标准和非标准模式 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d31d3d8f04fda7caa519722266b806dafbb3fa5c
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717450"
---
# <a name="switching-between-standard-and-nonstandard-modes"></a>在标准与非标准模式之间切换


## <span id="ddk_switching_between_standard_and_nonstandard_modes_gg"></span><span id="DDK_SWITCHING_BETWEEN_STANDARD_AND_NONSTANDARD_MODES_GG"></span>


DirectX 9.0 驱动程序为标准模式创建标准主表面，为非标准模式创建虚拟主图面，以便运行时可以在需要时在模式间切换。 这两个图面表示相同的视频内存，但以不同的格式显示。 请求页面翻转时，驱动程序在标准和非标准模式之间切换，如以下顺序所示：

1.  应用程序请求模式开关。

    应用程序调用 **ChangeDisplaySettings** 函数将视频模式更改为匹配的位深度。 对于10:10:10:2 模式，位深度为每像素32位。 有关 **ChangeDisplaySettings**的详细信息，请参阅 Microsoft Windows SDK 的文档。

2.  驱动程序创建标准主表面。

    运行时调用驱动程序的 [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)) 函数来请求创建主图面。 此主要表面使用标准显示格式 (例如，D3DFMT \_ A8B8G8R8) 并且没有后台缓冲区。

3.  驱动程序创建虚拟主表面链。

    运行时调用驱动程序的 *DdCreateSurface* 函数，请求创建虚拟主图面。 运行时在 \_ 此图面的[**DDSCAPS2**](/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))结构的**DWCAPS2**成员中指定 DDSCAPS2 EXTENDEDFORMATPRIMARY (0x40000000) 功能位，以指示该图面使用非标准显示模式 (例如，D3DFMT \_ A2R10G10B10) 。 运行时还 \_ 在 DDSCAPS2 的 **dwCaps** 成员中指定 DDSCAPS OFFSCREENPLAIN 功能位，以指示该图面具有显式像素格式。

    由于此表面仅适用于现有主表面的另一个名称，因此驱动程序不应将更多的视频内存分配给表面。

    对于此图面，运行时还指定了 \_ dwCaps 中的 DDSCAPS FLIP 和 DDSCAPS \_ 复杂功能位，并与运行时设置标准主表面翻转链的方式类似。 **dwCaps** 驱动程序应为这些后台缓冲区分配视频内存，因为对这些后台缓冲区不会进一步调用驱动程序的 *DdCreateSurface* 函数;也就是说，运行时仅为标准主副本创建一个多个 surface 对象。

4.  驱动程序将曲面翻转为非标准格式。

    显示设备输出标准格式时，应用程序会在其中一个后台缓冲区中撰写非标准图像。 此映像准备好可供显示后，运行时在调用驱动程序的 [*DdFlip*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_flip) 函数时指定了一个非标准曲面作为目标。 然后，该驱动程序将 reprograms 显示设备输出非标准格式。

5.  将运行应用程序。

    应用程序在非标准缓冲区之间生成对驱动程序的 *DdFlip* 函数的进一步调用，驱动程序将继续显示非标准格式。 应用程序还可以使用 D3DDP2OP BLT 操作代码生成对驱动程序的 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 函数的调用 \_ ，以将后台缓冲区复制到前台缓冲区，但这些调用始终在两个非标准 surface 对象之间进行。 除非驱动程序在窗口模式下支持非标准格式，否则驱动程序不会在非标准和标准表面格式之间处理 blts。 有关窗口模式情况的详细信息，请参阅 [支持二维操作](supporting-two-dimensional-operations.md)。

6.  驱动程序将表面反转为标准格式。

    关闭或最小化应用程序时，运行时将标准格式的主表面指定为对驱动程序的 *DdFlip* 函数的调用中的目标。 然后，该驱动程序将 reprograms 显示设备输出标准格式。

7.  驱动程序销毁了虚拟图面。

    当驱动程序损坏虚拟图面时，它应确保在显示设备中 reprogrammed 标准格式。

 

