---
title: 初始化内存段的使用
description: 初始化内存段的使用
ms.assetid: 8e4cf1dc-c428-4564-9a16-925e17e6d488
keywords:
- 内存段 WDK 显示初始化
- GPU 地址空间 WDK 显示
- 分页缓冲区 WDK 显示
- 段 WDK 显示
- 地址空间 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 076280f0f858acc4b20b56486e4b0790496404a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385183"
---
# <a name="initializing-use-of-memory-segments"></a>初始化内存段的使用


## <span id="ddk_initializing_use_of_memory_segments_gg"></span><span id="DDK_INITIALIZING_USE_OF_MEMORY_SEGMENTS_GG"></span>


适用于 Windows Vista 和更高版本 (WDDM) 的显示驱动程序模型的上下文中内存各段描述图形处理单元的 (GPU) 到视频内存管理器的地址空间。 内存段通用化和虚拟化视频内存资源。 根据硬件支持的内存类型配置内存段 （例如，帧缓冲区内存或系统内存分段）。

若要初始化它如何使用内存段，Microsoft DirectX 图形内核子系统 (Dxgkrnl.sys) 调用显示微型端口驱动程序[ *DxgkDdiQueryAdapterInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)函数。 若要直接显示微型端口驱动程序返回信息从内存段*DxgkDdiQueryAdapterInfo*调用，图形子系统指定任一配置文件**DXGKQAITYPE\_QUERYSEGMENT**或**DXGKQAITYPE\_QUERYSEGMENT3**中的值**类型**隶属[ **DXGKARG\_QUERYADAPTERINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)结构。

图形子系统调用显示微型端口驱动程序[ *DxgkDdiQueryAdapterInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)函数两次以段信息。 首次调用*DxgkDdiQueryAdapterInfo*检索的段数和支持的驱动程序，第二次调用检索有关每个段的详细的信息。 在调用*DxgkDdiQueryAdapterInfo*，驱动程序点**pOutputData**的成员[ **DXGKARG\_QUERYADAPTERINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)个填充[ **DXGK\_QUERYSEGMENTOUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)结构 （用于驱动程序版本之前 Windows 显示器驱动程序模型 (WDDM) 1.2） 或到填充[ **DXGK\_QUERYSEGMENTOUT3** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3) （对于 WDDM 1.2 和更高版本的驱动程序） 的结构。

在第一个调用中， **pSegmentDescriptor**的成员[ **DXGK\_QUERYSEGMENTOUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout) （对于 WDDM 1.2 之前的驱动程序版本） 或[ **DXGK\_QUERYSEGMENTOUT3** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3) （对于 WDDM 1.2 和更高版本的驱动程序） 设置为**NULL**。 该驱动程序应仅填充**NbSegment**的成员**DXGK\_QUERYSEGMENTOUT**或**DXGK\_QUERYSEGMENTOUT3**数它支持的段类型。 此数字还指示的即便[ **DXGK\_SEGMENTDESCRIPTOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor) （对于 WDDM 1.2 之前的驱动程序版本） 或[ **DXGK\_SEGMENTDESCRIPTOR3** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor3) （对于 WDDM 1.2 和更高版本的驱动程序） 驱动程序需要从第二次调用的结构[ *DxgkDdiQueryAdapterInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo).

在第二个调用中，该驱动程序应填充的所有成员[ **DXGK\_QUERYSEGMENTOUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)或[ **DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3). 在第二个调用中，该驱动程序应填充数组的大小**NbSegment**的[ **DXGK\_SEGMENTDESCRIPTOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)或[ **DXGK\_SEGMENTDESCRIPTOR3** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor3)中结构**pSegmentDescriptor**的成员**DXGK\_QUERYSEGMENTOUT**或**DXGK\_QUERYSEGMENTOUT3**有关驱动程序支持的段的信息。

在对这两个调用中[ *DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)，则**pInputData**隶属[ **DXGKARG\_QUERYADAPTERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)指向[ **DXGK\_QUERYSEGMENTIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentin)结构，其中包含有关位置和 AGP aperture 属性信息。 如果没有 AGP aperture 不可用，或如果不存在，但没有相应的 GART 驱动程序已安装，有关 AGP aperture 信息设置为零。 如果没有 AGP aperture 存在，则显示微型端口驱动程序不应指示，在**pSegmentDescriptor**构成的数组[ **DXGK\_QUERYSEGMENTOUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)或[ **DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)，它支持 AGP 类型 aperture 段。 如果 AGP 类型 aperture 段指示在此类情况下，适配器将无法初始化。

在初始化期间，因为内存充足，分页缓冲区可以分配的内存从特定段。 视频内存管理器中指定的段中的分页缓冲区分配内存**PagingBufferSegmentId**的成员[ **DXGK\_QUERYSEGMENTOUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)或[ **DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)。 该驱动程序指示的第二次调用中的分页缓冲区段标识符[ *DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)。 该驱动程序还应以字节为单位中的分页缓冲区应分配给指定的大小**PagingBufferSize**的成员**DXGK\_QUERYSEGMENTOUT**或**DXGK\_QUERYSEGMENTOUT3**。

有关内存段和分页缓冲区使用的详细信息，请参阅[处理内存段](handling-memory-segments.md)并[分页的视频内存资源](paging-video-memory-resources.md)。

 

 





