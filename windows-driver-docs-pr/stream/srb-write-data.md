---
title: SRB\_WRITE\_DATA
description: SRB\_WRITE\_DATA
ms.assetid: f7867185-3f1b-4c83-b23a-5b2b4ce6e484
keywords:
- SRB_WRITE_DATA 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_WRITE_DATA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9c83b23fbd4e1acad95d3f6ac8c8d8a0a036cf6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377848"
---
# <a name="srbwritedata"></a>SRB\_WRITE\_DATA


## <span id="ddk_srb_write_data_ks"></span><span id="DDK_SRB_WRITE_DATA_KS"></span>


在类驱动程序收到的写入请求的微型驱动程序。 值*pSrb*-&gt;**CommandData**。**DataBufferArray**指向的数组[ **KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)结构，一起描述了数据缓冲区。 值*pSrb*-&gt;**CommandData**。**NumberOfBuffers**指定数组的大小。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)结构。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序可以将以下项之一设置为 SRB 中的状态，或者它可以传递其他错误代码，以指示错误的情况下，例如内存错误和错误的参数。 在类驱动程序只关心状态\_成功。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_不\_实现  
指示该函数不受微型驱动程序。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示发生了硬件故障。

## <a name="see-also"></a>请参阅


[**SRB\_SET\_STREAM\_STATE**](srb-set-stream-state.md)

 

 






