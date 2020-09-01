---
title: KSEVENT \_ 时钟 \_ 间隔 \_ 标记
description: '\_ \_ \_ 当到达初始时间值时，客户端启用 KSEVENT 时钟间隔标记事件，然后在该时间之后的固定时间增量发出通知。'
ms.assetid: 5292606e-d0b3-4e64-a236-c1cecf3fd53a
keywords:
- KSEVENT_CLOCK_INTERVAL_MARK 流媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_CLOCK_INTERVAL_MARK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4562add4237ddfd0fe8f929b2732eee7d6d71db4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190177"
---
# <a name="ksevent_clock_interval_mark"></a>KSEVENT \_ 时钟 \_ 间隔 \_ 标记


\_ \_ \_ 当到达初始时间值时，客户端启用 KSEVENT 时钟间隔标记事件，然后在该时间之后的固定时间增量发出通知。

## <span id="ddk_ksevent_clock_interval_mark_ks"></span><span id="DDK_KSEVENT_CLOCK_INTERVAL_MARK_KS"></span>


### <a name="span-idevent_dataspanspan-idevent_dataspanevent-data"></a><span id="event_data"></span><span id="EVENT_DATA"></span>事件数据

调用[**KsSynchronousDeviceControl**](/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)注册此事件时，请使用[**KSEVENT \_ 时间 \_ 间隔**](/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_time_interval)类型的结构作为*OutBuffer*参数。

<a name="remarks"></a>备注
-------

有关如何注册事件的信息，请参阅 [KS 事件](./ks-events.md)。

 

