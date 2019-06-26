---
title: 高阶图面渲染状态
description: 高阶图面渲染状态
ms.assetid: c664e0b8-8b96-4f66-bb9c-b87c5d5e7a05
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示高顺序图面，呈现状态
- 高顺序图面 WDK DirectX 8.0 呈现状态
- 呈现状态 WDK DirectX 8.0
- 呈现状态 WDK DirectX 8.0，高顺序图面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2190b2a4b7c3e7669bc4c6fed81ed0af0507a54f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380211"
---
# <a name="high-order-surface-render-states"></a>高阶图面渲染状态


## <span id="ddk_high_order_surface_render_states_gg"></span><span id="DDK_HIGH_ORDER_SURFACE_RENDER_STATES_GG"></span>


有三个与高顺序应用层协议一起使用的呈现状态。 这些呈现状态如下所述。

### <a name="span-idd3drspatchedgestylespanspan-idd3drspatchedgestylespand3drspatchedgestyle"></a><span id="d3drs_patchedgestyle"></span><span id="D3DRS_PATCHEDGESTYLE"></span>D3DRS\_PATCHEDGESTYLE

此呈现器状态用于控制修补程序边缘是否使用离散的还是连续分割。 请参阅更多详细信息的 DirectX 8.0 SDK 文档。

### <a name="span-idd3drspatchsegmentsspanspan-idd3drspatchsegmentsspand3drspatchsegments"></a><span id="d3drs_patchsegments"></span><span id="D3DRS_PATCHSEGMENTS"></span>D3DRS\_PATCHSEGMENTS

这呈现状态提供要用于的修补程序的每个边缘的段数。 如果段的明确的数字指定 DP2 令牌中这些段应重写此设置的值呈现状态。 有关更多详细信息，请参阅 DirectX 8.0 SDK 文档。

### <a name="span-idd3drsdeletertpatchspanspan-idd3drsdeletertpatchspan-d3drsdeletertpatch"></a><span id="d3drs_deletertpatch"></span><span id="D3DRS_DELETERTPATCH"></span> D3DRS\_DELETERTPATCH

此呈现器状态通知修补程序是要删除的驱动程序。 有关详细信息，请参阅[ **D3DRENDERSTATETYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ne-d3d9types-_d3drenderstatetype)。

 

 





