---
title: AGP 类型孔径空间段
description: AGP 类型孔径空间段
ms.assetid: a531f79e-541a-4454-8337-19a99aa046ae
keywords:
- 内存段 WDK 显示，AGP 类型口径-空间段
- AGP 类型口径-太空段 WDK 显示
- 口径空间段 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeb4d8bda3852129028a05bdfa53fb03b127aeb8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839077"
---
# <a name="agp-type-aperture-space-segments"></a>AGP 类型孔径空间段


## <span id="ddk_agp_type_aperture_space_segments_gg"></span><span id="DDK_AGP_TYPE_APERTURE_SPACE_SEGMENTS_GG"></span>


AGP 类型口径段类似于线性口径区，但是，显示微型端口驱动程序不会\_操作公开 DXGK\_MAP\_口径\_段和 DXGK\_操作\_取消映射\_[**DxgkDdiBuildPagingBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)回调函数通过 AGP 类型口径段。 相反，视频内存管理器使用 GART 驱动程序来映射和取消映射系统页面（也就是说，视频内存管理器不涉及显示微型端口驱动程序）。

驱动程序必须在[**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)结构的**Flags**成员中设置**agp**位域标志，才能指定 agp 类型的口径段。

 

 





