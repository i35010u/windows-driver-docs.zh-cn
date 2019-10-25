---
title: SRB\_获取\_交集\_数据
description: SRB\_获取\_交集\_数据
ms.assetid: 67100c7f-dbca-4f75-b884-52e25a666190
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
ms.openlocfilehash: d65552fd031ce679f793cd090d43d2c4dd2f744f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843308"
---
# <a name="srb_get_data_intersection"></a>SRB\_获取\_交集\_数据


## <span id="ddk_srb_get_data_intersection_ks"></span><span id="DDK_SRB_GET_DATA_INTERSECTION_KS"></span>


类驱动程序发送此请求，以在数据范围内查询最佳匹配数据格式的微型驱动程序。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>成功\_状态  
指示找到匹配项。

### <a name="comments"></a>备注

*pSrb*-&gt;**CommandData**。**IntersectInfo**指定要在其中搜索匹配项的数据范围和返回该格式的缓冲区。 *PSrb*指针指向[**HW\_STREAM\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。 （ **IntersectInfo**成员的类型为指向[**流\_数据\_与\_信息结构相交的流**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_stream_data_intersect_info)。）

类驱动程序使用此请求来满足[**KSPROPERTY\_PIN\_DATAINTERSECTION**](ksproperty-pin-dataintersection.md)属性请求。 类驱动程序一次将一个[**KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))馈送到微型驱动程序，直到微型驱动程序返回*pSrb* **-状态的请求&gt;状态**\_SUCCESS。 微型驱动程序检查 DataRange 值中是否存在匹配项。

通常，生成的数据格式会立即用于以该格式打开流。 有关数据格式和数据区域的详细信息，请参阅[AVStream 中的数据范围交集](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)。

 

 





