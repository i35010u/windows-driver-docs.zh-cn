---
title: SRB\_设置\_流\_属性
description: SRB\_设置\_流\_属性
ms.assetid: 33a44732-a75c-4394-9839-f3c7d71d01e1
keywords:
- SRB_SET_STREAM_PROPERTY 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_SET_STREAM_PROPERTY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 148bd6efcd645b60350936ce37ab7cc774e7ae4d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377857"
---
# <a name="srbsetstreamproperty"></a>SRB\_设置\_流\_属性


## <span id="ddk_srb_set_stream_property_ks"></span><span id="DDK_SRB_SET_STREAM_PROPERTY_KS"></span>


类驱动程序将发送此请求查询微型驱动程序完成此流的微型驱动程序定义的属性上的属性集请求所需的数据。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_不\_实现  
指示该函数不受微型驱动程序。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示发生了硬件故障。

### <a name="comments"></a>备注

类驱动程序将在操作的参数传递*pSrb*-&gt;**CommandData**。**PropertyInfo**缓冲，窗体结构[**流\_属性\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_stream_property_descriptor)。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)结构。

**属性**流成员\_属性\_说明符所描述的属性有问题，同时**PropertyInfo**成员指定从其复制缓冲区属性数据。 如果缓冲区太小，微型驱动程序应设置**状态**指向成员*pSrb*到状态\_缓冲区\_溢出。

## <a name="see-also"></a>请参阅


[**SRB\_GET\_STREAM\_PROPERTY**](srb-get-stream-property.md)

[**流\_属性\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_stream_property_descriptor)

 

 






