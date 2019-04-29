---
title: D3dCreateSurfaceEx 和 MIP 贴图
description: D3dCreateSurfaceEx 和 MIP 贴图
ms.assetid: d0f4ee41-7622-4153-877c-17c88f8147a9
keywords:
- MIP 映射可呈现 WDK Direct3D
- 上下文 WDK Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19c652e50ee642e61c4e9c76ed804b7761004be6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327209"
---
# <a name="d3dcreatesurfaceex-and-mip-maps"></a>D3dCreateSurfaceEx 和 MIP 贴图


## <span id="ddk_d3dcreatesurfaceex_and_mip_maps_gg"></span><span id="DDK_D3DCREATESURFACEEX_AND_MIP_MAPS_GG"></span>


MIP 映射中的每个级别都具有不同的句柄值相关联。 这些句柄可能不是连续的但是。 Direct3D DDI 设计用于确保仅在顶级面句柄传递为中的参数**IDirect3DDevice7::SetTexture** API 方法 （Direct3D SDK 文档中介绍），然后当前的详细级别指定的纹理阶段状态 (D3DTSS\_MAXMIPLEVEL)。 使用 MIP 映射的最简单方法是生成一个端驱动程序的结构，它表示整个 MIP 映射。

 

 





