---
title: SRB \_ 设置 \_ 设备 \_ 属性
description: SRB \_ 设置 \_ 设备 \_ 属性
ms.assetid: b913cd6a-cab7-4703-af30-3066a650a0f2
keywords:
- SRB_SET_DEVICE_PROPERTY 流媒体设备
topic_type:
- apiref
api_name:
- SRB_SET_DEVICE_PROPERTY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6a24aac3ea5e59d212e32bddc0358c5e70c6fa0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186279"
---
# <a name="srb_set_device_property"></a>SRB \_ 设置 \_ 设备 \_ 属性


## <span id="ddk_srb_set_device_property_ks"></span><span id="DDK_SRB_SET_DEVICE_PROPERTY_KS"></span>


类驱动程序发送此请求以查询微型驱动程序，以获取对微型驱动程序定义的属性完成属性集请求所需的数据。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态 \_ 未 \_ 实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态 \_ IO \_ 设备 \_ 错误  
指示出现硬件故障。

### <a name="comments"></a>说明

类驱动程序将操作的参数传递到*pSrb* - &gt; **CommandData**中。**PropertyInfo** buffer，形式为[**流 \_ 属性 \_ 描述符**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_stream_property_descriptor)的结构。 *PSrb*指针指向[**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。 流属性描述符的 **属性** 成员 \_ 描述了 \_ 有问题的属性，而 **PropertyInfo** 成员指定了要从中复制属性数据的缓冲区。 如果缓冲区太小，则微型驱动程序应将*pSrb*指向的**状态**成员设置为状态 \_ 缓冲区 \_ 溢出。

有关属性集的详细信息，请参阅 [KS 属性](./ks-properties.md)。

## <a name="see-also"></a>请参阅


[**流 \_ 属性 \_ 描述符**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_stream_property_descriptor)

 

