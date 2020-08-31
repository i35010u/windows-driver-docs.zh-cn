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
ms.openlocfilehash: 107d04ed48461e506d1faaea34154ae57960ef8a
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063178"
---
# <a name="agp-type-aperture-space-segments"></a>AGP 类型孔径空间段


## <span id="ddk_agp_type_aperture_space_segments_gg"></span><span id="DDK_AGP_TYPE_APERTURE_SPACE_SEGMENTS_GG"></span>


AGP 类型口径段类似于线性口径区，但是，显示微型端口驱动程序不会 \_ \_ \_ \_ \_ \_ \_ \_ 通过 AGP 类型口径段来显示 [**DxgkDdiBuildPagingBuffer**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) 回调函数的 DXGK 操作地图口径段和 DXGK 操作取消映射口径段操作类型。 相反，视频内存管理器使用 GART 驱动程序来映射和取消映射系统页 (也就是说，视频内存管理器不涉及显示微型端口驱动程序) 。

驱动程序必须在[**DXGK \_ SEGMENTDESCRIPTOR**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)结构的**Flags**成员中设置**agp**位域标志，才能指定 agp 类型的口径段。

 

