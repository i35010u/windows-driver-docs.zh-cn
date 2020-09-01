---
title: SRB \_ 建议 \_ 数据 \_ 格式
description: SRB \_ 建议 \_ 数据 \_ 格式
ms.assetid: a15ec7cc-7351-4a63-ad35-e59610205913
keywords:
- SRB_PROPOSE_DATA_FORMAT 流媒体设备
topic_type:
- apiref
api_name:
- SRB_PROPOSE_DATA_FORMAT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fad0273f50ae027ef163df5c9132a7f5a34d8147
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186321"
---
# <a name="srb_propose_data_format"></a>SRB \_ 建议 \_ 数据 \_ 格式


## <span id="ddk_srb_propose_data_format_ks"></span><span id="DDK_SRB_PROPOSE_DATA_FORMAT_KS"></span>


类驱动程序发出此请求，以确定流是否支持给定的数据格式。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态 \_ 未 \_ 实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_NOT_SUPPORTED"></span><span id="status_not_supported"></span>\_不 \_ 支持的状态  
指示微型驱动程序不支持建议的格式。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态 \_ IO \_ 设备 \_ 错误  
指示出现硬件故障。

### <a name="comments"></a>说明

当类驱动程序收到 [**KSPROPERTY \_ 连接 \_ PROPOSEDATAFORMAT**](ksproperty-connection-proposedataformat.md) 请求时，它将使用此 SRB 代码来确定是否支持所建议的格式。 类驱动程序在**CommandData**中传递建议的数据格式。*PSrb*指向的**OpenFormat**成员。 *PSrb*指针指向[**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。

如果微型驱动程序不支持数据格式，则会将*pSrb* - &gt; **状态**设置为 \_ 不支持的状态 \_ 。 如果微型驱动程序能够将流转换为指定的格式，则会将此字段设置为状态 " \_ 成功"。

如果微型驱动程序能够接受新格式，则稍后的类驱动程序可以将微型驱动程序设置为格式更改，该更改由[**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构中的**OptionsFlags**成员指示。

## <a name="see-also"></a>请参阅


[**SRB \_ 设置 \_ 数据 \_ 格式**](srb-set-data-format.md)

[SRB \_ 获取 \_ 数据 \_ 格式](srb-get-data-format.md)

 

