---
title: SRB \_ 获取 \_ 流 \_ 信息
description: SRB \_ 获取 \_ 流 \_ 信息
keywords:
- SRB_GET_STREAM_INFO 流媒体设备
topic_type:
- apiref
api_name:
- SRB_GET_STREAM_INFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15e4e29d94ce77f9a761eba4ce97b8583b955c98
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839341"
---
# <a name="srb_get_stream_info"></a>SRB \_ 获取 \_ 流 \_ 信息


## <span id="ddk_srb_get_stream_info_ks"></span><span id="DDK_SRB_GET_STREAM_INFO_KS"></span>


类驱动程序发送此请求以获取设备及其支持的流的描述。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示命令成功完成。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态 \_ IO \_ 设备 \_ 错误  
指示出现硬件故障。

### <a name="comments"></a>注释

类驱动程序在 *pSrb* CommandData. StreamBuffer 中传递一个缓冲区，以 - &gt; **CommandData.StreamBuffer** 响应类驱动程序的 [**SRB \_ INITIALIZE \_ 设备**](srb-initialize-device.md)请求。 *PSrb* 指针指向 [**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。 另请参阅 [**端口 \_ 配置 \_ 信息**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_port_configuration_information)。

微型驱动程序使用 [**HW \_ 流 \_ 描述符**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)填充 **CommandData StreamBuffer** ，其中描述了设备及其支持的流。 此缓冲区的大小由 [**端口 \_ 配置 \_ 信息**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_port_configuration_information)结构中 **StreamDescriptorSize** 字段的微型驱动程序指示。

类驱动程序通常只颁发此请求一次。 微型驱动程序可以通过调用 [StreamClassReenumerateStreams](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassreenumeratestreams)强制类驱动程序重新发出此请求，以更新其支持的流的说明。

**当 \_ 微型驱动程序接收到 SRB 获取 \_ 流 \_ 信息命令时，微型驱动程序应：**

1.  检索流标头和流信息数据结构的指针。 例如：

    ```cpp
     PHW_STREAM_HEADER pstrhdr =
      (PHW_STREAM_HEADER)&(pSrb->CommandData.StreamBuffer->StreamHeader);
     PHW_STREAM_INFORMATION pstrinfo =
      (PHW_STREAM_INFORMATION)&(pSrb->CommandData.StreamBuffer->StreamInfo);
     
    ```

2.  验证缓冲区是否足够大以容纳返回的数据。

3.  将信息写入缓冲区。
