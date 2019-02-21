---
title: SRB\_提议\_数据\_格式
description: SRB\_提议\_数据\_格式
ms.assetid: a15ec7cc-7351-4a63-ad35-e59610205913
keywords:
- SRB_PROPOSE_DATA_FORMAT 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_PROPOSE_DATA_FORMAT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 325f5403ad585813e81b06c3b8eb505c1a9cd5d0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555229"
---
# <a name="srbproposedataformat"></a>SRB\_提议\_数据\_格式


## <span id="ddk_srb_propose_data_format_ks"></span><span id="DDK_SRB_PROPOSE_DATA_FORMAT_KS"></span>


在类驱动程序发出此请求，以确定该流是否支持给定的数据格式。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_不\_实现  
指示该函数不受微型驱动程序。

<span id="STATUS_NOT_SUPPORTED"></span><span id="status_not_supported"></span>状态\_不\_支持  
指示建议的格式不受微型驱动程序。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示发生了硬件故障。

### <a name="comments"></a>备注

当在类驱动程序收到[ **KSPROPERTY\_连接\_PROPOSEDATAFORMAT** ](ksproperty-connection-proposedataformat.md)请求，它使用此 SRB 代码来确定是否支持此建议的格式。 在类驱动程序将传递中的建议的数据格式**CommandData**。**OpenFormat**指向成员*pSrb*。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff559702)结构。

如果微型驱动程序不支持的数据格式，它会设置*pSrb*-&gt;**状态**状态\_不\_受支持。 如果微型驱动程序能够切换到指定的格式的流，它将此字段设置为状态\_成功。

在更高版本的时间段的类驱动程序微型驱动程序是否能够接受新的格式，可能会发送微型驱动程序格式更改，这将由**OptionsFlags**中的成员[ **KSSTREAM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff567138)结构。

## <a name="see-also"></a>另请参阅


[**SRB\_SET\_DATA\_FORMAT**](srb-set-data-format.md)

[SRB\_GET\_DATA\_FORMAT](srb-get-data-format.md)

 

 






