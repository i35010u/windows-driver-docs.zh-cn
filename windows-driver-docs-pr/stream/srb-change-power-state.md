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
ms.openlocfilehash: 96ebff42c50459f8d4e45921bb7656363850db1d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190363"
---
# <a name="srb_change_power_state"></a>SRB_CHANGE_POWER_STATE

类驱动程序发送此请求以便向微型驱动程序发出信号，指出应重置其电源状态。 *pSrb* ->**DeviceState**指定新电源状态。

请参阅 [**HW_STREAM_REQUEST_BLOCK**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)。

## <a name="return-value"></a>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

| 值 | 描述 |
|--|--|
| STATUS_SUCCESS | 指示命令成功完成。 |
| STATUS_NOT_IMPLEMENTED | 指示微型驱动程序不支持该函数。 |
| STATUS_IO_DEVICE_ERROR | 指示出现硬件故障且无法调用低功率。 |

## <a name="remarks"></a>备注

如果微型驱动程序需要保存或还原特定于设备的数据，则应在处理 SRB_CHANGE_POWER_STATE 请求时执行此操作。

有关电源状态的详细信息，请参阅 [适用于单个设备的电源 irp](../kernel/power-irps-for-individual-devices.md)。