---
title: SRB\_SET\_STREAM\_STATE
description: SRB\_SET\_STREAM\_STATE
ms.assetid: 8dd1237c-3b3e-4207-96b8-22311968c3a0
keywords:
- SRB_SET_STREAM_STATE 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_SET_STREAM_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae1db6f6fa35bf3bcde1da11534e27102e305f52
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377853"
---
# <a name="srbsetstreamstate"></a>SRB\_SET\_STREAM\_STATE


## <span id="ddk_srb_set_stream_state_ks"></span><span id="DDK_SRB_SET_STREAM_STATE_KS"></span>


在类驱动程序将发送此请求用于设置此流的流的状态。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_不\_实现  
指示该函数不受微型驱动程序。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示发生了硬件故障。

### <a name="comments"></a>备注

在类驱动程序指定新的流状态中*pSrb*-&gt;**CommandData**。**StreamState**。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)结构。 请参阅[ **KSPROPERTY\_连接\_状态**](ksproperty-connection-state.md)流状态的说明。

微型驱动程序应将该流设置为指定的状态并返回状态\_如果成功，则成功。 如果操作失败，则应返回相应的错误代码。

## <a name="see-also"></a>请参阅


[SRB\_GET\_STREAM\_STATE](srb-get-stream-state.md)

 

 






