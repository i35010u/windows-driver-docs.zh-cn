---
title: SRB \_ 获取 \_ 数据 \_ 交集
description: SRB \_ 获取 \_ 数据 \_ 交集
keywords:
- SRB_GET_DATA_INTERSECTION 流媒体设备
topic_type:
- apiref
api_name:
- SRB_GET_DATA_INTERSECTION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b32b9ed92cb0e7f781340734b705ddca1e61367
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809859"
---
# <a name="srb_get_data_intersection"></a>SRB \_ 获取 \_ 数据 \_ 交集


## <span id="ddk_srb_get_data_intersection_ks"></span><span id="DDK_SRB_GET_DATA_INTERSECTION_KS"></span>


类驱动程序发送此请求，以在数据范围内查询最佳匹配数据格式的微型驱动程序。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示找到匹配项。

### <a name="comments"></a>注释

*pSrb* - pSrb &gt;**CommandData**。**IntersectInfo** 指定要在其中搜索匹配项的数据范围和返回该格式的缓冲区。 *PSrb* 指针指向 [**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。  (**IntersectInfo** 成员是指向 [**流 \_ 数据 \_ 交集 \_ 信息**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_stream_data_intersect_info) 结构的类型指针。 ) 

类驱动程序使用此请求来满足 [**KSPROPERTY \_ 引脚 \_ DATAINTERSECTION**](ksproperty-pin-dataintersection.md) 属性请求。 类驱动程序一次将一个 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85))送入微型驱动程序，直到微型驱动程序返回 *状态为 "* 成功" 的请求 - &gt; **Status** \_ 。 微型驱动程序检查 DataRange 值中是否存在匹配项。

通常，生成的数据格式会立即用于以该格式打开流。 有关数据格式和数据区域的详细信息，请参阅 [AVStream 中的数据范围交集](./data-range-intersections-in-avstream.md)。

 

