---
title: SRB\_GET\_STREAM\_INFO
description: SRB\_GET\_STREAM\_INFO
ms.assetid: ff5412ee-6e4f-43f4-a90d-4a2bdfa5d4ae
keywords:
- SRB_GET_STREAM_INFO 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_GET_STREAM_INFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55703bfffb363c27088f9f236053ac4f279d32de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358374"
---
# <a name="srbgetstreaminfo"></a>SRB\_GET\_STREAM\_INFO


## <span id="ddk_srb_get_stream_info_ks"></span><span id="DDK_SRB_GET_STREAM_INFO_KS"></span>


在类驱动程序将发送此请求可获取说明的设备和它支持的流。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示发生了硬件故障。

### <a name="comments"></a>备注

在类驱动程序将传递的缓冲区*pSrb*-&gt;**CommandData.StreamBuffer**微型驱动程序的类驱动程序的响应中指定的大小的[**SRB\_初始化\_设备**](srb-initialize-device.md)请求。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)结构。 另请参阅[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_port_configuration_information)。

微型驱动程序填充**CommandData.StreamBuffer**与[ **HW\_流\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_descriptor)设备和流描述它支持。 此缓冲区的大小将由在微型驱动程序**StreamDescriptorSize**字段中[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_port_configuration_information)结构。

在类驱动程序通常只有一次发出此请求。 微型驱动程序可能会强制类驱动程序来重新发出此请求中，若要更新的受支持的流，其说明通过调用[StreamClassReenumerateStreams](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassreenumeratestreams)。

**当 SRB\_获取\_流\_微型驱动程序收到 INFO 命令时，微型驱动程序应：**

1.  检索流标头和流信息数据结构的指针。 例如：

    ```cpp
     PHW_STREAM_HEADER pstrhdr =
      (PHW_STREAM_HEADER)&(pSrb->CommandData.StreamBuffer->StreamHeader);
     PHW_STREAM_INFORMATION pstrinfo =
      (PHW_STREAM_INFORMATION)&(pSrb->CommandData.StreamBuffer->StreamInfo);
     
    ```

2.  验证缓冲区足够大以保存返回的数据。

3.  将信息写入到缓冲区。
