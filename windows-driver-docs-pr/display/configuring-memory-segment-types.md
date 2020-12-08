---
title: 配置内存段类型
description: 配置内存段类型
keywords:
- 内存段 WDK 显示，配置
- 内存段 WDK 显示，类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 546b4d2c81a18c6be2961b2af4c44a35555992c4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810183"
---
# <a name="configuring-memory-segment-types"></a>配置内存段类型


## <span id="ddk_configuring_memory_segment_types_gg"></span><span id="DDK_CONFIGURING_MEMORY_SEGMENT_TYPES_GG"></span>


视频内存管理器和显示硬件仅支持某些类型的内存段，因此显示微型端口驱动程序只能配置这些类型的段。 显示微型端口驱动程序可以配置内存空间和口径区，这不同于内存空间段包含一个介质，其中包含分配的位，而口径区为虚拟地址空间。 分配内存空间段中的范围时，将分配实际内存。 分配口径区中的范围时，会将虚拟地址空间重定向到独立于视频内存池或系统内存分配的物理页面。

显示微型端口驱动程序可以配置以下类型的内存段：

-   [线性内存空间段](linear-memory-space-segments.md)

-   [线性孔径空间段](linear-aperture-space-segments.md)

-   [AGP 类型孔径空间段](agp-type-aperture-space-segments.md)

 

 





