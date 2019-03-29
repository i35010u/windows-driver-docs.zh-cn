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
ms.openlocfilehash: ddc77408d072ae8a02a987ed3fe043843002173a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567674"
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

在类驱动程序将传递的缓冲区*pSrb*-&gt;**CommandData.StreamBuffer**微型驱动程序的类驱动程序的响应中指定的大小的[**SRB\_初始化\_设备**](srb-initialize-device.md)请求。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff559702)结构。 另请参阅[**端口\_配置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567785)。

微型驱动程序填充**CommandData.StreamBuffer**与[ **HW\_流\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff559686)设备和流描述它支持。 此缓冲区的大小将由在微型驱动程序**StreamDescriptorSize**字段中[**端口\_配置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567785)结构。

在类驱动程序通常只有一次发出此请求。 微型驱动程序可能会强制类驱动程序来重新发出此请求中，若要更新的受支持的流，其说明通过调用[StreamClassReenumerateStreams](https://msdn.microsoft.com/library/windows/hardware/ff568256)。

**当 SRB\_获取\_流\_微型驱动程序收到 INFO 命令时，微型驱动程序应：**

1.  检索流标头和流信息数据结构的指针。 例如：

    ```cpp
     PHW_STREAM_HEADER pstrhdr =
      (PHW_STREAM_HEADER)&amp;(pSrb->CommandData.StreamBuffer->StreamHeader);
     PHW_STREAM_INFORMATION pstrinfo =
      (PHW_STREAM_INFORMATION)&amp;(pSrb->CommandData.StreamBuffer->StreamInfo);
     
    ```

2.  验证缓冲区足够大以保存返回的数据。

3.  将信息写入到缓冲区。
