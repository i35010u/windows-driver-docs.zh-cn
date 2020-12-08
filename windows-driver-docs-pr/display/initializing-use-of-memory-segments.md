---
title: 初始化内存段的使用
description: 初始化内存段的使用
keywords:
- 内存段 WDK 显示，初始化
- GPU 地址空间 WDK 显示
- 分页缓冲区 WDK 显示
- 显示 WDK 显示的段
- 地址空间 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79aded5fadbdcd1a3611ba8e1a6f2e4ca440c412
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827251"
---
# <a name="initializing-use-of-memory-segments"></a>初始化内存段的使用


## <span id="ddk_initializing_use_of_memory_segments_gg"></span><span id="DDK_INITIALIZING_USE_OF_MEMORY_SEGMENTS_GG"></span>


内存段，在 Windows Vista 和更高版本 (WDDM) 的显示器驱动程序模型的上下文中，描述图形处理单元的 (GPU) 地址空间到视频内存管理器。 内存段通用化并虚拟化视频内存资源。 内存段根据硬件支持的内存类型进行配置 (例如，帧缓冲区内存或系统内存口径) 。

若要初始化它如何使用内存段，Microsoft DirectX graphics 内核子系统 ( # A0) 调用显示微型端口驱动程序的 [*DxgkDdiQueryAdapterInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo) 函数。 若要指示显示微型端口驱动程序从 *DxgkDdiQueryAdapterInfo* 调用返回有关内存段的信息，图形子系统应在 [**QUERYSEGMENT3 \_ DXGKARG**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)结构的 **Type** 成员中指定 **DXGKQAITYPE \_ QUERYSEGMENT** 或 **DXGKQAITYPE \_ QUERYADAPTERINFO** 值。

对于段信息，图形子系统两次调用显示微型端口驱动程序的 [*DxgkDdiQueryAdapterInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo) 函数。 对 *DxgkDdiQueryAdapterInfo* 的第一次调用检索驱动程序支持的段数，第二次调用则检索有关每个段的详细信息。 在对 *DxgkDdiQueryAdapterInfo* 的调用中，驱动程序将 [**DXGKARG (\_ QUERYADAPTERINFO**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)的 **pOutputData** 成员指向 (wddm) 1.2) 之前的驱动程序版本，并为 wddm 1.2 和更高版本的驱动程序 [**(填充 \_**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout) [**DXGK \_ QUERYSEGMENTOUT**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)结构。

第一次调用时， [**DXGK \_ QUERYSEGMENTOUT**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)的 **pSegmentDescriptor** 成员 (用于 wddm 1.2) 的驱动程序版本或 wddm 1.2 和更高版本驱动程序的 [**DXGK \_ QUERYSEGMENTOUT3**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3) () 设置为 **NULL**。 驱动程序应仅填写 **DXGK \_ QUERYSEGMENTOUT** 或 **DXGK \_ QUERYSEGMENTOUT3** 的 **NbSegment** 成员以及它支持的段类型的数量。 此数字还指示 wddm 1.2) 或 [**DXGK \_ SEGMENTDESCRIPTOR3**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor3) (for wddm 1.2 和更) 高版本的驱动程序在第二次调用 [*DxgkDdiQueryAdapterInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)时所需的驱动程序版本的未填充 [**DXGK \_ SEGMENTDESCRIPTOR**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor) (数量。

在第二次调用中，驱动程序应填写 [**DXGK \_ QUERYSEGMENTOUT**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout) 或 [**DXGK \_ QUERYSEGMENTOUT3**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)的所有成员。 在第二次调用中，驱动程序应在 SEGMENTDESCRIPTOR3 pSegmentDescriptor 或 **DXGK \_ QUERYSEGMENTOUT** 的 **DXGK** 成员中填充数组，其大小为 **NbSegment** of [**DXGK \_ SEGMENTDESCRIPTOR**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)或 [**DXGK \_ QUERYSEGMENTOUT3**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor3)结构，其中包含驱动程序支持的段的相关信息。 **\_**

在两次调用 [*DxgkDdiQueryAdapterInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)时， [**DXGKARG \_ QUERYADAPTERINFO**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)的 **pInputData** 成员指向 [**DXGK \_ QUERYSEGMENTIN**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentin)结构，该结构包含 AGP 口径的位置和属性的相关信息。 如果没有 AGP 口径可用，或者存在，但未安装适当的 GART 驱动程序，则有关 AGP 口径的信息设置为零。 如果没有 AGP 口径，则显示微型端口驱动程序不应在 [**DXGK \_ QUERYSEGMENTOUT**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)或 [**DXGK \_ QUERYSEGMENTOUT3**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)的 **pSegmentDescriptor** 数组中指示它支持 agp 类型孔径段。 如果在这种情况下指示 AGP 类型的口径段，则适配器将无法初始化。

在初始化期间，由于内存为大量，因此可以从特定段分配分页缓冲区的内存。 视频内存管理器从 [**DXGK \_ QUERYSEGMENTOUT**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)或 [**DXGK \_ QUERYSEGMENTOUT3**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)的 **PagingBufferSegmentId** 成员中指定的段为分页缓冲区分配内存。 驱动程序指示 [*DxgkDdiQueryAdapterInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)的第二次调用中分页缓冲区段的标识符。 驱动程序还应指定为 **DXGK \_ QUERYSEGMENTOUT** 或 **DXGK \_ QUERYSEGMENTOUT3** 的 **PagingBufferSize** 成员中的分页缓冲区分配的大小（以字节为单位）。

有关内存段和使用分页缓冲区的详细信息，请参阅 [处理内存段](handling-memory-segments.md) 和 [分页视频内存资源](paging-video-memory-resources.md)。

 

