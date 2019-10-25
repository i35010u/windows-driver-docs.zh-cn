---
title: 使用内存段描述 GPU 地址空间
description: 使用内存段描述 GPU 地址空间
ms.assetid: 5ff23d53-0860-44fa-8ce1-c34aa22b8730
keywords:
- 内存段 WDK 显示，关于内存段
- 隐藏的视频内存 WDK 显示
- 视频内存管理器 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a9430586b11f180a63f6e79abf86d4b10ef5a8e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829256"
---
# <a name="using-memory-segments-to-describe-the-gpu-address-space"></a>使用内存段描述 GPU 地址空间


## <span id="ddk_using_memory_segments_to_describe_the_gpu_address_space_gg"></span><span id="DDK_USING_MEMORY_SEGMENTS_TO_DESCRIBE_THE_GPU_ADDRESS_SPACE_GG"></span>


显示微型端口驱动程序必须使用内存段将 GPU 的地址空间描述为视频内存管理器，然后才能管理 GPU 的地址空间。 显示微型端口驱动程序创建内存段来通用化和虚拟化视频内存资源。 驱动程序可以根据硬件支持的内存类型（例如，帧缓冲区内存或系统内存口径）配置内存段。

在驱动程序初始化期间，驱动程序必须返回描述内存资源如何由视频内存管理器管理的段类型的列表。 驱动程序通过响应对其[**DxgkDdiQueryAdapterInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)函数的调用来指定它支持的段类型数并描述每个段类型。 驱动程序使用[**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)结构描述每个段。 有关详细信息，请参阅[初始化使用内存段](initializing-use-of-memory-segments.md)。

此后，段的数量和类型保持不变。 视频内存管理器可确保每个进程接收到任何特定段中的资源的公平份额。 视频内存管理器独立管理所有段，段不重叠。 因此，无论应用程序当前从另一段保存多少资源，视频内存管理器都将从一个段向应用程序分配大量的视频内存资源。

驱动程序将段标识符分配给其每个内存段。 稍后，当视频内存管理器请求为视频资源创建分配并呈现这些资源时，驱动程序将标识支持请求的段并按顺序指定驱动程序首选视频内存管理器的段。用法. 有关详细信息，请参阅[创建分配时指定段](specifying-segments-when-creating-allocations.md)。

驱动程序无需指定可用于其内存段中 GPU 的所有视频内存资源;但是，驱动程序必须指定在系统上运行的所有进程中，视频内存管理器管理的所有内存资源。 例如，实现固定函数管道的顶点着色器微码可以驻留在 GPU 地址空间中，但会超出视频内存管理器管理的内存（即，不是段的一部分），因为微码始终可用于所有进程和不是进程间的争用源。 但是，视频内存管理器必须从驱动程序的内存段中分配视频内存资源，如顶点缓冲区、纹理、呈现目标和特定于应用程序的着色器代码，因为资源类型必须对所有工艺.

下图显示了驱动程序如何从 GPU 地址空间配置内存段。

![说明如何将 gpu 地址空间划分为段的关系图](images/memseg.png)

**请注意**，不能将视频内存管理器中隐藏   视频内存映射到用户空间，也不能以独占方式用于任何特定进程。 为此，需要中断系统上运行的所有进程都可以访问所有内存的基本规则。

 

 

 





