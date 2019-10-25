---
title: SRB\_建议\_数据\_格式
description: SRB\_建议\_数据\_格式
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
ms.openlocfilehash: 74ee1eeb67971bef4d14be795f607b4b39dfcad6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837714"
---
# <a name="srb_propose_data_format"></a>SRB\_建议\_数据\_格式


## <span id="ddk_srb_propose_data_format_ks"></span><span id="DDK_SRB_PROPOSE_DATA_FORMAT_KS"></span>


类驱动程序发出此请求，以确定流是否支持给定的数据格式。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>成功\_状态  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_未\_实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_NOT_SUPPORTED"></span><span id="status_not_supported"></span>状态\_不\_支持  
指示微型驱动程序不支持建议的格式。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>IO\_设备状态\_\_错误  
指示出现硬件故障。

### <a name="comments"></a>备注

当类驱动程序接收到[**KSPROPERTY\_连接\_PROPOSEDATAFORMAT**](ksproperty-connection-proposedataformat.md)请求时，它将使用此 SRB 代码来确定是否支持所建议的格式。 类驱动程序在**CommandData**中传递建议的数据格式。*PSrb*指向的**OpenFormat**成员。 *PSrb*指针指向[**HW\_STREAM\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。

如果微型驱动程序不支持数据格式，则它会将*pSrb*&gt;-\_不\_**支持的状态设置为 "** 状态"。 如果微型驱动程序能够将流转换为指定的格式，则会将此字段设置为 STATUS\_SUCCESS。

如果微型驱动程序能够接受新格式，则稍后的类驱动程序可以将微型驱动程序设置为格式更改，这由[**KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构中的**OptionsFlags**成员指示。

## <a name="see-also"></a>另请参阅


[**SRB\_设置\_数据\_格式**](srb-set-data-format.md)

[SRB\_获取\_数据\_格式](srb-get-data-format.md)

 

 






