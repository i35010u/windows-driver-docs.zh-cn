---
title: D3dCreateSurfaceEx 和复杂图面
description: D3dCreateSurfaceEx 和复杂图面
ms.assetid: aabe01bd-a7b8-4533-970e-4e1e49ba6596
keywords:
- 上下文 WDK Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- 复杂的图面 WDK Direct3D
- 隐式图面上附件 WDK Direct3D
- 显式图面上附件 WDK Direct3D
- WDK Direct3D 图面上附件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6252e47f23443ccde3e8a07ba15e482a40f741c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370161"
---
# <a name="d3dcreatesurfaceex-and-complex-surfaces"></a>D3dCreateSurfaceEx 和复杂图面


## <span id="ddk_d3dcreatesurfaceex_and_complex_surfaces_gg"></span><span id="DDK_D3DCREATESURFACEEX_AND_COMPLEX_SURFACES_GG"></span>


中所述[创建和销毁 DirectDraw 表面](creating-and-destroying-directdraw-surfaces.md)DirectDraw 文档中的复杂面创建会导致应用层协议传递给数组[ *DdCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)). 但是，即使在复杂的情况下，只有到根图面指针传递给[ **D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)。 它是必需的驱动程序通过根面的附件列表和创建附加的所有曲面的驱动程序端副本。 如果驱动程序尝试处理多维数据集映射或 MIP 映射创建，这可以是一个困难的操作。

有两种类型的 DirectDraw surface 附件，隐式和显式。 隐式附件是复杂的图面上创建期间生成的。 例如，当应用程序创建主翻转链时，主要和后台缓冲区创建由单个**用于 CreateSurface** API 调用并附加到另一个隐式**用于 CreateSurface**调用。 另一个示例是其中一系列 MIP 映射创建由单个 MIP 映射链**用于 CreateSurface** API 调用。 显式附件时图面创建来自不同的格式**用于 CreateSurface**显式附加调用**AddAttachedSurface**。

DirectX 运行时如何以及何时调用驾[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)函数和驱动程序如何处理图面取决于是否隐式或显式附加这些图面。 显式附加两个图面，然后这两个这些图面创建的单独调用**用于 CreateSurface**和每个面都将导致调用了**D3dCreateSurfaceEx**之前创建是图面上的附件。 但是，对于隐式附加的图面，只有一个**用于 CreateSurface**并**D3dCreateSurfaceEx**为整个链的图面进行调用。 因此，处理时**D3dCreateSurfaceEx**调用时，驱动程序必须运行图面以确定句柄并创建每个附加面的端的数据结构的驱动程序的附加的列表。 但是，附加的图面上列表可能包含混合隐式和显式附加表面。 该驱动程序将已通知的通过显式附加图面**D3dCreateSurfaceEx**和可能不需要重新处理此类表面。

该驱动程序可以区分 DDAL 通过隐式和显式附件\_隐式标记存储在**dwFlags**字段[ **DD\_ATTACHLIST**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_attachlist)数据结构。 如果 DDAL\_中设置隐式**dwFlags**字段附件是隐式和不单独[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)调用将被附加为图面。 如果未设置此标志，附件是显式附加的面会导致其自身**D3dCreateSurfaceEx**调用。 通过检查此标志，该驱动程序可以确定是否作为父图面的一部分，它必须处理的附加图面**D3dCreateSurfaceEx**调用，还是单独**D3dCreateSurfaceEx**调用将对附加的图面进行。

详细信息，请参阅部分中的图面上附件[DirectDraw 驱动程序基础知识](directdraw-driver-fundamentals.md)，并查看中包含的示例代码[ **D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)。

 

 





