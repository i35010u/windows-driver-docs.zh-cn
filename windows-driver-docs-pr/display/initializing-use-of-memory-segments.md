---
title: 初始化内存段的使用
description: 初始化内存段的使用
ms.assetid: 8e4cf1dc-c428-4564-9a16-925e17e6d488
keywords:
- 内存段 WDK 显示，初始化
- GPU 地址空间 WDK 显示
- 分页缓冲区 WDK 显示
- 显示 WDK 显示的段
- 地址空间 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 586c210fd48a3dec00e52ff74822b5eb8a2ff91d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840368"
---
# <a name="initializing-use-of-memory-segments"></a>初始化内存段的使用


## <span id="ddk_initializing_use_of_memory_segments_gg"></span><span id="DDK_INITIALIZING_USE_OF_MEMORY_SEGMENTS_GG"></span>


内存段，在 Windows Vista 和更高版本（WDDM）的显示驱动程序模型的上下文中，描述了视频内存管理器的图形处理单元（GPU）地址空间。 内存段通用化并虚拟化视频内存资源。 根据硬件支持的内存类型（例如，帧缓冲区内存或系统内存口径）配置内存段。

为了初始化它如何使用内存段，Microsoft DirectX 图形内核子系统（Dxgkrnl）将调用显示微型端口驱动程序的[*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)函数。 为了指示显示微型端口驱动程序从*DxgkDdiQueryAdapterInfo*调用返回有关内存段的信息，图形子系统指定了**DXGKQAITYPE\_QUERYSEGMENT**或**DXGKQAITYPE\_** [**DXGKARG\_QUERYADAPTERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)结构的**类型**成员中的 QUERYSEGMENT3 值。

对于段信息，图形子系统两次调用显示微型端口驱动程序的[*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)函数。 对*DxgkDdiQueryAdapterInfo*的第一次调用检索驱动程序支持的段数，第二次调用则检索有关每个段的详细信息。 在对*DxgkDdiQueryAdapterInfo*的调用中，驱动程序将[**DXGKARG\_QUERYADAPTERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)的**pOutputData**成员指向填充[**DXGK\_QUERYSEGMENTOUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)结构（适用于 Windows 之前的驱动程序版本）显示驱动程序模型（WDDM）1.2）或填充[**DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)结构（适用于 WDDM 1.2 和更高版本的驱动程序）。

第一次调用时， [**DXGK\_QUERYSEGMENTOUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)的**pSegmentDescriptor**成员（适用于 wddm 1.2 之前的驱动程序版本）或[**DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3) （对于 wddm 1.2 和更高版本的驱动程序）设置为**NULL**。 驱动程序只应将**DXGK\_QUERYSEGMENTOUT**或**DXGK\_QUERYSEGMENTOUT3**的**NbSegment**成员填充到它支持的段类型的数目。 此数字还表明驱动程序所需的未填充[**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)数量（适用于 wddm 1.2 之前的驱动程序版本）或[**DXGK\_SEGMENTDESCRIPTOR3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor3) （适用于 wddm 1.2 和更高版本的驱动程序）结构对[*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)的第二次调用。

在第二次调用中，驱动程序应填写[**DXGK\_QUERYSEGMENTOUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)或[**DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)的所有成员。 在第二次调用中，驱动程序应在 SEGMENTDESCRIPTOR3 的**pSegmentDescriptor**成员中填充数组，其大小为**NbSegment** of [**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)或[**DXGK\_DXGK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor3)结构 **\_QUERYSEGMENTOUT**或**DXGK\_QUERYSEGMENTOUT3** ，其中包含驱动程序支持的段的相关信息。

在两次调用[*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)时， [**DXGKARG\_QUERYADAPTERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)的**PINPUTDATA**成员指向[**DXGK\_QUERYSEGMENTIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentin)结构，该结构包含有关的位置和属性的信息AGP 口径。 如果没有 AGP 口径可用，或者存在，但未安装适当的 GART 驱动程序，则有关 AGP 口径的信息设置为零。 如果未出现 AGP 口径，则显示微型端口驱动程序不应在[**DXGK\_QUERYSEGMENTOUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)或[**DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)的**pSegmentDescriptor**数组中指示它支持 agp 类型的口径段。 如果在这种情况下指示 AGP 类型的口径段，则适配器将无法初始化。

在初始化期间，由于内存为大量，因此可以从特定段分配分页缓冲区的内存。 视频内存管理器从[**DXGK\_QUERYSEGMENTOUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)或[**DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)的**PagingBufferSegmentId**成员中指定的段为分页缓冲区分配内存。 驱动程序指示[*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)的第二次调用中分页缓冲区段的标识符。 驱动程序还应指定应为**DXGK\_QUERYSEGMENTOUT**或**DXGK\_QUERYSEGMENTOUT3**的**PagingBufferSize**成员中的分页缓冲区分配的大小（以字节为单位）。

有关内存段和使用分页缓冲区的详细信息，请参阅[处理内存段](handling-memory-segments.md)和[分页视频内存资源](paging-video-memory-resources.md)。

 

 





