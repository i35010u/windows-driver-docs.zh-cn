---
title: 报告使用图面格式执行 2D 操作的支持
description: 报告使用图面格式执行 2D 操作的支持
ms.assetid: c7737daf-3342-48dc-a365-f789b7203013
keywords:
- 二维操作 WDK DirectX 9.0，表面格式
- 2D 操作 WDK DirectX 9.0，表面格式
- 表面格式 WDK DirectX 9。0
- surface 格式化 WDK DirectX 9.0，报告支持2D 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c439bf6b41c61469faa4e2a8db03faafe17fccd8
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067266"
---
# <a name="reporting-support-for-2d-operations-using-surface-formats"></a>报告使用图面格式执行 2D 操作的支持


## <span id="ddk_reporting_support_for_2d_operations_using_surface_formats_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_2D_OPERATIONS_USING_SURFACE_FORMATS_GG"></span>


驱动程序在[**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的**dwOperations**成员中指定了图面的格式标志，以指示它可以使用该格式执行2d 操作。

例如，驱动程序可以通过设置 D3DFORMAT \_ OP OFFSCREENPLAIN 标志来指示它可以复制到图面上或从颜色填充到图面 \_ 。

当驱动程序使用供应商提供的代码或 D3DFORMAT 枚举类型的代码设置 DDPIXELFORMAT 的 **dwFourCC** 成员并为图面分配格式时，驱动程序还可以使用 D3DFORMAT \_ OP \_ 转换 \_ 为 \_ ARGB 和 D3DFORMAT \_ MEMBEROFGROUP \_ ARGB 标志，指示是否可以在源和目标曲面之间执行颜色转换。 也就是说，具有 D3DFORMAT \_ MEMBEROFGROUP ARGB 标志集的目标图面 \_ 指示其颜色格式可转换为具有 D3DFORMAT \_ OP \_ 转换 \_ 为 \_ ARGB 标志集的任何源图面。

\_ \_ 对于每个通道至少具有5位颜色信息的目标表面格式，驱动程序只能指定 D3DFORMAT MEMBEROFGROUP ARGB 标志。 也就是说， \_ DDPIXELFORMAT 的 **dwFourCC** 成员中设置的 D3DFMT A1R5G5B5 格式有效。 但是，D3DFMT \_ A4R4G4B4 格式无效。 指定 D3DFORMAT \_ OP \_ 转换 \_ 为 \_ ARGB 标志时，驱动程序也被限制为特定的源表面格式。 源格式可以是对 D3DFORMAT \_ MEMBEROFGROUP \_ ARGB 标志或 *FOURCC* surface 格式有效的任何格式。

请注意，尽管 D3DFORMAT \_ OP \_ 转换 \_ 为 \_ argb 和 D3DFORMAT \_ MEMBEROFGROUP \_ argb 表示 ARGB 格式，但运行时还允许驱动程序指定带有 XRGB 格式的表面 (例如，D3DFMT \_ X1R5G5B5) 。 如果驱动程序指定 D3DFORMAT \_ MEMBEROFGROUP \_ ARGB 或 D3DFORMAT \_ OP \_ 转换 \_ 为 \_ 具有无效格式的 ARGB，则运行时将阻止 Direct3D HAL 加载。

 

