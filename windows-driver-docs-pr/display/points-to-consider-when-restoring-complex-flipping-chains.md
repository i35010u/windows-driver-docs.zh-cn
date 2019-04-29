---
title: 还原复杂交替链时需考虑的要点
description: 还原复杂交替链时需考虑的要点
ms.assetid: f368576f-a0a0-4def-888d-abf4fea8f6fb
keywords:
- 上下文 WDK Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- 翻转链 WDK Direct3D
- Z 缓冲区 WDK Direct3D
- 还原翻转链 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f96d45245fe6cb0f83c1cc8b0cd7fb4d8b50c456
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383954"
---
# <a name="points-to-consider-when-restoring-complex-flipping-chains"></a>还原复杂交替链时需考虑的要点


## <span id="ddk_points_to_consider_when_restoring_complex_flipping_chains_gg"></span><span id="DDK_POINTS_TO_CONSIDER_WHEN_RESTORING_COMPLEX_FLIPPING_CHAINS_GG"></span>


创建复杂的主图面时，它可能会或可能不具有附加的 Z 缓冲区。 还原图面后，就可以在应用程序已添加到 Z 缓冲区的附件。 时经过图面上的附件列表驱动程序编写人员应了解这些不同的方案[ **D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)。

中提供的典型技术*Perm3*示例驱动程序，是将标记一个面**dwReserved1**字段*D3dCreateSurfaceEx*调用为该图面。 该驱动程序仅将标记的图面上的 if **fpVidMem** (隶属[ **DD\_图面\_全局**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global)结构) 不等于零。 这是因为**fpVidMem**可能是零，因为该应用程序还原主图面，必须使用显式附加 Z 缓冲区，后台缓冲区，但 Z 缓冲区有尚未还原。 在某些更高版本时，应用程序还原 Z 缓冲区和驱动程序然后将其标记。 如果还原主链，该驱动程序之前的 Z 缓冲区可能会收到 Z-缓冲区，已标记，应用程序还原到后面附加缓冲区何时*D3dCreateSurfaceEx*调用。

> [!NOTE]
> Microsoft Windows Driver Kit (WDK) 不包含 3Dlabs Permedia3 示例显示器驱动程序 (*Perm3.h*)。 你可以获取从 Windows Server 2003 SP1 驱动程序开发工具包 (DDK)，可以从 DDK-WDHC 网站的 Windows 驱动程序开发工具包页面下载此示例驱动程序。

 

 

 





