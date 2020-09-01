---
title: SRB \_ 设置 \_ 流 \_ 状态
description: SRB \_ 设置 \_ 流 \_ 状态
ms.assetid: 8dd1237c-3b3e-4207-96b8-22311968c3a0
keywords:
- SRB_SET_STREAM_STATE 流媒体设备
topic_type:
- apiref
api_name:
- SRB_SET_STREAM_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 504830ed4435a110d7dcae7f45db4d30b53d16d6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185583"
---
# <a name="srb_set_stream_state"></a>SRB \_ 设置 \_ 流 \_ 状态


## <span id="ddk_srb_set_stream_state_ks"></span><span id="DDK_SRB_SET_STREAM_STATE_KS"></span>


类驱动程序发送此请求以设置此流的流状态。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态 \_ 未 \_ 实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态 \_ IO \_ 设备 \_ 错误  
指示出现硬件故障。

### <a name="comments"></a>注释

类驱动程序在*pSrb*CommandData 中指定新的流状态 - &gt; **CommandData**。**StreamState**。 *PSrb*指针指向[**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。 有关流状态的说明，请参阅 [**KSPROPERTY \_ 连接 \_ 状态**](ksproperty-connection-state.md) 。

微型驱动程序应将流设置为指定状态，并在 \_ 成功时返回状态 SUCCESS。 如果操作失败，则应返回相应的错误代码。

## <a name="see-also"></a>另请参阅


[SRB \_ 获取 \_ 流 \_ 状态](srb-get-stream-state.md)

 

