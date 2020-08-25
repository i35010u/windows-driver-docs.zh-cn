---
title: SRB_CHANGE_POWER_STATE
description: SRB_CHANGE_POWER_STATE
ms.assetid: 61a3e390-1ba2-44e0-b364-e86b10937cd6
keywords:
- SRB_CHANGE_POWER_STATE 流媒体设备
topic_type:
- apiref
api_name:
- SRB_CHANGE_POWER_STATE
api_type:
- NA
ms.date: 08/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2de2e654e16da49bfabb106aafdccbb382fa6dbb
ms.sourcegitcommit: d9a9925f790271f4ca2c8377d551d96e8d1e62c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88850299"
---
# <a name="srb_change_power_state"></a>SRB_CHANGE_POWER_STATE

类驱动程序发送此请求以便向微型驱动程序发出信号，指出应重置其电源状态。 *pSrb* ->**DeviceState**指定新电源状态。

请参阅 [**HW_STREAM_REQUEST_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)。

## <a name="return-value"></a>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

| 值 | 说明 |
|--|--|
| STATUS_SUCCESS | 指示命令成功完成。 |
| STATUS_NOT_IMPLEMENTED | 指示微型驱动程序不支持该函数。 |
| STATUS_IO_DEVICE_ERROR | 指示出现硬件故障且无法调用低功率。 |

## <a name="remarks"></a>注解

如果微型驱动程序需要保存或还原特定于设备的数据，则应在处理 SRB_CHANGE_POWER_STATE 请求时执行此操作。

有关电源状态的详细信息，请参阅 [适用于单个设备的电源 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/power-irps-for-individual-devices)。
