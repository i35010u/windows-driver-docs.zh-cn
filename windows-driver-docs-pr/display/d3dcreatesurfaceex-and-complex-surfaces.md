---
title: D3dCreateSurfaceEx 和复杂图面
description: D3dCreateSurfaceEx 和复杂图面
ms.assetid: aabe01bd-a7b8-4533-970e-4e1e49ba6596
keywords:
- 上下文 WDK Direct3D，D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- 复杂图面 WDK Direct3D
- 隐式 surface 附件 WDK Direct3D
- 显式 surface 附件 WDK Direct3D
- surface 附件 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02ce3210729bb812b8a8c10d237ab307e5a7125a
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063144"
---
# <a name="d3dcreatesurfaceex-and-complex-surfaces"></a>D3dCreateSurfaceEx 和复杂图面


## <span id="ddk_d3dcreatesurfaceex_and_complex_surfaces_gg"></span><span id="DDK_D3DCREATESURFACEEX_AND_COMPLEX_SURFACES_GG"></span>


如在 DirectDraw 文档中 [创建和销毁 directdraw](creating-and-destroying-directdraw-surfaces.md) 图面中所述，创建一个复杂的图面会导致将一个图面数组传递到 [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))。 但是，即使在复杂情况下，也只会将指向根图面的指针传递到 [**D3dCreateSurfaceEx**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)。 驱动程序需要通过根图面的附件列表，并为所有已连接的表面创建驱动端副本。 如果驱动程序尝试处理多维数据集映射或 MIP maps 的创建，这可能是一个很难操作的操作。

DirectDraw 图面附件有两种类型：隐式和显式。 隐式附件在复杂表面创建期间形成。 例如，当应用程序创建主翻转链时，主缓冲区和后台缓冲区由单个 **CreateSurface** API 调用创建，并由 **CreateSurface** 调用隐式附加到另一个。 另一个示例是 MIP map 链，其中一系列 MIP map 由单个 **CreateSurface** API 调用创建。 当**AddAttachedSurface**显式附加从不同**CreateSurface**调用创建的曲面时，将形成显式附件。

DirectX 运行时如何以及何时调用驱动程序的 [**D3dCreateSurfaceEx**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 函数，以及驱动程序如何处理图面取决于这些曲面是隐式连接还是显式附加。 如果显式附加了两个图面，则这两个图面都是通过单独的 **CreateSurface** 调用创建的，并且每个图面都将导致在表面附件建立前对 **D3dCreateSurfaceEx** 的调用。 但对于隐式附加的图面，只会对整个曲面链进行单个 **CreateSurface** 和 **D3dCreateSurfaceEx** 调用。 因此，在处理 **D3dCreateSurfaceEx** 调用时，驱动程序必须运行附加的图面列表以标识图柄，并为每个附加表面创建驱动程序端数据结构。 但是，附加 surface 列表可能包含隐式和显式连接的表面。 该驱动程序已被 **D3dCreateSurfaceEx** 的显式附加表面通知，并且可能不希望再次处理此类表面。

驱动程序可以通过 \_ 存储在[**DD \_ ATTACHLIST**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_attachlist)数据结构的**dwFlags**字段中的 DDAL 隐式标志来区分隐式和显式附件。 如果 \_ 在 **dwFlags** 字段中设置了 DDAL 隐式，则附件是隐式的，并且不会为附加表面显示单独的 [**D3dCreateSurfaceEx**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 调用。 如果未设置此标志，则附件是显式的，附加的图面将导致其自己的 **D3dCreateSurfaceEx** 调用。 通过检查此标志，驱动程序可以确定它是否必须处理连接的表面作为父图面的 **D3dCreateSurfaceEx** 调用的一部分，或者是否为附加的表面进行了单独的 **D3dCreateSurfaceEx** 调用。

有关详细信息，请参阅 [DirectDraw 驱动程序基础](directdraw-driver-fundamentals.md) 中有关 surface 附件的部分，并查看 [**D3dCreateSurfaceEx**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)中包含的示例代码。

 

