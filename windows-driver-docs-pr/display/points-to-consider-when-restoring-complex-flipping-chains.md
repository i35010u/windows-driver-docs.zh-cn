---
title: 还原复杂交替链时需考虑的要点
description: 还原复杂交替链时需考虑的要点
ms.assetid: f368576f-a0a0-4def-888d-abf4fea8f6fb
keywords:
- 上下文 WDK Direct3D，D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- 翻转链 WDK Direct3D
- Z 缓冲 WDK Direct3D
- 还原翻转链 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46e467dbbdfb02e679e7052ca69e5556d42c80e7
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066683"
---
# <a name="points-to-consider-when-restoring-complex-flipping-chains"></a>还原复杂交替链时需考虑的要点


## <span id="ddk_points_to_consider_when_restoring_complex_flipping_chains_gg"></span><span id="DDK_POINTS_TO_CONSIDER_WHEN_RESTORING_COMPLEX_FLIPPING_CHAINS_GG"></span>


当创建一个复杂的主图面时，它可能有也可能没有附加的 Z 缓冲区。 当图面恢复时，应用程序可能已将附件添加到了 Z 缓冲区。 当在 [**D3dCreateSurfaceEx**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)中通过 surface 附件列表时，驱动程序编写人员应注意到这些不同方案。

在*Perm3*示例驱动程序中提供的一种典型的方法是，当为该表面调用*D3dCreateSurfaceEx*时，将标记图面的**dwReserved1**字段。 仅当 **fpVidMem** ([**DD \_ 表面 \_ 全局**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global) 结构的成员) 不等于零时，驱动程序才会标记图面。 这是因为， **fpVidMem** 可能为零，因为该应用程序还原了具有显式附加 z 缓冲区的后台缓冲区的主表面，但 Z 缓冲区尚未还原。 稍后，应用程序将还原 Z 缓冲区，然后该驱动程序会将其标记为。 如果在还原主链之前，应用程序将还原 Z 缓冲区，则在调用 *D3dCreateSurfaceEx* 时，驱动程序可能会收到已标记的 z 缓冲区。

> [!NOTE]
> Microsoft Windows 驱动程序工具包 (WDK) 不包含 *Perm3*)  (的 3Dlabs Permedia3 示例显示驱动程序。 你可以从 Windows Server 2003 SP1 驱动程序开发工具包获取此示例驱动程序 (DDK) ，你可以从 WDHC 网站的 "Windows 驱动程序开发工具包" 页下载该驱动程序。

 

 

