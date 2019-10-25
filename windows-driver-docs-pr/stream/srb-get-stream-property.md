---
title: SRB\_获取\_STREAM\_属性
description: SRB\_获取\_STREAM\_属性
ms.assetid: 579ae9b1-06f0-4f7b-afbf-c5a7df399745
keywords:
- SRB_GET_STREAM_PROPERTY 流媒体设备
topic_type:
- apiref
api_name:
- SRB_GET_STREAM_PROPERTY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1441f76b29dba92604d4991fdbae62178951410b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843304"
---
# <a name="srb_get_stream_property"></a>SRB\_获取\_STREAM\_属性


## <span id="ddk_srb_get_stream_property_ks"></span><span id="DDK_SRB_GET_STREAM_PROPERTY_KS"></span>


类驱动程序将发送此请求以查询微型驱动程序，以获取针对此流的微型驱动程序定义的属性获取属性 get 请求所需的数据。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>成功\_状态  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_未\_实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>IO\_设备状态\_\_错误  
指示出现硬件故障。

### <a name="comments"></a>备注

类驱动程序在*pSrb*-&gt;**CommandData**中传递操作的参数。**PropertyInfo** buffer，格式为[**STREAM\_属性\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_stream_property_descriptor)的结构。 *PSrb*指针指向[**HW\_STREAM\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。

STREAM\_属性\_说明符结构的**属性**成员描述了相关的属性，而**PropertyInfo**成员指定了要将属性数据复制到的缓冲区。 如果缓冲区太小，则微型驱动程序应将*pSrb*指向的**状态**成员设置为状态\_缓冲区\_溢出。

## <a name="see-also"></a>另请参阅


[**SRB\_设置\_STREAM\_属性**](srb-set-stream-property.md)

[**STREAM\_属性\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_stream_property_descriptor)

 

 






