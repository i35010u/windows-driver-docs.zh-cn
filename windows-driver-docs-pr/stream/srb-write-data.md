---
title: SRB \_ 写入 \_ 数据
description: SRB \_ 写入 \_ 数据
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
ms.openlocfilehash: c19c166cca66087fa1f4f14ffb4262006c86b6cd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824863"
---
# <a name="srb_write_data"></a>SRB \_ 写入 \_ 数据


## <span id="ddk_srb_write_data_ks"></span><span id="DDK_SRB_WRITE_DATA_KS"></span>


类驱动程序已收到微型驱动程序的写入请求。 *PSrb* - &gt; **CommandData** 的值。**DataBufferArray** 指向 [**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构的数组，它们共同描述了数据缓冲区。 *PSrb* - &gt; **CommandData** 的值。**NumberOfBuffers** 指定数组的大小。 *PSrb* 指针指向 [**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序可以将以下项之一设置为 SRB 中的状态，也可以通过其他错误代码来指示错误情况，如内存错误和参数错误。 类驱动程序只涉及状态 " \_ 成功"。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态 \_ 未 \_ 实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态 \_ IO \_ 设备 \_ 错误  
指示出现硬件故障。

## <a name="see-also"></a>请参阅


[**SRB \_ 设置 \_ 流 \_ 状态**](srb-set-stream-state.md)

 

