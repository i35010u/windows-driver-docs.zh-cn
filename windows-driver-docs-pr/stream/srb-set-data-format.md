---
title: SRB\_设置\_数据\_格式
description: SRB\_设置\_数据\_格式
ms.assetid: a111ab92-a0a0-464e-ac13-f5be33ecd064
keywords:
- SRB_SET_DATA_FORMAT 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_SET_DATA_FORMAT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0b97893b39d8e81e11696a6da8ceb00767eba4a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377873"
---
# <a name="srbsetdataformat"></a>SRB\_设置\_数据\_格式


## <span id="ddk_srb_set_data_format_ks"></span><span id="DDK_SRB_SET_DATA_FORMAT_KS"></span>


在类驱动程序发出此请求，以流的数据格式设置。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_SUPPORTED"></span><span id="status_not_supported"></span>状态\_不\_支持  
指示微型驱动程序不支持请求的数据格式。

### <a name="comments"></a>备注

在类驱动程序将传递中的新数据格式**CommandData**。**OpenFormat**的成员*pSrb*指针。 (此指针指向[ **HW\_流\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)结构。)

有关数据格式的详细信息，请参阅[Stream 类微型驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)。 另请参阅[AVStream 中的数据范围交集](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)。

 

 





