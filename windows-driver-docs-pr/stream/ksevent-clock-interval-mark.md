---
title: KSEVENT\_时钟\_间隔\_标记
description: 客户端启用 KSEVENT\_时钟\_间隔\_后获得通知时达到初始时间值，然后在固定的时间增量的标记事件。
ms.assetid: 5292606e-d0b3-4e64-a236-c1cecf3fd53a
keywords:
- KSEVENT_CLOCK_INTERVAL_MARK 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_CLOCK_INTERVAL_MARK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1593765b0264780eadb5e18d76ec2ba506e6a6fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382434"
---
# <a name="kseventclockintervalmark"></a>KSEVENT\_时钟\_间隔\_标记


客户端启用 KSEVENT\_时钟\_间隔\_后获得通知时达到初始时间值，然后在固定的时间增量的标记事件。

## <span id="ddk_ksevent_clock_interval_mark_ks"></span><span id="DDK_KSEVENT_CLOCK_INTERVAL_MARK_KS"></span>


### <a name="span-ideventdataspanspan-ideventdataspanevent-data"></a><span id="event_data"></span><span id="EVENT_DATA"></span>事件数据

使用类型的结构[ **KSEVENT\_时间\_间隔**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksevent_time_interval)作为*OutBuffer*参数调用时[ **KsSynchronousDeviceControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)注册此事件。

<a name="remarks"></a>备注
-------

有关如何注册事件的信息，请参阅[KS 事件](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-events)。

 

 





