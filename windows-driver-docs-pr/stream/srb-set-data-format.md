---
title: SRB \_ 设置 \_ 数据 \_ 格式
description: SRB \_ 设置 \_ 数据 \_ 格式
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
ms.openlocfilehash: 1b2cfef29b3c221db451ee8396543b31e99e5135
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186289"
---
# <a name="srb_set_data_format"></a>SRB \_ 设置 \_ 数据 \_ 格式


## <span id="ddk_srb_set_data_format_ks"></span><span id="DDK_SRB_SET_DATA_FORMAT_KS"></span>


类驱动程序发出此请求以设置流的数据格式。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示命令成功完成。

<span id="STATUS_NOT_SUPPORTED"></span><span id="status_not_supported"></span>\_不 \_ 支持的状态  
指示微型驱动程序不支持所请求的数据格式。

### <a name="comments"></a>注释

类驱动程序在**CommandData**中传递新的数据格式。*PSrb*指针的**OpenFormat**成员。  (此指针指向 [**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block) 结构。 ) 

有关数据格式的详细信息，请参阅 [Stream 类微型驱动程序 Design Guide](./streaming-minidrivers2.md)。 另请参阅 [AVStream 中的数据范围交集](./data-range-intersections-in-avstream.md)。

 

