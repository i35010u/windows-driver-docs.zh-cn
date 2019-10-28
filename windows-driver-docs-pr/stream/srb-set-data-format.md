---
title: SRB\_设置\_数据\_格式
description: SRB\_设置\_数据\_格式
ms.assetid: a111ab92-a0a0-464e-ac13-f5be33ecd064
keywords:
- SRB_SET_DATA_FORMAT 流媒体设备
topic_type:
- apiref
api_name:
- SRB_SET_DATA_FORMAT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3acabd401f734f1a4e32f5fe3552705ea252b09f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837710"
---
# <a name="srb_set_data_format"></a>SRB\_设置\_数据\_格式


## <span id="ddk_srb_set_data_format_ks"></span><span id="DDK_SRB_SET_DATA_FORMAT_KS"></span>


类驱动程序发出此请求以设置流的数据格式。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>成功\_状态  
指示命令成功完成。

<span id="STATUS_NOT_SUPPORTED"></span><span id="status_not_supported"></span>状态\_不\_支持  
指示微型驱动程序不支持所请求的数据格式。

### <a name="comments"></a>备注

类驱动程序在**CommandData**中传递新的数据格式。*PSrb*指针的**OpenFormat**成员。 （该指针指向[**HW\_流\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。）

有关数据格式的详细信息，请参阅[Stream 类微型驱动程序 Design Guide](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)。 另请参阅[AVStream 中的数据范围交集](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)。

 

 





