---
title: D3dCreateSurfaceEx 和 MIP 贴图
description: D3dCreateSurfaceEx 和 MIP 贴图
keywords:
- MIP 地图面 WDK Direct3D
- 上下文 WDK Direct3D，D3dCreateSurfaceEx
- D3dCreateSurfaceEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e3828b2077ba1ea34e5819edfe5b2a6d6e240ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838501"
---
# <a name="d3dcreatesurfaceex-and-mip-maps"></a>D3dCreateSurfaceEx 和 MIP 贴图


## <span id="ddk_d3dcreatesurfaceex_and_mip_maps_gg"></span><span id="DDK_D3DCREATESURFACEEX_AND_MIP_MAPS_GG"></span>


MIP 映射中的每个级别都与不同的句柄值相关联。 但这些句柄可能不是连续的。 Direct3D DDI 旨在使顶级图面控点作为自变量传递到 Direct3D SDK 文档) 中的 **IDirect3DDevice7：： SetTexture** API 方法 (，然后，当前的详细级别由纹理阶段状态 (D3DTSS \_ MAXMIPLEVEL) 指定。 使用 MIP maps 的最自然方法是构建一个表示整个 MIP 地图的驱动程序端结构。

 

 





