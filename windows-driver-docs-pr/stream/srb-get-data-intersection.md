---
title: SRB\_获取\_数据\_交集
description: SRB\_获取\_数据\_交集
ms.assetid: 67100c7f-dbca-4f75-b884-52e25a666190
keywords:
- SRB_GET_DATA_INTERSECTION 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_GET_DATA_INTERSECTION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c6d0e92d2298365c56b8d41f823d51e0447bede
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358394"
---
# <a name="srbgetdataintersection"></a>SRB\_获取\_数据\_交集


## <span id="ddk_srb_get_data_intersection_ks"></span><span id="DDK_SRB_GET_DATA_INTERSECTION_KS"></span>


在类驱动程序将发送此请求来查询数据范围中的最佳匹配数据格式的微型驱动程序。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示已找到匹配项。

### <a name="comments"></a>备注

*pSrb*-&gt;**CommandData**。**IntersectInfo**指定这两个数据区域来搜索匹配项，缓冲区返回格式。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)结构。 ( **IntersectInfo**的类型指针的成员是[**流\_数据\_INTERSECT\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_stream_data_intersect_info)结构。)

在类驱动程序将使用此请求来满足[ **KSPROPERTY\_PIN\_DATAINTERSECTION** ](ksproperty-pin-dataintersection.md)属性请求。 类驱动程序源之一[ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))时，微型驱动程序直到微型驱动程序返回与请求*pSrb* - &gt;**状态**状态的值\_成功。 微型驱动程序检查 DataRange.Specifier 值中的匹配项。

通常情况下，生成的数据格式立即用于打开该格式的流。 有关数据格式和数据区域的详细信息，请参阅[AVStream 中的数据范围交集](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)。

 

 





