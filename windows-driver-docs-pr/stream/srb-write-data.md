---
title: SRB\_写入\_数据
description: SRB\_写入\_数据
ms.assetid: f7867185-3f1b-4c83-b23a-5b2b4ce6e484
keywords:
- SRB_WRITE_DATA 流媒体设备
topic_type:
- apiref
api_name:
- SRB_WRITE_DATA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 633b5e567fb32965eef2f2d01580acfa283fb806
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837698"
---
# <a name="srb_write_data"></a>SRB\_写入\_数据


## <span id="ddk_srb_write_data_ks"></span><span id="DDK_SRB_WRITE_DATA_KS"></span>


类驱动程序已收到微型驱动程序的写入请求。 *PSrb*-&gt;**CommandData**的值。**DataBufferArray**指向[**KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构的数组，它们共同描述了数据缓冲区。 *PSrb*-&gt;**CommandData**的值。**NumberOfBuffers**指定数组的大小。 *PSrb*指针指向[**HW\_STREAM\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序可以将以下项之一设置为 SRB 中的状态，也可以通过其他错误代码来指示错误情况，如内存错误和参数错误。 类驱动程序只涉及状态\_成功。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>成功\_状态  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_未\_实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>IO\_设备状态\_\_错误  
指示出现硬件故障。

## <a name="see-also"></a>另请参阅


[**SRB\_设置\_STREAM\_状态**](srb-set-stream-state.md)

 

 






