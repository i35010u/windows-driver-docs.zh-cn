---
title: SRB\_更改\_电源\_状态
description: SRB\_更改\_电源\_状态
ms.assetid: 61a3e390-1ba2-44e0-b364-e86b10937cd6
keywords:
- SRB_CHANGE_POWER_STATE 流媒体设备
topic_type:
- apiref
api_name:
- SRB_CHANGE_POWER_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c9106a03bce351956b2bc444cd6fda3ef1913f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843314"
---
# <a name="srb_change_power_state"></a>SRB\_更改\_电源\_状态


## <span id="ddk_srb_change_power_state_ks"></span><span id="DDK_SRB_CHANGE_POWER_STATE_KS"></span>


类驱动程序发送此请求以便向微型驱动程序发出信号，指出应重置其电源状态。 *pSrb*-&gt;**DeviceState**指定新电源状态。 请参阅[**HW\_STREAM\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>成功\_状态  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_未\_实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>IO\_设备状态\_\_错误  
指示出现硬件故障且无法调用低功率。

### <a name="comments"></a>备注

如果微型驱动程序需要保存或还原特定于设备的数据，则应在处理 SRB\_更改\_POWER\_状态请求。

有关电源状态的详细信息，请参阅[管理单个设备的电源](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-power-for-individual-devices)。

 

 





