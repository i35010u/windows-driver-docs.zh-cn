---
title: SRB\_设置\_STREAM\_状态
description: SRB\_设置\_STREAM\_状态
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
ms.openlocfilehash: ffc2e56ad0f13f607728bc35391479cbf309b139
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837703"
---
# <a name="srb_set_stream_state"></a>SRB\_设置\_STREAM\_状态


## <span id="ddk_srb_set_stream_state_ks"></span><span id="DDK_SRB_SET_STREAM_STATE_KS"></span>


类驱动程序发送此请求以设置此流的流状态。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>成功\_状态  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_未\_实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>IO\_设备状态\_\_错误  
指示出现硬件故障。

### <a name="comments"></a>备注

类驱动程序在*pSrb*中指定新的流状态-&gt;**CommandData**。**StreamState**。 *PSrb*指针指向[**HW\_STREAM\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。 有关流状态的说明，请参阅[**KSPROPERTY\_连接\_状态**](ksproperty-connection-state.md)。

微型驱动程序应将流设置为指定状态，并在成功时返回状态\_成功。 如果操作失败，则应返回相应的错误代码。

## <a name="see-also"></a>另请参阅


[SRB\_获取\_流\_状态](srb-get-stream-state.md)

 

 






