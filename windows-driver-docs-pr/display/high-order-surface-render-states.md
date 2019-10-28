---
title: 高阶图面渲染状态
description: 高阶图面渲染状态
ms.assetid: c664e0b8-8b96-4f66-bb9c-b87c5d5e7a05
keywords:
- DirectX 8.0 发行说明了 WDK Windows 2000 显示、高顺序曲面、渲染状态
- 高阶图面 WDK DirectX 8.0，呈现状态
- 呈现状态 WDK DirectX 8。0
- 呈现状态 WDK DirectX 8.0，高序位图面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16c763c9d2dad1134df88fb604d9429a9563e8b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838898"
---
# <a name="high-order-surface-render-states"></a>高阶图面渲染状态


## <span id="ddk_high_order_surface_render_states_gg"></span><span id="DDK_HIGH_ORDER_SURFACE_RENDER_STATES_GG"></span>


有三种渲染状态用于高顺序曲面。 下面介绍了这些呈现状态。

### <a name="span-idd3drs_patchedgestylespanspan-idd3drs_patchedgestylespand3drs_patchedgestyle"></a><span id="d3drs_patchedgestyle"></span><span id="D3DRS_PATCHEDGESTYLE"></span>D3DRS\_PATCHEDGESTYLE

此呈现状态用于控制修补程序边缘是使用离散分割还是连续分割。 有关更多详细信息，请参阅 DirectX 8.0 SDK 文档。

### <a name="span-idd3drs_patchsegmentsspanspan-idd3drs_patchsegmentsspand3drs_patchsegments"></a><span id="d3drs_patchsegments"></span><span id="D3DRS_PATCHSEGMENTS"></span>D3DRS\_PATCHSEGMENTS

此呈现状态提供要用于修补程序的每个边缘的段数。 如果在 DP2 标记中指定了明确数量的段，这些段应覆盖此呈现状态的值。 有关更多详细信息，请参阅 DirectX 8.0 SDK 文档。

### <a name="span-idd3drs_deletertpatchspanspan-idd3drs_deletertpatchspan-d3drs_deletertpatch"></a><span id="d3drs_deletertpatch"></span><span id="D3DRS_DELETERTPATCH"></span>D3DRS\_DELETERTPATCH

此呈现状态通知驱动程序要删除的修补程序。 有关详细信息，请参阅[**D3DRENDERSTATETYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3drenderstatetype)。

 

 





