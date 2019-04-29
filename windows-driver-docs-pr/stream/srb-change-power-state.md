---
title: SRB\_更改\_电源\_状态
description: SRB\_更改\_电源\_状态
ms.assetid: 61a3e390-1ba2-44e0-b364-e86b10937cd6
keywords:
- SRB_CHANGE_POWER_STATE 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_CHANGE_POWER_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d975d8569d98eb5bd8a00a0603627a8903446a3a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365222"
---
# <a name="srbchangepowerstate"></a>SRB\_更改\_电源\_状态


## <span id="ddk_srb_change_power_state_ks"></span><span id="DDK_SRB_CHANGE_POWER_STATE_KS"></span>


在类驱动程序将发送此请求将信号发送到微型驱动程序，它应重置其电源状态。 *pSrb*-&gt;**DeviceState**指定新的电源状态。 请参阅[ **HW\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff559702)。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_不\_实现  
指示该函数不受微型驱动程序。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示发生硬件故障，并且不能调用低能耗。

### <a name="comments"></a>备注

如果微型驱动程序需要保存或还原特定于设备的数据应该这样做时处理 SRB\_更改\_电源\_状态请求。

有关电源状态的详细信息，请参阅[管理的电源可用于单个设备](https://msdn.microsoft.com/library/windows/hardware/ff554397)。

 

 





