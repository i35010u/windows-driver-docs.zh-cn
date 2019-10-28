---
title: SRB\_读取\_数据
description: SRB\_读取\_数据
ms.assetid: b59d705d-5215-42ee-85cf-369a2e69f99b
keywords:
- SRB_READ_DATA 流媒体设备
topic_type:
- apiref
api_name:
- SRB_READ_DATA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f9daf3bbcbe6df3d124767100e2f7c33a0254e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837712"
---
# <a name="srb_read_data"></a>SRB\_读取\_数据


## <span id="ddk_srb_read_data_ks"></span><span id="DDK_SRB_READ_DATA_KS"></span>


类驱动程序已收到微型驱动程序的读取请求。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序可以将以下项之一设置为 SRB 中的状态，也可以通过其他错误代码来指示错误情况，如内存错误和错误的参数。 类驱动程序仅检查状态\_"成功"。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>成功\_状态  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_未\_实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>IO\_设备状态\_\_错误  
指示出现硬件故障。

### <a name="comments"></a>备注

*PSrb*-&gt;**CommandData**的值。**DataBufferArray**指向[**KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构的数组，它们共同描述了数据缓冲区。 *PSrb*指针指向[**HW\_STREAM\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。 *pSrb*-&gt;**CommandData**。**NumberOfBuffers**指定数组的大小。

**当微型驱动程序接收到 SRB\_READ\_数据命令时，响应的微型驱动程序例程应：**

1.  检查以确定当前流状态。 在处于 "暂停" 或 "运行" 状态时，微型驱动程序只接受读取请求。 如果流已停止，则它应立即完成并返回 SRB。

2.  将 SRB 放在队列中。

 

 





