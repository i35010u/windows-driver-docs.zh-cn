---
title: 高阶图面渲染状态
description: 高阶图面渲染状态
keywords:
- DirectX 8.0 发行说明了 WDK Windows 2000 显示、高顺序曲面、渲染状态
- 高阶图面 WDK DirectX 8.0，呈现状态
- 呈现状态 WDK DirectX 8。0
- 呈现状态 WDK DirectX 8.0，高序位图面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a6c1ff5e8befba9f1267b6e5348cbe7eb0fc6eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838287"
---
# <a name="high-order-surface-render-states"></a>高阶图面渲染状态


## <span id="ddk_high_order_surface_render_states_gg"></span><span id="DDK_HIGH_ORDER_SURFACE_RENDER_STATES_GG"></span>


有三种渲染状态用于高顺序曲面。 下面介绍了这些呈现状态。

### <a name="span-idd3drs_patchedgestylespanspan-idd3drs_patchedgestylespand3drs_patchedgestyle"></a><span id="d3drs_patchedgestyle"></span><span id="D3DRS_PATCHEDGESTYLE"></span>D3DRS \_ PATCHEDGESTYLE

此呈现状态用于控制修补程序边缘是使用离散分割还是连续分割。 有关更多详细信息，请参阅 DirectX 8.0 SDK 文档。

### <a name="span-idd3drs_patchsegmentsspanspan-idd3drs_patchsegmentsspand3drs_patchsegments"></a><span id="d3drs_patchsegments"></span><span id="D3DRS_PATCHSEGMENTS"></span>D3DRS \_ PATCHSEGMENTS

此呈现状态提供要用于修补程序的每个边缘的段数。 如果在 DP2 标记中指定了明确数量的段，这些段应覆盖此呈现状态的值。 有关更多详细信息，请参阅 DirectX 8.0 SDK 文档。

### <a name="span-idd3drs_deletertpatchspanspan-idd3drs_deletertpatchspan-d3drs_deletertpatch"></a><span id="d3drs_deletertpatch"></span><span id="D3DRS_DELETERTPATCH"></span> D3DRS \_ DELETERTPATCH

此呈现状态通知驱动程序要删除的修补程序。 有关详细信息，请参阅 [**D3DRENDERSTATETYPE**](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3drenderstatetype)。

 

