---
title: 配置内存段类型
description: 配置内存段类型
ms.assetid: a1fed4d6-60ae-42f2-9be0-98b667953606
keywords:
- 内存段 WDK 显示配置
- 内存段 WDK 显示类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 070df4408d3e0f6474cb31e79b01940e6087dfe6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565986"
---
# <a name="configuring-memory-segment-types"></a>配置内存段类型


## <span id="ddk_configuring_memory_segment_types_gg"></span><span id="DDK_CONFIGURING_MEMORY_SEGMENT_TYPES_GG"></span>


视频内存管理器和显示硬件仅支持某些类型的内存段，因此显示微型端口驱动程序只能配置这些类型的段。 显示微型端口驱动程序可以配置内存空间和 aperture 空间段，其中的不同在于内存空间段包含的介质上包含的分配的位，而 aperture 空间段虚拟地址空间。 分配的内存空间段中的范围后，分配实际内存。 分配的范围中的小孔空间段后，虚拟地址空间将重定向到独立地从视频内存池或系统内存分配的物理页。

显示微型端口驱动程序可以配置以下类型的内存段：

-   [线性内存空间段](linear-memory-space-segments.md)

-   [线性 Aperture 空间段](linear-aperture-space-segments.md)

-   [AGP 类型 Aperture 空间段](agp-type-aperture-space-segments.md)

 

 





