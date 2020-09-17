---
title: 支持拉伸位图传送操作
description: 支持拉伸位图传送操作
ms.assetid: 1d279e56-41fd-4189-84d2-858e51db281d
keywords:
- array.blit stretch 操作 WDK DirectX 9。0
- stretch array.blit 操作 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e353058c69a6560a7f600979a12b8c055ee1f782
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714968"
---
# <a name="supporting-stretch-blit-operations"></a>支持拉伸位图传送操作


## <span id="ddk_supporting_stretch_blit_operations_gg"></span><span id="DDK_SUPPORTING_STRETCH_BLIT_OPERATIONS_GG"></span>


驱动程序如何执行 stretch array.blit 取决于运行该驱动程序的平台。 对于 Windows 98/Me 平台，当驱动程序的[*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)函数收到 array.blit 请求时，驱动程序可以从[**DD \_ rOrigSrc**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_bltdata)结构的**rOrigDest**和**BLTDATA**成员的未剪辑矩形区计算 stretch 因数，并在执行 array.blit 操作时计算计算中的因素。

对于在基于 NT 的操作系统上使用的 DirectX 9.0 和更高版本，驱动程序可以在接收到 array.blit 请求时使用 DDBLT \_ 扩展 \_ 标志和 DDBLT \_ 扩展 \_ 表示法 \_ STRETCHFACTOR 标记（在 DD dwFlags 的 **BLTDATA** 成员中设置 \_ ）来计算和记录 stretch 因数。 该驱动程序将从 .Rsrc 和**bltFX**成员中的未剪辑源和目标矩形区，分别计算**rSrc**和成员的拉伸系数 \_ \_ \_ \_ 。 请注意，驱动程序必须从 **bltFX**中 DDBLTFX 结构的以下成员获取未剪辑目标矩形区，而不能使用 **rDest** 成员中的信息。

-   DDBLTFX 的 **ddckDestColorkey** 成员中 DDCOLORKEY 结构的以下成员的左坐标和上坐标：
    -   DDCOLORKEY 的 **dwColorSpaceLowValue** 成员的左坐标。
    -   DDCOLORKEY 的 **dwColorSpaceHighValue** 成员的顶层坐标。
-   在 DDBLTFX 的 **ddckSrcColorkey** 成员中，从 DDCOLORKEY 结构的以下成员开始向右和向下坐标：
    -   右坐标来自 DDCOLORKEY 的 **dwColorSpaceLowValue** 成员。
    -   从 DDCOLORKEY 的 **dwColorSpaceHighValue** 成员开始的下坐标。

请注意，驱动程序将这些坐标解释为有符号整数，而不是 Dword。 另请注意，驱动程序必须在计算延伸因子之前验证这些坐标窗体的矩形，并对图形设备中的 stretch 因数进行编程。 有关 DDBLTFX 和 DDCOLORKEY 的详细信息，请参阅最新的 DirectDraw SDK 文档。

当驱动程序接收到 DDBLT \_ 扩展 \_ 显示 STRETCHFACTOR 集的 array.blit 时 \_ ，驱动程序不得使用未剪辑矩形区来执行任何实际的 blitting。

当驱动程序随后接收到 DDBLT \_ 表示法和 DDBLT 的 \_ 最后一个 \_ 表示标志集的 array.blit 请求时，驱动程序可以将此记录的延伸系数考虑到 array.blit 操作中。 当驱动程序完成最后一个 array.blit 并设置了 DDBLT 的 \_ 最后一个 \_ 显示标志之后，驱动程序必须清除 stretch 因数记录，以防止与后续 blits 的干扰。 有关 DDBLT \_ 表示和 DDBLT \_ 最后一个演示标志的详细信息 \_ ，请参阅 [演示](presentation.md)。

由于 stretch 因数是浮点计算，因此并非所有图形设备都能支持它。 因此，此类设备的驱动程序不需要计算和使用延伸系数。 但是，即使不支持 stretch 因数计算，基于 NT 的操作系统上的 DirectX 9.0 和更高版本驱动程序仍必须确定 DDBLT \_ 扩展 \_ 呈现 STRETCHFACTOR 标志的状态， \_ 因为尝试执行实际 array.blit 操作时，DDBLT \_ 扩展 \_ 表示 \_ STRETCHFACTOR 标志设置为会导致呈现损坏。

有关扩展的 array.blit 标志的详细信息，请参阅 [扩展的 Blt 标志](extended-blt-flags.md)。

 

