---
title: 计算图形内存
description: 计算图形内存
ms.assetid: 030a332b-d1f0-4a86-b11f-cfd2fbe42ac2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfb559848f62cf286ff95eb8e0989ffe7f0e8f0c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839064"
---
# <a name="calculating-graphics-memory"></a>计算图形内存


视频内存管理器必须先计算图形内存总量，然后才能报告准确的图形内存。 以下项列表介绍了视频内存管理器如何计算图形内存号：

<span id="Total_system_memory"></span><span id="total_system_memory"></span><span id="TOTAL_SYSTEM_MEMORY"></span>系统内存总量  
操作系统可以访问的系统内存总量。 BIOS 分配的内存不会出现在此总系统内存中。 例如，使用 1 GB DIMM 的计算机（即，1024 MB），并且还有一台 BIOS 保留了 1 MB 的内存，这种情况下，系统内存可能会超过 1023 MB。

<span id="Total_system_memory_that_is_available_for_graphics_use"></span><span id="total_system_memory_that_is_available_for_graphics_use"></span><span id="TOTAL_SYSTEM_MEMORY_THAT_IS_AVAILABLE_FOR_GRAPHICS_USE"></span>可供图形使用的总系统内存  
专用或共享到 GPU 的系统内存总量。 此数字的计算方式如下：

```cpp
TotalSystemMemoryAvailableForGraphics = MAX((TotalSystemMemory / 2), 64MB)
```

<span id="Commit_limit_on_aperture_segment"></span><span id="commit_limit_on_aperture_segment"></span><span id="COMMIT_LIMIT_ON_APERTURE_SEGMENT"></span>口径段的提交限制  
在任意给定时刻，视频内存管理器允许显示微型端口驱动程序的系统内存量（即显示微型端口驱动程序的系统内存量可以通过口径段进行内存映射）。 为 GPU 分配的系统内存总量可能会大大超过提交限制;但是，在任何时候，视频内存管理器都确保最多只能在一个口径段内驻留提交限制。

默认情况下，特定光圈段的提交限制为该段的大小。 当驱动程序描述段时，显示微型端口驱动程序可以在[**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)结构的**CommitLimit**成员中指定不同的提交限制。 以这种方式指定的 commit 限制仅适用于驱动程序描述的特定段。

除了按段提交限制之外，所有口径段都有全局提交限制。 此全局提交限制也称为共享系统内存。 此值由视频内存管理器计算。 但是，尽管显示微型端口驱动程序可以将此值减少到[**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)结构的**ApertureSegmentCommitLimit**成员中的较低值，但我们不建议这样做。

视频内存管理器不允许显示微型端口驱动程序违反每个段的提交限制或全局提交限制。 如果某个特定段的提交限制为 1 GB，但全局提交限制为 256 MB，则视频内存管理器不允许显示微型端口驱动程序将超过 256 MB 的系统内存映射到该段。

<span id="Dedicated_video_memory"></span><span id="dedicated_video_memory"></span><span id="DEDICATED_VIDEO_MEMORY"></span>专用视频内存  
显示微型端口驱动程序未在每个段的[**DXGK\_SEGMENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)结构中指定**PopulatedFromSystemMemory**成员的所有内存段的大小之和。

<span id="Dedicated_system_memory"></span><span id="dedicated_system_memory"></span><span id="DEDICATED_SYSTEM_MEMORY"></span>专用系统内存  
显示微型端口驱动程序为每个段指定[**DXGK\_SEGMENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)结构中的**PopulatedFromSystemMemory**成员的所有内存段的大小之和。 此数字不能大于可供图形使用的总系统内存（TotalSystemMemoryAvailableForGraphics）。

<span id="Shared_system_memory"></span><span id="shared_system_memory"></span><span id="SHARED_SYSTEM_MEMORY"></span>共享系统内存  
为 GPU 共享的系统内存的最大数量。 此数字的计算方式如下：

```cpp
MaxSharedSystemMemory = TotalSystemMemoryAvailableForGraphics - DedicatedSystemMemory
```

共享到 GPU 的系统内存量。 此数字的计算方式如下：

```cpp
SharedSystemMemory = MIN(MIN(SumOfCommitLimitOnAllApertureSegment, DXGK_DRIVERCAPS.ApertureSegmentCommitLimit), MaxSharedSystemMemory)
```

<span id="Total_video_memory"></span><span id="total_video_memory"></span><span id="TOTAL_VIDEO_MEMORY"></span>视频内存总量  
视频内存总量。 此数字的计算方式如下：

```cpp
TotalVideoMemory = DedicatedVideoMemory + DedicatedSystemMemory + SharedSystemMemory
```

 

 





