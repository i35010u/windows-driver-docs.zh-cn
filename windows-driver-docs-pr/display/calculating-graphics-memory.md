---
title: 计算图形内存
description: 计算图形内存
ms.assetid: 030a332b-d1f0-4a86-b11f-cfd2fbe42ac2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1da5c9c39b974691ee4b3ba58a48d1221a75d28c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384608"
---
# <a name="calculating-graphics-memory"></a>计算图形内存


它可以报告图形内存的准确帐户之前，视频内存管理器必须计算图形内存的总量。 下面的列表项的描述的视频内存管理器如何计算图形内存数字：

<span id="Total_system_memory"></span><span id="total_system_memory"></span><span id="TOTAL_SYSTEM_MEMORY"></span>系统总内存  
可以访问操作系统的系统内存的总量。 BIOS 分配的内存不会出现在此系统总内存数。 有关示例，使用 1 GB DIMM (即，1024 MB) 和的计算机还具有保留 1 MB 的内存的 BIOS 可能有 1023 MB 的系统内存。

<span id="Total_system_memory_that_is_available_for_graphics_use"></span><span id="total_system_memory_that_is_available_for_graphics_use"></span><span id="TOTAL_SYSTEM_MEMORY_THAT_IS_AVAILABLE_FOR_GRAPHICS_USE"></span>可用于图形的系统总内存  
专用或共享到 GPU 的系统内存的总量。 此数字的计算方式如下：

```cpp
TotalSystemMemoryAvailableForGraphics = MAX((TotalSystemMemory / 2), 64MB)
```

<span id="Commit_limit_on_aperture_segment"></span><span id="commit_limit_on_aperture_segment"></span><span id="COMMIT_LIMIT_ON_APERTURE_SEGMENT"></span>提交 aperture 段上的限制  
视频内存管理器允许的系统内存量显示微型端口驱动程序要在 （即，显示微型端口驱动程序的系统内存量可以通过 aperture 段的内存映射） 在任何给定时刻的 GPU 使用。 总分配并供其 GPU 的系统内存量可能会极大地; 超过提交限制但是，视频内存管理器可确保最多提交只限制量 aperture 段中实际驻留在任何时候。

默认情况下，特定 aperture 段上的则 commit limit 是该时间段的大小。 显示微型端口驱动程序可以指定不同的提交限制**CommitLimit**的成员[ **DXGK\_SEGMENTDESCRIPTOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)结构时驱动程序描述段。 在此类指定的提交限制一种方法仅适用于该驱动程序描述的特定部分。

除了每个段提交限制，所有 aperture 段上没有全局提交限制。 此全局提交限制也称为共享的系统内存。 视频内存管理器计算此值。 但是，尽管显示微型端口驱动程序可以为在较低值减小该值**ApertureSegmentCommitLimit**的成员[ **DXGK\_DRIVERCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)结构，我们并不建议这样做。

视频内存管理器不允许显示微型端口驱动程序，则每个段 commit limit 也全局提交限制不违反。 如果某一特定段的提交限制为 1 GB，但全局提交限制为 256 MB，视频内存管理器不允许显示微型端口驱动程序，以将多个 256 MB 的系统内存映射到该时间段。

<span id="Dedicated_video_memory"></span><span id="dedicated_video_memory"></span><span id="DEDICATED_VIDEO_MEMORY"></span>专用视频内存  
所有内存的大小之和的显示微型端口驱动程序未指定的这段**PopulatedFromSystemMemory**中的成员[ **DXGK\_SEGMENTFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)为每个段的结构。

<span id="Dedicated_system_memory"></span><span id="dedicated_system_memory"></span><span id="DEDICATED_SYSTEM_MEMORY"></span>专用的系统内存  
用于显示微型端口驱动程序指定的所有内存的大小之和段**PopulatedFromSystemMemory**中的成员[ **DXGK\_SEGMENTFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)每个段的结构。 此数字不能晚于可供图形使用 (TotalSystemMemoryAvailableForGraphics) 的系统总内存。

<span id="Shared_system_memory"></span><span id="shared_system_memory"></span><span id="SHARED_SYSTEM_MEMORY"></span>共享的系统内存  
最大共享到 GPU 的系统内存量。 此数字的计算方式如下：

```cpp
MaxSharedSystemMemory = TotalSystemMemoryAvailableForGraphics - DedicatedSystemMemory
```

在 GPU 上共享的系统内存量。 此数字的计算方式如下：

```cpp
SharedSystemMemory = MIN(MIN(SumOfCommitLimitOnAllApertureSegment, DXGK_DRIVERCAPS.ApertureSegmentCommitLimit), MaxSharedSystemMemory)
```

<span id="Total_video_memory"></span><span id="total_video_memory"></span><span id="TOTAL_VIDEO_MEMORY"></span>视频内存总量  
视频内存的总量。 此数字的计算方式如下：

```cpp
TotalVideoMemory = DedicatedVideoMemory + DedicatedSystemMemory + SharedSystemMemory
```

 

 





