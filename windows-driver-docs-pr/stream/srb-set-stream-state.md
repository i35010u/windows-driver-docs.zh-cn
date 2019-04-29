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
ms.openlocfilehash: c48cbb6d2d0d813bc5c85b0a0a6c18401e5bb1e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392108"
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

在类驱动程序指定新的流状态中*pSrb*-&gt;**CommandData**。**StreamState**。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff559702)结构。 请参阅[ **KSPROPERTY\_连接\_状态**](ksproperty-connection-state.md)流状态的说明。

微型驱动程序应将该流设置为指定的状态并返回状态\_如果成功，则成功。 如果操作失败，则应返回相应的错误代码。

## <a name="see-also"></a>请参阅


[SRB\_GET\_STREAM\_STATE](srb-get-stream-state.md)

 

 






