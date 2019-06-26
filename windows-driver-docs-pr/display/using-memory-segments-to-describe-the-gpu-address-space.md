---
title: 使用内存段描述 GPU 地址空间
description: 使用内存段描述 GPU 地址空间
ms.assetid: 5ff23d53-0860-44fa-8ce1-c34aa22b8730
keywords:
- 内存段 WDK 显示有关内存段
- 隐藏视频内存 WDK 显示
- 视频内存管理器 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7982c5b9fb4ce6c61bc66b1239d6384f7d7c3387
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381083"
---
# <a name="using-memory-segments-to-describe-the-gpu-address-space"></a>使用内存段描述 GPU 地址空间


## <span id="ddk_using_memory_segments_to_describe_the_gpu_address_space_gg"></span><span id="DDK_USING_MEMORY_SEGMENTS_TO_DESCRIBE_THE_GPU_ADDRESS_SPACE_GG"></span>


视频内存管理器可以管理 GPU 的地址空间之前，显示微型端口驱动程序必须通过使用内存段描述的视频内存管理器对 GPU 的地址空间。 显示微型端口驱动程序创建内存段通用化和虚拟化视频内存资源。 该驱动程序可以配置根据内存段类型的内存硬件支持 （例如，帧缓冲区内存或系统内存分段）。

驱动程序在初始化期间，驱动程序必须返回描述视频内存管理器可以如何管理内存资源的段类型的列表。 该驱动程序指定它支持，并通过响应对的调用来描述每个段类型类型段的数目及其[ **DxgkDdiQueryAdapterInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)函数。 该驱动程序描述每个段使用[ **DXGK\_SEGMENTDESCRIPTOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)结构。 有关详细信息，请参阅[初始化内存段使用](initializing-use-of-memory-segments.md)。

此后的数量和类型的段保持不变。 视频内存管理器可确保每个进程在任何特定的段中收到的资源的公平份额。 视频内存管理器管理的所有段独立，并不重叠段。 因此，视频内存管理器会分配大量视频内存资源的一个段中而不考虑应用程序在从另一个段当前持有的资源量的应用程序。

该驱动程序将分配给每个其内存段的段标识符。 更高版本，当视频内存管理器请求创建的视频资源分配和呈现这些资源，则驱动程序将标识支持该请求的段并按顺序，指定驱动程序首选的视频内存管理器的段使用。 有关详细信息，请参阅[创建分配时指定段](specifying-segments-when-creating-allocations.md)。

该驱动程序不需要指定可供其内存段; 中的 GPU 的所有视频内存资源但是，该驱动程序必须指定所有视频内存管理器管理的系统上运行的所有进程之间的内存资源。 例如，实现固定的函数管道顶点着色器微代码可以驻留在 GPU 地址空间中，但不由视频内存管理器 （即，未分段的一部分），因为微代码，始终可用于所有进程的内存且永远不会发生争用的进程之间的源。 但是，视频内存管理器必须分配视频内存资源，如纹理、 顶点缓冲区呈现目标和特定于应用程序的着色器代码，从一个驱动程序的内存段，因为必须相当于所有可用的资源类型处理。

下图显示了该驱动程序配置中的 GPU 地址空间的内存段的方式。

![说明的 gpu 地址空间划分成段的关系图](images/memseg.png)

**请注意**  隐藏的视频内存管理器的视频内存不能映射到用户空间或以独占方式可用于任何特定进程。 若要执行此操作会中断虚拟内存的基本规则，需要在系统上运行的所有进程都有权访问所有内存。

 

 

 





